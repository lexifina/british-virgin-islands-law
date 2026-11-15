# British Virgin Islands: law history in git


The law of the British Virgin Islands as a git history: one file per section, one commit per version on the day it took effect, and the law that made each change as the commit's author. `git blame` names the law behind every line; `git log` lists every change to a section; picking a date gives the text in force that day.

Part of [lexifina/global-law](https://github.com/lexifina/global-law), one git history for every country's law: this is the British Virgin Islands' national law, which global-law reads at `british-virgin-islands/national/acts/`.

**What is in it now:** the Virgin Islands Constitution Order 2007 (SI 2007/1678), as made, with sections 1 to 119 and Schedules 1 and 2, in its one version, in force from 15 June 2007; and a snapshot of facts about the legal system from Wikidata, which is not law. [`constitution/README.md`](constitution/README.md) lists every provision; [`data/laws.csv`](data/laws.csv) lists the law with the days it was made and took effect.

The Order is in `constitution/`, one file per section or schedule: section 1 is the Order's own (citation and commencement), sections 2 to 119 are the Constitution, and `constitution/sec-023.md` is section 23, protection of freedom of expression. `legal-system/` holds the Wikidata facts (courts, legal texts, the state).

The text is in English, as legislation.gov.uk publishes the Order as made.

## Questions as git commands

| Question | Command |
| --- | --- |
| Every change to section 23 of the Constitution | `git log -p --word-diff -- constitution/sec-023.md` |
| Which law wrote each line of section 23? | `git blame constitution/sec-023.md` |
| Every version of the Constitution Order, with the day each took effect | `git log --format="%h %(trailers:key=In-force,valueonly,separator=) %an" -- constitution ':!constitution/README.md'` |
| Section 23 as in force on 1 January 2026 | `python tools/on.py 2026-01-01 constitution sec-023` |

**Outside git**, we also host this record publicly, for free:

- **[Ask Claude about British Virgin Islands law](https://global-law.lexifina.com/v1/try_claude?country=british-virgin-islands)**: opens Claude with a first question ready.
- **[Ask ChatGPT](https://global-law.lexifina.com/v1/try_chatgpt?country=british-virgin-islands)**: the same question in ChatGPT.
- **[Search British Virgin Islands law on our site](https://lexifina.com/law?country=british-virgin-islands&q=freedom+of+expression)**: a search for "freedom of expression", with each provision's text and its versions, no account needed.
- **[Developer REST API](https://global-law.lexifina.com/v1/search_law?query=freedom+of+expression&jurisdiction=british-virgin-islands)**: the same search as JSON, with no key. See the [documentation here](https://lexifina.com/api/global-law).

Both assistants read the record through the free Global law connector (MCP, `https://global-law.lexifina.com/mcp`); the first time, the chat gives you the link that adds it. Ask in English.

**Host it yourself easily.** All it takes is git and Python, and the tools run on your machine:

```sh
git clone --depth 1 https://github.com/lexifina/global-law && cd global-law
python3 tools/countries.py add british-virgin-islands/national/acts
python3 tools/law.py show 2026-01-01 british-virgin-islands/national/acts/constitution/sec-023.md
```

Opened in Claude Code, Cursor, VS Code or Codex, the clone also starts a local MCP server with the same tools ([MCP.md](https://github.com/lexifina/global-law/blob/main/MCP.md)).

## Dates

Each commit is dated at noon, America/Tortola, on the day the version took effect, and carries it in its `In-force:` trailer:

- for the Order, 15 June 2007: it was made on 13 June 2007, and section 1(2) brings it into force on "the appointed day", the day the Legislative Council was next dissolved, which the Government of the Virgin Islands gives as 15 June 2007. Every section and schedule is dated that day;
- for the Wikidata snapshot, the item's own last change (18 October 2026), as the oldest version available.

The Constitution is credited to the Order (`SI 2007/1678`); the Wikidata snapshot to its publisher, not to a law. The committer is always Lexifina.

## How it is checked

- `tools/check_repo.py` reads every version back from git on the day it took effect and on the day before and compares it with the corpus: 2 versions of 2 acts, 0 mismatches.
- Every commit's trailers parse; there are no merge commits, no commit dates that go backwards and none after the build. The results are in [`REPRODUCE.md`](REPRODUCE.md); no second build has been compared yet.

## What it does not show

- **Amendments since 2007.** This is the Order as made: the amending Orders (for example SI 2015/1767 and SI 2022/627) are not applied, and the text is not consolidated.
- **The territory's own law.** No Act of the House of Assembly, no subsidiary legislation and no case law. The Laws of the Virgin Islands (laws.gov.vg), published by the Attorney General's Chambers, carry a copyright claim, and permission to reproduce them has not been asked for.
- **Headings and notes.** Part, chapter and cross-headings, footnotes and the explanatory note are left out, and curly quotes are written as straight quotes.

## Sources

| Source | Kind | Past versions | Notes |
| --- | --- | --- | --- |
| [legislation.gov.uk](https://www.legislation.gov.uk/uksi/2007/1678/made) (The National Archives) | UK statutory instruments, as made | no | The Virgin Islands Constitution Order 2007 (SI 2007/1678), read from the publisher's XML |
| [Wikidata](https://www.wikidata.org/wiki/Q25305) | Facts about the legal system | the item's history; one snapshot here | Courts, legal texts and the state; not law |

## Licence

See [`LICENSE`](LICENSE). The Order is Crown copyright, reused from legislation.gov.uk under the Open Government Licence v3.0; the Wikidata facts are CC0 1.0, and Lexifina's own contributions (the history, commit messages, tables and tools) are CC0 1.0.

No AI model wrote, translated or changed legal text; the scripts were written by an AI model (see [`REPRODUCE.md`](REPRODUCE.md)).

## More

From [lexifina/global-law](https://github.com/lexifina/global-law):

- [FEATURES.md](https://github.com/lexifina/global-law/blob/main/FEATURES.md): every feature, and what every corpus must support (`git blame`, `law.py`, the MCP tools)
- [FAQ.md](https://github.com/lexifina/global-law/blob/main/FAQ.md): questions and answers · [CONTRIBUTING.md](https://github.com/lexifina/global-law/blob/main/CONTRIBUTING.md): proposing changes · [MCP.md](https://github.com/lexifina/global-law/blob/main/MCP.md): the MCP server · [REPRODUCE.md](https://github.com/lexifina/global-law/blob/main/REPRODUCE.md): how it was built · [CHANGELOG.md](https://github.com/lexifina/global-law/blob/main/CHANGELOG.md)
- [FRESHNESS.md](https://github.com/lexifina/global-law/blob/main/FRESHNESS.md): how current each corpus is · [Monitoring](https://github.com/lexifina/global-law/tree/main/monitoring): whether updates are running · [WATCHING.md](https://github.com/lexifina/global-law/blob/main/WATCHING.md): how each official source is watched for changes
- [performance/](https://github.com/lexifina/global-law/tree/main/performance): how fast the tools are, measured
- [visualisations/](https://github.com/lexifina/global-law/tree/main/visualisations): charts and bridges across the world's law
- [Vulnerabilities](https://github.com/lexifina/global-law/tree/main/vulnerabilities): mistakes in legislation as published
