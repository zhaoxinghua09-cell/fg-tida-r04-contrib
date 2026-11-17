# C5 gap analysis: what this repository corpus can and cannot serve as

**Status:** working draft. Not adopted, agreed or endorsed by any standards body.
**Measured:** 2026-11-17, against the GitHub REST API, one pass, serial with retries.
**Author:** Xinghua Zhao, independent expert, individual capacity.

This document exists because row C5 of `FG-TIDA-SUPPORTER-CONTRIBUTIONS.md` claims
empirical gap analysis of the open-source AI tool chain, and until now only a
repository sweep existed. A sweep is not an analysis. This is the analysis, and it
is deliberately narrower than the row's wording.

---

## 1. What was measured, and what was not

**Measured.** Repository-level metadata for 239 public repositories across four
accounts: `zhaoxinghua09-cell` (171), `stevenzhao07` (33), `LGD-Eval` (24),
`Medxpert-org` (11). Fields: name, description, primary language, stars, forks,
size, licence, fork status, archive status, disabled status, last push time.
239 of 239 responded; the collection was serial with a delay and three retries.

**Not measured.** No repository's contents were audited. No dependency graph was
resolved. No code was scanned for vulnerabilities. No third-party repository was
surveyed.

The last point matters most. "Gap analysis of the open-source AI tool chain" would
require surveying the tool chain, which is other people's code. What follows is a
gap analysis of **this corpus**, and its question is not "what is missing from the
ecosystem" but "what can this corpus support, and where does it fail on its own
terms". Those are different documents. Only the second one exists.

---

## 2. Seven gaps, with the numbers

Scope for all figures below: the 171 repositories of `zhaoxinghua09-cell`, the
account the C5 row refers to.

### G1 — Licence ambiguity covers 48 of 171 (28.1%)

| Licence | Count |
|---|---:|
| MIT | 82 |
| NOASSERTION (custom or unrecognised) | 37 |
| Apache-2.0 | 36 |
| none | 11 |
| CC-BY-4.0 | 4 |
| AGPL-3.0 | 1 |

Eleven repositories carry no licence at all, and thirty-seven carry a licence
GitHub cannot classify. Under default copyright, a third party may not reuse the
first group and cannot know the terms of the second without asking. A corpus that
others cannot licence is a corpus others cannot adopt, so this is the largest
practical gap in the set — larger than any missing capability.

### G2 — 55 of 171 (32.2%) are archived, yet still counted

Archived repositories are read-only and, by GitHub's own marking, retired. A third
of the corpus is in that state. Two of them exceed 100 KB, so they are not trivial
fragments. Any statement that counts "171 repositories" as an asset is counting
retired material; the operative figure is 116.

### G3 — 49 of 171 (28.7%) have never been exercised by anyone outside

Zero stars and zero forks on 49 repositories. This is not a defect in the code. It
does mean that for those 49, nobody outside has ever run them, which makes every
claim about their behaviour an author-side claim. For a standards contribution the
relevant question is which of these a stranger could run, and that is answered per
repository, not by a count.

### G4 — 22 of 171 (12.9%) are under 10 KB

A repository below 10 KB cannot hold much beyond a README and a stub. Median corpus
size is 34 KB, so these sit well under it. They are placeholders, and should be
described as placeholders rather than as parts of the corpus.

### G5 — 99 of 171 (57.9%) have no detected primary language

Documentation and scaffolding only. That is consistent with the corpus's purpose —
much of it is theory, glossary and policy text rather than code — but it means the
corpus cannot be described as a software tool chain. It is a documentation corpus
with 62 Python repositories attached.

### G6 — 92.4% of the corpus's volume is one repository

| Repository | Size |
|---|---:|
| `fhir` | 800,748 KB |
| everything else (170 repositories) | 65,828 KB |
| **total** | **866,576 KB** |

`fhir` alone is 92.4% of total bytes, against a median of 34 KB — a factor of
roughly 23,000 above the median. A single repository that dominates the corpus
this completely is almost always committed build output or data rather than
source. Nobody can clone that repository casually, and anyone quoting "total
corpus size" is quoting `fhir`.

### G7 — 12 names exist in more than one account

`uibc-core` (3 accounts), `silent-failure-catalog` (3), `medxpert-skills` (3),
`awesome-claude-skills` (2), `LGD-Eval` (2), `lgd-gate` (2), `skill-audit` (2),
`evaluation-evidence` (2), `evaluation-protocol` (2), `medxpert-fhir` (2),
`lgd-theory` (2), `.github` (4).

An outsider cannot tell which copy is authoritative, and in at least one case the
difference is material: `Medxpert-org/lgd-theory` is 12 KB and archived, while
`zhaoxinghua09-cell/lgd-theory` is 5,472 KB and active. Both are called
`lgd-theory`. A citation to "lgd-theory" resolves to whichever the reader picks.

---

## 3. What this supports, and what it does not

**Supported.** This corpus is a documentation and policy body with 62 active Python
repositories, of which one (the verifier described in the conformance surface) can
be run by a stranger with no credentials and no configuration. The corpus's
licensing is mostly clear (123 of 171 carry a recognisable licence) but a quarter
is not. A third is retired. Two thirds has never been run from outside.

**Not supported.** Any statement that the corpus is a tool chain. Any statement
that its size represents capability. Any statement about the wider open-source
ecosystem, because the wider ecosystem was not surveyed.

---

## 4. What would close each gap

| Gap | Closeable by |
|---|---|
| G1 licence ambiguity | Adding a licence file to the 11 unlicensed repositories; replacing the 37 custom licences with SPDX-recognisable text, or stating in each README that the custom terms are intentional |
| G2 archived material | Either un-archiving what is still maintained, or stating the operative count (116) wherever the corpus is described |
| G3 no external exercise | Per-repository outsider runs, reported individually; this is work, not a statement |
| G4 stubs | Renaming or clearly labelling them as stubs |
| G5 no language | Already accurate; the corpus should stop being described in software terms |
| G6 volume concentration | Checking whether `fhir` commits build output; if so, removing it from history or stating that clones are large |
| G7 duplicate names | Deciding one authoritative copy per name and archiving or renaming the others with a pointer |

None of these is done as of 2026-11-17. They are listed so that a reviewer can
check them, not to suggest they have been addressed.

---

## 5. Reproducing this

The figures come from a single API pass over the four accounts' repository
metadata, saved as JSON and re-counted with a script, not read off the GitHub web
interface. Anyone repeating it on a later date will get different totals: archive
state, licence recognition and star counts all move. The date of measurement is
part of the result, which is why it appears at the top of this page.
