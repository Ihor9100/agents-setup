<!-- CODEGRAPH_START -->
## CodeGraph

When you need to understand, locate, or trace code, reach for CodeGraph BEFORE grep/find or manual file reading.

- If a `.codegraph/` directory exists at the repo root, use the existing index:
  - **MCP tool** when available: `codegraph_explore` answers most code questions in one call: relevant symbols' verbatim source plus call paths between them, including dynamic-dispatch hops grep can't follow. Name a file or symbol in the query to read its current line-numbered source. If it's listed but deferred, load it by name via tool search.
  - **Shell fallback**: `codegraph explore "<symbol names or question>"` prints the same output.

- If there is no `.codegraph/` directory at the repo root, create/build the CodeGraph index first, then use CodeGraph for the investigation.

- Fall back to `rg`/manual file reading only when CodeGraph is unavailable, indexing fails, or the task is genuinely too small to justify indexing.

Indexing is allowed as part of the investigation; do not skip CodeGraph solely because `.codegraph/` is missing.
<!-- CODEGRAPH_END -->