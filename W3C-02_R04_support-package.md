# R04 Supporting Materials Package (companion to insertion draft v4)

> Companion main document: `W3C-02_R04_InsertionDraft.md` (v4).
> Purpose: to serve as the **supporting material and demo instance** for the R04 written submission (sent to public-agent-identity from the 07 mailbox), so that review can verify independently, without depending on attendance on site.
> Status: NOT FINAL; to be sent only after per-item confirmation at L3. Under Gate 3 red-team pressure test (B1/B2/B3 pending closure).

---

## A. Worked examples: the five values walked through one by one in a registry hiring use case

**Setting**: a hiring platform (registry) verifying an agent identity bundle uploaded by a candidate needs to reach a conclusion about "the revocation negative for that credential". The bundle carries a `revocation_establishment` field (the mandatory field proposed in this draft). Below, each value is given with a minimal bundle fragment plus a narrative.

### A.1 `recorded` — "a revocation event exists" is established
```json
{
  "revocation_establishment": {
    "value": "recorded",
    "evaluator_side": true,
    "evaluated_at": "2026-11-01T09:30:00Z",
    "evidence": {
      "event_id": "rev-9f2c...",
      "source": "ca.example.org/revocation-list",
      "retrieved_at": "2026-11-01T09:30:00Z",
      "route": { "queried_paths": ["ca.example.org/revocation-list"] }
    }
  }
}
```
Narrative: the source answered, and the answer is unambiguous — a revocation event **exists** and has been retrieved. The bundle's own statement settles the question of whether revocation occurred, and no longer triggers the "who signed / countersigned" follow-up.

### A.2 `not_recorded` — supports a negative statement
```json
{
  "revocation_establishment": {
    "value": "not_recorded",
    "evaluator_side": true,
    "evaluated_at": "2026-11-01T09:30:00Z",
    "evidence": {
      "source": "ca.example.org/revocation-list",
      "answer": "no revocation event recorded for [start,now)",
      "answered_at": "2026-11-01T09:30:00Z",
      "route": { "queried_paths": ["ca.example.org/revocation-list"] }
    }
  }
}
```
Narrative: the source **answered**, and the answer is "no revocation event recorded for that interval". This **supports a negative statement** ("not revoked within the queried interval"), but note that it is not equivalent to "never revoked" — outside that interval is not covered.

### A.3 `query_failed` — supports no statement in either direction
```json
{
  "revocation_establishment": {
    "value": "query_failed",
    "evaluator_side": true,
    "evaluated_at": "2026-11-01T09:30:00Z",
    "evidence": {
      "source": "ca.example.org/revocation-list",
      "error": "timeout after 5000ms",
      "attempted_at": "2026-11-01T09:30:00Z",
      "route": { "queried_paths": ["ca.example.org/revocation-list"] }
    }
  }
}
```
Narrative: the source **did not answer** (timeout or refusal). Nothing is therefore supported in either direction — one can say neither "not revoked" nor "revoked". This is the case most often conflated with `not_recorded` on the receiver side; this field deliberately splits them apart.

### A.4 `cross_federation_unsynchronised` — local negative, but a federation path may hold a separate record
```json
{
  "revocation_establishment": {
    "value": "cross_federation_unsynchronised",
    "evaluator_side": true,
    "evaluated_at": "2026-11-01T09:30:00Z",
    "evidence": {
      "local_source": "ca.example.org/revocation-list",
      "local_answer": "no revocation event recorded",
      "route": {
        "queried_paths": ["ca.example.org/revocation-list"],
        "unsynced_path": "federation-B / authority-C"
      },
      "coverage_note": "authority-C not yet queried / not in sync"
    }
  }
}
```
Narrative: the local source answered negatively, but on this federation path **another authority may hold that record**. The local negative therefore **does not generalise to the whole**. This distinction matters in multi-federation interoperability, and prevents the wrong conclusion "not found locally = not revoked network-wide".

### A.5 `undetermined` — the fallback; nothing was established
```json
{
  "revocation_establishment": {
    "value": "undetermined",
    "evaluator_side": true,
    "evaluated_at": "2026-11-01T09:30:00Z",
    "evidence": {
      "attempted": ["query ca.example.org (timeout)", "query federation-B (refused)"],
      "route": { "queried_paths": ["ca.example.org/revocation-list", "federation-B"] },
      "note": "neither recorded nor not_recorded nor cross_federation_unsynchronised could be established"
    }
  }
}
```
Narrative: none of the above holds. **Never fall back to `recorded`** — an optional field, or one that falls back to recorded, gets left empty under delivery pressure, making every bundle look "settled", which is exactly the failure mode to be eliminated.

---

