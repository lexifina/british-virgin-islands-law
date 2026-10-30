# British Virgin Islands: law history in git

The law of the British Virgin Islands as a git history: one file per provision, one commit per law on the day it took effect, and the law that made each change as the commit's author. `git blame` names the law behind every paragraph; `git log` lists every change; picking a date gives the text in force that day.

It follows the shared design of [lexifina/global-law](https://github.com/lexifina/global-law).

**What is in it now (a first build, not complete)**

| Folder | Act | Versions | History |
| --- | --- | ---: | --- |
| `constitution/` | The Virgin Islands Constitution Order 2007 (SI 2007/1678), as made: sections 1 to 119 (the Constitution is sections 2 to 119) and Schedules 1 and 2 | 1 | As made, in force 15 June 2007. Later amending Orders are not applied. |
| `legal-system/` | Legal system of the British Virgin Islands: open facts from Wikidata | 1 | A snapshot of Wikidata, dated by the item's last change (18 October 2026) |

**Language.** English, the official language.

**Source.** [legislation.gov.uk](https://www.legislation.gov.uk/uksi/2007/1678/made), The National Archives: *The Virgin Islands Constitution Order 2007* (SI 2007/1678), as made, read from the publisher's XML on 30 October 2026. The Order is Crown copyright, reused under the Open Government Licence v3.0. The legal-system facts are from [Wikidata](https://www.wikidata.org/wiki/Q25305) (CC0). Nothing is taken from the Laws of the Virgin Islands (laws.gov.vg), whose official versions carry a copyright claim.

## Dates

The Order was made on 13 June 2007. Section 1(2) brings it into force on "the appointed day", the day the Legislative Council was next dissolved; that was 15 June 2007, as the Government of the Virgin Islands states. Every section and schedule is dated that day. The legal-system act is a single snapshot dated by the Wikidata item's own last-modified day, as the oldest version available.

## How it is built

Lexifina reads the sources listed here and records each act's dated versions, and the laws that made each change, in one corpus file. `tools/build.py` writes this repository from that file, and the same corpus always gives the same commit hashes; `REPRODUCE.md` gives the details and the checks. A model (Claude) wrote Lexifina's code; it wrote no legal text, and no model runs when the history is built.

## How it is checked

Every version is read back from git on the day it took effect and on the day before (`tools/check_repo.py`) and must match `corpus.json`; results are in `REPRODUCE.md`.

## What "author" means

The author of a commit is the law that made the change, with an e-mail address that cannot exist (`<law key>@lexifina-first-build.invalid`). The Constitution is credited to SI 2007/1678; the legal-system snapshot to its publisher (oldest version available). The committer is always Lexifina.

## Limits

Not complete and not current. This is the Order as made: the amendments made since (for example by SI 2015/1767 and SI 2022/627) are not applied, and the Order is not consolidated. Part, chapter and cross-headings, footnotes and the explanatory note are left out. The territory's own Acts are not included: the Laws of the Virgin Islands are published by the Attorney General's Chambers under a copyright claim, and permission to reproduce them has not been asked for. This repository is not legal advice and not an official publication; for anything that matters, read the original.
