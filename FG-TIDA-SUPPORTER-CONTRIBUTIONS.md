# FG-TIDA SUPPORTER CONTRIBUTIONS — contribution proposal
# (zhaoxinghua09-cell, individual · supporter positioning, offering contribution points)

> Maintained by: zhaoxinghua09-cell (individual contributor) | In effect from: 2026-10-14 | Basis: the full FG-TIDA Terms of Reference (itu.int/en/ITU-T/focusgroups/tida/Pages/ToR.aspx)
> **Positioning statement: I participate in FG-TIDA as a supporter — not leading, not duplicating, not overstepping; offering, per the ToR, the contribution points I am able to support, for the focus group to adopt by consensus.**

---

## 1. Supporter positioning

| Dimension | Our position |
|---|---|
| Role | Supporter / contributor, not an agenda leader |
| Principle | Complies with ITU A.7: no duplication of existing study group / focus group work; whether a contribution is taken up is decided by focus group consensus |
| Boundary | Does not touch FG-TIDA out-of-scope areas: agentic AI protocols / AI governance / national digital identity content |
| Stance | I offer contribution points on a "usable is contributed" basis; the right of adoption rests with the focus group, with no commitment to adoption |
| Identity | Four accounts with separated roles (theory, evaluation, product, organisation), one signature identity per contribution package, to avoid role conflict |

> **Keyword discipline**: contributions use FG-TIDA language (trust management / lifecycle assurance / continuous assessment / accountability / behavioural signals), and do **not** take "AI governance" as a theme keyword (the ToR explicitly places it out of scope).

---

## 2. Contribution points (ordered by strength of authoritative backing)

### P0 core contribution points

| # | Contribution point | Corresponding ToR item | Our authoritative backing |
|---|---|---|---|
| C1 | **Trust lifecycle framework**: establish → continuous assessment → downgrade → revoke, with evidence standards at each stage | Annex A.2.2 | The LGD end-to-end governance theory (Registry · Evidence · Gates), held in **`zhaoxinghua09-cell/lgd-theory`** — that is the repository carrying the theory text (`.zenodo.json`, `CITATION.cff`, `CHANGELOG.md` present). P0/P3 papers: DOI 10.5281/zenodo.22456647. Note: a same-named repository exists under the organisation account (`Medxpert-org/lgd-theory`); it holds only community templates and is archived — **it is not the theory text**. |
| C2 | **Assessment criteria and benchmarks**: methods for assessing trustworthiness / interoperability / accountability / human oversight, including evidence grading and bias control | ToR 3.4 / 4.5 | The full evaluation-account set: authoritative criteria (five-level reading, Verified → Preliminary), test-expert handbook L0–L13, multi-judge plus human anchoring, AB/BA bias control, GRADE evidence grading, OWASP/NIST/ISO standard mapping |
| C3 | **Behavioural trust signals and silent failures**: behavioural baselines, anomaly detection, evidence data model | Annex A.2.8 | The Silent Failure Catalog plus an evaluation evidence chain (hash / .ots / manifest) — the detection domain for "no error was raised but it was wrong" |
| C4 | **Terminology and definitions package**: registration / evidence / gates as interoperable terms | ToR 3.1 | lgd-glossary (bilingual definitions, versioned revision history) |

### P1 strong contribution points

| # | Contribution point | Corresponding ToR item | Our authoritative backing |
|---|---|---|---|
| C5 | **Security gap analysis of open-source agents** | Annex A.1.8 | A repository-level sweep of the theory account's **171 public repositories** (size, licence, archive state, language, activity), plus a skill-audit scanner and a proactive evaluation regime. Status: **repository sweep completed; the written gap report is not yet available.** Empirical gap analysis of the open-source AI tool chain is precisely this item. |
| C6 | **Human oversight integration framework**: intervention triggers / escalation criteria / audit trail / responsibility allocation | Annex A.2.4 | The principle that issuing authority rests with a human (criterion P7), two independent reviewers plus a third adjudicator, procedural justice (14-day response / 24-hour correction / right to present a rejoinder) |
| C7 | **Machine-readable trust metadata**: the intended approach | ToR 4.4 | Three files per repository: a Schema.org-compatible `schema.jsonld` describing the work and its parts, a `.zenodo.json` for archiving, and a `CITATION.cff`. **Status: present in all four contribution repositories, checked 2026-11-17.** All three files declare the material as a draft, not adopted and not submitted. Each repository's `hasPart` list was written from that repository's own file list, not copied between repositories, and each cites the theory record DOI as `isReferencedBy` while stating that it is not the DOI of these drafts. |

### P2 use-case contribution

| # | Contribution point | Corresponding ToR item | Our authoritative backing |
|---|---|---|---|
| C8 | **Industry use case: medical-device compliance tool chain (anonymised) field test** | ToR 4.1 / A.3.1 | Field-test report on a medical-device compliance tool chain (anonymised) plus anonymised field-test evidence (real deployment evidence, signed in the capacity of the use-case provider / individual) |

