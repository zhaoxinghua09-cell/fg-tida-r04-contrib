# W3C-02 · R04 Insertion Draft (v4 · calibrated verbatim against sources 0000/0001 + red-team V1/V2 closed)

> Status: draft v4 (NOT FINAL; to be sent only after per-item confirmation at L3).
> Basis: Steven 0000.html (2026-11-01 09:38 UTC, original retrieved) + Raphael 0001.html (2026-11-01 10:48 UTC, original retrieved).
> Red-team dimension 5: PASS (V1/V2/B2 closed; B1/B3 keep the proposed marker pending the v0.2 anchor); B4 (unify dual names for one person) / B5 (provenance evidence) converged.

---

## 1. Provenance verified (Gate 4 · outsider/verification, not assertion)

- 0000.html / 0001.html **both confirmed reachable** (original retrieved via WebFetch).
- Permanent links to the primary sources (anyone can access with zero credentials): 0000 = `https://lists.w3.org/Archives/Public/public-agent-identity/2026Nov/0000.html`; 0001 = `https://lists.w3.org/Archives/Public/public-agent-identity/2026Nov/0001.html`.
- The thread subject is actually **"Re: Introduction and a hiring use case for the registry"** (not "revocation vs anonymity" — that was an early mis-labelling in a session summary, now corrected).
- Raphael's exact words (verbatim, 0001):
  > "Could you make it a short, concrete insert covering **the field and values, who records the finding, the evaluation time, and the evidence required for each result**? It would also help to show how it relates to the **existing D3 fetch statuses and NOT_EVIDENCED / NOT_DETERMINED**, so we don't introduce overlapping terms."
  > "I'll credit your proposal in the v0.2 change record and bring it back for review. We can then decide whether this belongs in the present test or in the next revision; **it isn't agreed or frozen yet**."
- Addressee/signature: 0001 `To: zhaoxinghua07@126.com`, addressed to Xinghua — i.e. Steven (Xinghua Zhao) himself. Confirms the established W3C channel (the 07 mailbox) is correct.

---

## 2. The concrete R04 insertion (PROPOSAL · reuses the values from Steven's genuine 0000 source)

**Positioning**: alongside the existing "fetch status (D3)" for credential / agent-identity presentation, add a **mandatory** "revocation evidence establishment status" field that separates the several outcomes receivers routinely conflate on the wire, so that none has to be guessed.

**Field (proposed name; must be aligned with the real v0.2 naming; does not redefine D3)**: `revocation_establishment` (**proposed**, pending confirmation of the v0.2 anchor)

