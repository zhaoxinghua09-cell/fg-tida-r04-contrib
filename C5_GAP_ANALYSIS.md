# C5 gap analysis: what this repository corpus can and cannot serve as

**Status:** working draft. Not adopted, agreed or endorsed by any standards body.
**Measured:** 2026-11-17, against the GitHub REST API, one pass, serial with retries.
**Author:** Xinghua Zhao, independent expert, individual capacity.

Row C5 of `FG-TIDA-SUPPORTER-CONTRIBUTIONS.md` originally named an empirical gap
analysis of the open-source AI tool chain. That analysis does not exist in this
document and is not going to be produced here: it would require surveying other
people's repositories, and none were surveyed. What this document is instead is a
gap analysis of **this corpus against its own claims**, measured from repository
metadata. The difference is stated here, in section 1, and in the C5 row itself
rather than left for a reader to discover.

**It is also not a security analysis**, and the C5 row's earlier label said it was.
No code was read, no dependency resolved, no vulnerability scanned. What follows
is a provenance, licensing and hygiene analysis. The security half of Annex A.1.8
is not served by this document and the row now says so.

---

## 1. What was measured, and what was not

**Two measurements, of different kinds — they should not be read as one.**

*Measurement A:* repository-level metadata for 239 public repositories across four
accounts — `zhaoxinghua09-cell` (171), `stevenzhao07` (33), `LGD-Eval` (24),
`Medxpert-org` (11). Fields: name, description, primary language, stars, forks,
size, licence, fork status, archive status, disabled status, last push time.
239 of 239 responded; the collection was serial with a delay and three retries.
Nothing in sections 2 and 3 comes from anywhere else.

*Measurement B:* one repository was actually run. The verifier in
`conformance-surface-2026-11` was executed from a clean local copy on 2026-11-17
with no credentials and no network: 27 assertions, all passing, exit code 0.
That is a measurement of one repository, not of the corpus, and it is the only
place in this document where anything was executed rather than described.

**Not measured.** No repository's contents were audited. No dependency graph was
resolved. No code was scanned for vulnerabilities. No third-party repository was
surveyed.

The last point decides what this document can claim. "Gap analysis of the
open-source AI tool chain" would require surveying the tool chain, which is other
people's code. What follows answers a different question: not "what is missing
from the ecosystem" but "what can this corpus support, and where does it fail on
its own terms". A reviewer asking for the former still has nothing to hand over.

---

## 2. Seven gaps, with the numbers

Scope for all figures below: the 171 repositories of `zhaoxinghua09-cell`, the
account the C5 row refers to. Every figure is from Measurement A unless marked.

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
practical gap in the set — larger than any missing capability, and the one a
reader hits first when trying to build on anything here.

48 of 171 is 28.1%, more than a quarter. It is not "a quarter" and this document
does not round it down.

### G2 — 55 of 171 (32.2%) are archived, yet still counted

Archived repositories are read-only and, by GitHub's own marking, retired. Nearly
a third of the corpus is in that state. Two of them exceed 100 KB, so they are not
trivial fragments. Any statement that counts "171 repositories" as an asset is
counting retired material; the operative figure is 116.

### G3 — 49 of 171 (28.7%) carry no recorded external use

Zero stars and zero forks on 49 repositories.

The honest reading of that number is narrower than it looks. **A clone leaves no
trace: no stars and no forks is not evidence that nobody ever ran these
repositories.** It is evidence that no use was *recorded*. What it does support is
that any claim about how those 49 behave is author-side: it rests on the author's
own runs, and a reader cannot see that anyone independent has repeated them. For a
standards contribution the relevant question is which of these a stranger could
run, and that is answered per repository, not by a count.

### G4 — 22 of 171 (12.9%) are under 10 KB

Median corpus size is 34 KB, so these sit well under it. **On size alone they look
like stubs.** Contents were not audited, so this is a size observation, not a
finding about what they hold — 10 KB is enough for a small script or a single
configuration file. The claim this supports is only that a corpus described in
software terms should not count 22 of 171 among its substance without someone
opening them.

### G5 — 99 of 171 (57.9%) have no primary language that GitHub detected

| Primary language | Count |
|---|---:|
| none detected | 99 |
| Python | 62 |
| HTML | 9 |
| TypeScript | 1 |

The 62 is checkable against that table and against the account's public repository
list.

**A null language field is not evidence that a repository holds only
documentation.** GitHub assigns no primary language to code it cannot classify
either. What the number does support is narrower and still consequential: this
corpus cannot be described as a software tool chain. A reader who arrives
expecting a tool chain and finds 57.9% with no detected language will conclude,
wrongly or rightly, that it is not one.

### G6 — 92.4% of the corpus's volume is one repository

| Repository | Size |
|---|---:|
| `fhir` | 800,748 KB |
| everything else (170 repositories) | 65,828 KB |
| **total** | **866,576 KB** |

`fhir` alone is 92.4% of total bytes, against a median of 34 KB — a factor of
roughly 23,000 above the median.

**What `fhir` contains was not inspected.** This document does not say it is build
output, data or source, because the size field cannot distinguish those and the
contents were not audited. Two consequences follow from the size alone: nobody can
clone that repository casually, and anyone quoting "total corpus size" is quoting
`fhir`. Whether it should be in the corpus is a separate question that requires
opening it.

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

**Supported.** 123 of 171 carry a licence GitHub recognises; the other 48 do not.
116 are not archived. 62 have Python as primary language. One repository — the
verifier — was actually run from a clean environment with no credentials and no
network, and 27 assertions passed (Measurement B). 49 carry no recorded external
use, which is 28.7%, not two thirds.

**Not supported.** Any statement that the corpus is a tool chain. Any statement
that its size represents capability. Any statement that it has been security
reviewed. Any statement about the wider open-source ecosystem, because the wider
ecosystem was not surveyed. Any statement that a repository has never been run by
anyone, because metadata cannot show that.

---

## 4. What would close each gap

| Gap | Closeable by |
|---|---|
| G1 licence ambiguity | Adding a licence file to the 11 unlicensed repositories; replacing the 37 custom licences with SPDX-recognisable text, or stating in each README that the custom terms are intentional |
| G2 archived material | Either un-archiving what is still maintained, or stating the operative count (116) wherever the corpus is described |
| G3 no recorded external use | Per-repository outsider runs, reported individually; this is work, not a statement |
| G4 stubs by size | Opening them and either labelling them stubs or merging them |
| G5 no language | Already accurate; the corpus should stop being described in software terms |
| G6 volume concentration | Inspecting `fhir` and stating what it holds; if it is build output, removing it from history or stating that clones are large |
| G7 duplicate names | Deciding one authoritative copy per name and archiving or renaming the others with a pointer |

None of these is done as of 2026-11-17. They are listed so that a reviewer can
check them, not to suggest they have been addressed.

**The gap this document does not close** is the one the C5 row originally named:
analysis of the open-source AI tool chain. It would need a second measurement over
repositories that are not ours, and it has not been made.

---

## 5. Reproducing this

The figures come from a single API pass over the four accounts' repository
metadata, saved as JSON and re-counted with a script, not read off the GitHub web
interface. Anyone repeating it on a later date will get different totals: archive
state, licence recognition and star counts all move. The date of measurement is
part of the result, which is why it appears at the top of this page.

Measurement B is reproducible in one command from a copy of
`conformance-surface-2026-11`: `python verify_all.py`. It needs Python 3 only — no
credentials, no network, no installed packages.
