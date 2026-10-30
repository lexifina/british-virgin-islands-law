# How this repository was made (British Virgin Islands)

This file is written by the build on 2026-10-30, the day the source data was retrieved.

## Sources

| Source | Address | Retrieved | Licence |
| --- | --- | --- | --- |
| legislation.gov.uk (The National Archives) | <https://www.legislation.gov.uk/uksi/2007/1678/made> | 2026-10-30 | Open Government Licence v3.0 |
| Wikidata | <https://www.wikidata.org/wiki/Q25305> | 2026-10-30 | CC0 1.0 |

Every word of law in this repository comes from these sources. Lexifina reads them and records each act's dated versions, and the laws that made each change, in one corpus file. This repository is built from that file.

## What is in it

| Act | Title | Versions | Span |
| --- | --- | ---: | --- |
| `constitution` | The Virgin Islands Constitution Order 2007 (SI 2007/1678), as made | 1 | 2007-06-15 to 2007-06-15 |
| `legal-system` | Legal system of British Virgin Islands: open facts from Wikidata | 1 | 2026-10-18 to 2026-10-18 |

The build made 2 commits:

| Commits | Kind |
| ---: | --- |
| 2 | first version of an act |
| 0 | one law on its in-force day |
| 0 | changes no amendment note explains, credited to the publisher |

Other counts:
- 0 commits on the branch `future`: laws not yet in force on 2026-10-30.
- 0 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 1 laws in the record.
- 3 tags.

## Dates

Each commit is dated at noon (America/Tortola) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: An Order in Council comes into force as it provides; SI 2007/1678 s. 1(2): on the day the Legislative Council was next dissolved after the Order was made https://www.legislation.gov.uk/uksi/2007/1678/article/1/made

## How the history is built

`tools/build.py` turns the corpus into this history in one pass: one commit per law, on the day it took effect. The same corpus always gives the same commit hashes. `tools/check_repo.py` reads every version back from git and compares it with the corpus. `tools/on.py` shows the law as it stood on any date. The corpus format is described in `tools/SCHEMA.md`.

- Corpus: sha256 `dd8f04fdb56d425d920a406ca749d14a3a50eafbd3f51a99dfebc5de3fe0e240` (195084 bytes).
- Builder blob hashes (`git hash-object`): `build.py` `a4faa25af85facb64b956b372f6b528aafdd7ec1`, `check.py` `3e59cb6f05eccb94a9ec14431a7f6781221e83ef`, `on.py` `644a6c0857fbcc72562032b58d57aa113fee0641`.
- Python 3.14.0; git version 2.52.0.windows.1.

## Checks

2 versions of 2 acts read back from git on the day each took effect and on the day before: 0 mismatches. Trailers: 0 commits whose trailers git cannot parse. Health: 0 merge commits on main, 0 commit dates that go backwards, 0 commits dated after the build.

No second build of this corpus has been compared yet.

## Decisions made by hand

- The Constitution is dated 15 June 2007, the appointed day under section 1(2) of the Order (the dissolution of the Legislative Council next after 13 June 2007), as the Government of the Virgin Islands (yourconstitution.vg) states.
- Sections 1 to 119 and Schedules 1 and 2 of the Order are one act; part, chapter and cross-headings are not kept as units.
- Footnotes and the explanatory note are left out; curly quotes are written as straight quotes.
- The legal-system act is carried over unchanged from the earlier build of this repository.

## What AI did and did not do

The scripts that read the sources and build this repository were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- A model (Claude) wrote the parser that reads the publisher's XML; no model wrote or edited legal text.