**Values (reused directly from the five values in Steven's 0000 text; not invented here)**:

| Value | Meaning (verbatim from 0000) | Semantic nature |
|---|---|---|
| `recorded` | the revocation event exists and was retrieved; the bundle's own statement settles it and the countersign question does not arise | "a revocation event exists" is established |
| `not_recorded` | the source answered, and the answer was that no revocation event was recorded for the interval | **supports a negative statement** |
| `query_failed` | the source did not answer, so nothing is known either way | **supports no statement in either direction** |
| `cross_federation_unsynchronised` | a local source answered negatively, but on this federation path another authority could hold the record | local negative, but a federation path may hold a separate record |
| `undetermined` | none of the above could be established | fallback: nothing was established |

**Key invariant (from 0000)**: the field is **mandatory**; when nothing at all can be established the value **must** be `undetermined` and **must never** fall back to `recorded`. Rationale: an optional field, or one that falls back to recorded, gets left empty under delivery pressure, so every bundle looks "settled" — exactly the failure mode to be eliminated.

**Declared nature (not proof; from red-team perspective three)**: this field is **the evaluator's record of what it saw at the time**, and does not constitute a verifiable proof; its credibility rests on the evaluator's integrity and on independent re-checking by a later relying party (the relying party records its own value; see item 2 above). A reviewer should not read it as "a truth already witnessed by a third party".

**Record elements (responding to Raphael's five requirements, item by item)**:

1. **Field + values**: see the table above (five values).
2. **Who records**: the **evaluator-side**. Recorded at the same instant as the rest of the outcome, following the in-package separation rule of "evaluator result versus input". A relying party that re-queries later records its own value; the bundle must state which of the two it carries, otherwise a stale answer will be read as current — the same failure mode eliminated elsewhere in the package, closed here as well.
3. **Evaluation time and route (federation-path record)**: the value of this field, together with the **route recorded in its `evidence`** (the federation paths / authority list actually covered by this evaluation's queries; for `cross_federation_unsynchronised`, its `unsynced_path`), must be evaluated at the **same instant** as the other conditions, and must not be evaluated separately; otherwise the bundle is internally consistent at the moment of observation while carrying a route that only held earlier. (The route dimension comes from the genuine 0000 source: recording the route lets a later audit distinguish "the negative was once established and only later became unverifiable" from "the negative was never established" — different consequences for a relying party, and indistinguishable on the wire without the route. See 0000 §"Recording the route".)
4. **Evidence required for each result**:
   - `recorded`: must carry the retrieved revocation-event reference (event ID / timestamp / source).
   - `not_recorded`: must carry the source's negative answer as evidence (source, interval, answered-at time).
   - `query_failed`: must carry a query-failure record (source, time, error/timeout).
   - `cross_federation_unsynchronised`: must carry the coverage declaration for that federation path (which authorities are covered, which are not).
   - `undetermined`: must carry a record of what was attempted and why nothing was established.
5. **Relationship to the existing D3 fetch statuses / NOT_EVIDENCED / NOT_DETERMINED (avoiding overlapping terms)**:
   - "D3 fetch statuses", "NOT_EVIDENCED" and "NOT_DETERMINED" are **existing** terms in this group's registry / revocation test design, as pointed out by Raphael (0001) (see his wording: "show how it relates to the existing D3 fetch statuses and NOT_EVIDENCED / NOT_DETERMINED, so we don't introduce overlapping terms"). This insertion draft **cites these terms only and does not redefine them**; their precise normative anchor (v0.2 test specification RI-INTEROP-HIRE-001) awaits confirmation of the v0.2 change record, per §4 B3. **This draft fabricates no URL** — the exact provenance of the D3 terminology follows the official v0.2 document.
   - **D3 (fetch statuses)** answers "is the artefact retrievable / was retrieval attempted" — a **transport-layer** question.
   - **This field** answers "what has been established about the revocation negative" — a semantic question that arises **after** retrieval.
   - `NOT_DETERMINED` (D3) and this field's `undetermined` are **adjacent but differently scoped**: D3's NOT_DETERMINED = the retrieval state cannot be determined (transport); this field's `undetermined` = even though the artefact was retrieved, the revocation negative still cannot be established. **So as not to introduce overlapping terms**: this draft **does not redefine D3 and does not rename NOT_DETERMINED**; it adds only one independent, mandatory, evaluator-side field on top of D3, while the existing `NOT_EVIDENCED` stays unchanged and is not duplicated in this field.

---

## 3. Attribution / v0.2 change record

- R04 contributed by **Xinghua Zhao**, per the public-agent-identity 2026Nov thread (reply from Raphael La Touche, 0001.html); to be credited in the v0.2 change record per Raphael's statement.
- "it isn't agreed or frozen yet" → this insertion draft is a **proposal**, not adopted by the focus group, and does not imply settled status.
- Follows the existing patterns from Steven's 0000: AI-assistance disclosure + personal-capacity declaration (individual capacity, not for any organisation) + ORCID advisory-role disclosure.

---

## 4. Pre-release closure status (red-team V1 / V2 / V3 wrap-up · 2026-11-02)

- **V1 (missing route dimension · red-team hard defect)**: CLOSED. route is now explicitly defined as `evidence.route` (the federation paths / authority list actually covered by this evaluation's queries; for `cross_federation_unsynchronised` = `unsynced_path`), and aligned in three places: main draft §2.3, support package §B JSON Schema, and the demo.
- **V2 (D3 citation reachability · red-team RISK)**: CLOSED (transparent, not fabricated). Genuinely reachable sources pinned: 0000 (source of the five values and route), 0001 (Raphael's request, citing the existing D3 terms). The exact normative anchor for D3 / NOT_EVIDENCED / NOT_DETERMINED themselves (v0.2 test specification RI-INTEROP-HIRE-001) awaits the v0.2 change record per B3; this draft cites only, does not redefine, and invents no URL.
- **B1**: `revocation_establishment` remains a **proposed name**, pending the real v0.2 field name / section anchor (Raphael 0001: "it isn't agreed or frozen yet"). The proposed marker is maintained; no anchor is fabricated.
- **B2 (RFC2119)**: CHECKED. This draft uses no RFC2119 keywords as normative requirements; the descriptive "MUST align" in the support-package Schema has been changed to "aligned with (same instant)", removing the undefined 2119 keyword.
- **B3 (official D3 definition)**: as with V2, cited only; awaits the v0.2 anchor.
- **Non-proof declaration**: ADDED (§2, the "declared nature" paragraph).
- **Gate 3 conclusion**: red-team V1 / V2 / V3 closed → CONDITIONAL upgraded to **PASS** (fail-closed released), may proceed to L3 per-item confirmation. B1 is a transparently maintained proposed marker and does not constitute a blocker.

---

## 5. Gate 5 external-AI re-run note

- This v4 draft is calibrated against the genuine five-value source; red-team V1/V2 are closed (B1/B3 keep the proposed marker pending the v0.2 anchor).
- Local Ollama is unreachable (the office PC has no discrete GPU), so a local-model re-run was **BLOCKED** and was not claimed as done. It remains executable on a home PC (Ollama with GPU) or once Muse is restored.
- **Update (2026-11-17)**: an independent external review has since been executed, so Gate 5 is **no longer blocked**. It ran on SiliconFlow (`api.siliconflow.cn`) with two independent models — `deepseek-ai/DeepSeek-V4-Pro` (161 s) and `moonshotai/Kimi-K2.7-Code` (299 s); `zai-org/GLM-5.3` timed out twice and is recorded as not completed. Both successful runs concluded that the material cannot be submitted as-is; Kimi additionally identified a 64-bit truncation in the demo's evidence-chain digest, which has since been fixed to the full 256-bit value.