## B. Field JSON Schema sketch (proposed; to be aligned with the real v0.2 naming)

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "revocation_establishment (PROPOSED — name pending v0.2 anchor)",
  "type": "object",
  "required": ["value", "evaluator_side", "evaluated_at", "evidence"],
  "properties": {
    "value": {
      "type": "string",
      "enum": [
        "recorded",
        "not_recorded",
        "query_failed",
        "cross_federation_unsynchronised",
        "undetermined"
      ]
    },
    "evaluator_side": { "type": "boolean", "description": "true if recorded by the evaluator-side" },
    "evaluated_at": { "type": "string", "format": "date-time", "description": "aligned with the rest of the bundle's assurance conditions (same evaluation instant)" },
    "evidence": {
      "type": "object",
      "required": ["route"],
      "description": "per-value evidence per R04 §evidence",
      "properties": {
        "route": {
          "type": "object",
          "description": "The federation path(s) actually consulted when the check ran. Recorded at the same instant as the rest of the outcome (R04 §2.3 / §evaluation-time). Source: 0000 'Recording the route'. Distinguishes 'negative was established, later became unverifiable' from 'negative was never established'.",
          "required": ["queried_paths"],
          "properties": {
            "queried_paths": { "type": "array", "items": { "type": "string" }, "description": "Authorities/registries queried at evaluation time (e.g. ca.example.org, federation-B)." },
            "unsynced_path": { "type": "string", "description": "For cross_federation_unsynchronised only: the federation path on which another authority could hold the record (required when value=cross_federation_unsynchronised)." }
          }
        }
      }
    }
  }
}
```
> Note: the field name `revocation_establishment` is a **proposed name** and must be aligned with the real v0.2 field name and section anchor (red-team item B1). This sketch does not redefine D3 and does not rename NOT_EVIDENCED / NOT_DETERMINED; `route` / `unsynced_path` have been completed against the genuine 0000 source (red-team item V1 closed).

---

## C. Boundary and invariant analysis (supporting argument for red-team dimension 5)

1. **Invariant (core)**: the field is **mandatory**; when nothing at all can be established the value **must be `undetermined`** and **must never fall back to `recorded`**. Rationale in A.5.
2. **Evaluator-side recording**: record it at the same instant as the rest of the outcome, following the in-package separation rule of "evaluator result versus input". A relying party that re-checks later records its own value; the bundle must state which one it carries, otherwise a stale answer will be read as current.
3. **Evaluation-instant alignment**: the value of this field, together with its `evidence.route` (for `cross_federation_unsynchronised`, its `unsynced_path`), must be evaluated at the **same instant** as the other conditions and must not be evaluated separately; otherwise the bundle is internally consistent while carrying a route that only held earlier.
4. **Non-overlapping mapping to existing terminology**:
   - **D3 (fetch statuses)** = whether the artefact can be retrieved / whether retrieval was attempted (**transport layer**).
   - **This field** = what is established about the revocation negative **after** retrieval (**semantic layer**).
   - `NOT_DETERMINED` (D3) is not the same as this field's `undetermined`: the former is the transport-layer statement "retrieval cannot be determined", the latter is the semantic-layer statement "even though the artefact was retrieved, the revocation negative still cannot be established". To avoid introducing overlapping terminology, this draft adds only one independent, mandatory, evaluator-side field on top of D3.
   - **Plain disclosure (red-team item V2)**: "D3 fetch statuses", "NOT_EVIDENCED" and "NOT_DETERMINED" are terms from this group's existing registry/revocation test design, as pointed out by Raphael (0001) (see the wording in 0001). This draft **cites them only and does not redefine them**; their precise normative anchor (v0.2 test specification RI-INTEROP-HIRE-001) awaits confirmation of the v0.2 change record per B3; **this draft invents no URL**. The genuinely reachable primary sources are pinned: 0000 = `https://lists.w3.org/Archives/Public/public-agent-identity/2026Nov/0000.html`, 0001 = `https://lists.w3.org/Archives/Public/public-agent-identity/2026Nov/0001.html`.

---

## D. Relationship to existing terminology (text diagram)

```
                [ credential bundle presentation ]
                          |
                [ D3: fetch statuses ]  --- transport layer: retrievable? retrieval attempted?
                          | (after successful retrieval)
                          v
          [ revocation_establishment (new in this draft, mandatory) ]  --- semantic layer: what was established about the negative?
                          |
        +-----------------+-----------------+-----------------+-----------------+
        v                 v                 v                 v                 v
   recorded        not_recorded       query_failed   cross_federation_   undetermined
   (event exists,   (source answered:  (source did     unsynchronised      (fallback; never
    retrieved)       nothing recorded)  not answer)    (local negative;     falls back to
                                                        federation may       recorded)
                                                        hold a record)
```

---

## E. Demo instance (visual)

Companion interactive demo: `R04_demo_5values.html` (single file; opens directly in a browser / attach to the 07 mailbox submission). It presents five value cards + a highlighted invariant + a clickable "bundle evaluation" mini-demo, so that reviewers can grasp the distinctions without deploying anything.

> Gate 7 note: the demo is published in the theory-account public repository `zhaoxinghua09-cell/fg-tida-r04-contrib`; anyone can run it with zero credentials: `https://github.com/zhaoxinghua09-cell/fg-tida-r04-contrib/blob/main/R04_demo_5values.html`