---

## 3. Account separation matrix (four accounts, distinct, non-conflicting)

| Account | Role | Contribution content | Signature identity | Non-conflict rule |
|---|---|---|---|---|
| **zhaoxinghua09-cell** (theory account) | Source of theory | C1 lifecycle framework (theory version), C4 terminology | Theory author (cites the DOI) | Theory originates only from the lgd-theory SSOT; the evaluation account does not republish theory |
| **LGD-Eval** (evaluation account) | Independent evaluation execution (personal project) | C2 assessment criteria / benchmarks, C3 silent failures / evidence, C5 gap analysis, C6 human oversight, C7 metadata | Independent evaluation execution (personal project) | Cites the theory account's DOI; does not invent its own version of the theory; does not write as the evaluated party |
| **stevenzhao07** (product account · MedXpert product tool-chain GitHub account) | Tool-chain implementation | C8 use case (anonymised field test of a medical-device compliance tool chain) | Tool-chain implementer (use-case provider, individual capacity) | Only as tested party / use-case provider; does not take part in drafting the standard text |
| **Medxpert-org** (organisation account) | Organisation-level publication | Organisational assets kept separate from the three individual accounts | Organisation | Kept distinct from the three personal accounts; no duplicate submission of the same content |

> Note — **which mailbox to use, stated explicitly**. The two mailboxes are platform-specific and are never mixed:
> - **`zhaoxinghua06@126.com`** — the **ITU** mailbox. This is the address used to register at itu.int and to sign in to the FG-TIDA work area; it is the contact address for anything submitted to ITU.
> - **`zhaoxinghua07@126.com`** — the **W3C** standards-participation mailbox. This is the address that received W3C comment 0001; it is used for W3C correspondence.
>
> Separately, `stevenzhao07` is the MedXpert product tool-chain **GitHub account** — a GitHub identity, not a mailbox, and not to be confused with the 07 mailbox. The division of labour across all four GitHub accounts is recorded in `THREE_ACCOUNT_ACTION_PLAN.md`.

**Four conflict-avoidance rules**:
1. One contribution package carries exactly one identity (never co-bidding on the same work item).
2. The same content is never submitted twice under two accounts.
3. Theory versions always cite lgd-theory (DOI); any paraphrase defers to the SSOT.
4. Externally, everything is presented in an individual capacity (the accounts divide the work, each with its role); ITU correspondence uses the single coordinating mailbox **`zhaoxinghua06@126.com`**; W3C correspondence uses **`zhaoxinghua07@126.com`**. The coordinating mailbox for ITU is therefore a single, named address, so a rapporteur or the secretariat has exactly one point of contact.
5. **The four accounts are four separate GitHub logins, not one account with four labels.** Each has its own credentials. **The check performed, and its limit:** the credential used in this session authenticates as `zhaoxinghua09-cell`, and that is also the owner of the repositories written to here. This is a statement about the credential in use, **not** a claim that no account can ever write to another owner's repository — GitHub does permit that when write access is granted (collaborator, deploy key or app), and a pushed commit's author field is not proof of which credential pushed it. **A historical audit of every commit across all four accounts has not been performed**, so no such claim is made here.

---

## 4. Supporter action list

| Timing | Action | Status |
|---|---|---|
| Now | Register a free ITU account (itu.int) and subscribe to the FG-TIDA mailing list (fgtida@lists.itu.int) | DONE — ITU account registered; mailing-list subscription to be confirmed |
| Now | Contact the focus group secretariat tsbfgtida@itu.int: state supporter identity and contribution intent (with C1/C2 summaries) | Pending — requires the account holder |
| 2026-10 | Draft the C1 (trust lifecycle framework) and C2 (assessment criteria and benchmarks) contribution texts (ITU input-document template) | In preparation in this repository |
| 2026-11-30 / 12-01 | FG-TIDA first face-to-face meeting (UNESCO HQ, Paris) — participate on site or by remote registration | Pre-registration due 2026-11-20 |
| 2027-01-26 / 27 | Second meeting (Geneva): submit revised contribution texts | Planned |
| Continuous | C5 gap analysis submitted as the 171-repository sweep completes; C8 use case submitted in the AI for Good window | Planned |

> The contribution input-document template is on the FG-TIDA site under Templates (Input documents / Technical Report / Technical Specification); the working language is English.

---

## 5. Supporter credibility undertakings

1. **Originality**: every contribution point carries first-origin evidence (DOI / .ots / plagiarism-check report); no claim of priority that cannot be shown.
2. **Verifiability**: contribution content comes with public repository links and field-test evidence, so ITU can verify independently.
3. **Neutrality**: non-commercial, no advocacy position, no regional bias; only the best version available is offered.
4. **Transparency**: whether a contribution is adopted is recorded openly; no promises, no exaggeration.

---

*Evaluating Autonomy. Verifying Governance.*
