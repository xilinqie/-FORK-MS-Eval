# Historical Oracle sources

This directory preserves the exact inputs associated with the published golden
labels when a current execution guide is corrected. The files under `4c1bbd3/`
are byte-identical to their versions at MS-Eval commit
`4c1bbd3dc0d736623bba563e56cfd8666f85daac`; they deliberately retain the original
defects for reproducibility and are **not** the corrected guides.

See the [26-task errata](../oracle166/ERRATA-2026-11-09.md) and its
[source manifest](2026-11-09.json), followed by the
[four-task prompt errata](../oracle166/ERRATA-2026-11-09-TASK-PROMPTS.md) and
[prompt manifest](2026-11-09-task-prompts.json). The `4c1bbd3/` archive covers
29 distinct published contexts. The `5a0753a/` directory additionally preserves
the finance-workshop guide after the first plan fix and before the prompt cleanup.
The current guides remain in
[`data/oracle166/`](../oracle166/README.md).

Published golden records point at these snapshots where necessary. Their source
hashes and original LLM cache keys remain unchanged. Unchanged tasks need no copy.
The offline label exporter follows these pinned per-record sources by default;
using a revised guide as a new labeling context requires a separate review, not
silently reusing the old cache or changing its claimed provenance.
