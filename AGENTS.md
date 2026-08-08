# apps/docs — Agent Guide

## About

User-facing documentation served at docs.rootprint.io. Built with [Mintlify](https://mintlify.com): pages are MDX files with YAML frontmatter, navigation and theming are configured in `docs.json`.

For repo-wide rules (Bun, Prettier, no tests), see the root `AGENTS.md`. For Mintlify component/configuration/writing-standards reference, use the `mintlify` skill.

## Run / Build

```bash
mint dev                                            # local preview
mint broken-links --check-anchors --check-redirects # link check — run before merging content changes
mint validate                                       # strict-mode build validation
```

`mint` parses every `.md` file under the repo root, not just docs content — move scratch or process-artifact directories aside before a run, or the check aborts on a parse error before reaching any real page.

(Mintlify's `mint` CLI is run directly, not through Bun — this workspace doesn't have a `package.json`.)

## Source Layout

| Path | Purpose |
| --- | --- |
| `index.mdx` | Site landing |
| `quickstart.mdx` | Top-level quickstart linked from the root README |
| `indexes.mdx` | Indexes overview |
| `install/` | Install guides (Docker Compose, scaling, etc.) |
| `configuration/` | Env vars, index config, auth, admin operations |
| `send-logs/` | Language SDKs (`languages/`), log agents (`log-agents/`), web servers (`web-servers/`), platforms (`platforms/`), and protocol guides (HTTP, OTLP) |
| `traces/` | Trace overview, sending spans over OTLP, and reading a trace |
| `search/` | Query language reference |
| `api/` | HTTP API reference |
| `tutorials/` | End-to-end recipes (e.g. Linux auth audit with Vector) |
| `files/` | Downloadable assets — notably `docker-compose.yml` referenced from the root `README.md` curl line |
| `images/`, `favicon.ico` | Static assets |
| `docs.json` | Mintlify config: navigation, theme, redirects |

## Terminology

Use these terms consistently across pages:

- **index** — a Quickwit index. Not "dataset" or "collection".
- **view** — a saved search/filter combination. Not "preset" or "filter set".
- **ingest API key** — the bearer credential for log and span ingestion, created in **Settings → API keys**. It uses the `rp_` prefix and is scoped to one index. That index applies to log ingestion only; spans always go to the span store.
- **span store** — the single Quickwit index holding OTLP spans, named by `TRACE_INDEX_ID`. Not "trace index" in user-facing copy.
- **trace ID field** — the per-index setting naming the path to a trace ID inside a log document. Not "correlation field".
- **query API key** — umbrella term for read-only `rpk_` credentials that grant `logs: read` on log query endpoints. Use the specific term when the owner matters.
- **personal API key** / **personal access token (PAT)** — a query API key created by a signed-in user from **Settings → Profile**. It authenticates as that user.
- **service account** — a non-human account created by an admin from **Settings → Service accounts**. Service account API keys are query API keys for shared integrations.
- **log level** — severity (INFO/WARN/ERROR/DEBUG/UNKNOWN). Not "severity" or "log priority".
- **OTLP** — OpenTelemetry Protocol. Capitalize.
- **NDJSON gateway** — the per-line JSON ingest endpoint. Don't abbreviate to "JSON gateway".

## Style

- Sentence case for headings ("Send logs over HTTP", not "Send Logs Over HTTP").
- Active voice, second person ("Run `mint dev`...", not "The user runs...").
- One idea per sentence. Prefer concise sentences over compound ones.
- Bold for UI elements: "Click **Settings** → **Tokens**".
- Code formatting for file names, commands, paths, env vars, and code references.

## Content Boundaries

- Public-facing operator and integrator docs only.
- Do **not** document internal-only admin debugging endpoints or `apps/api/proto/` internals.
- Marketing copy belongs in `apps/landing`, not here.

## Cross-File Dependencies

- The root `README.md` Quick Start curl line links to `files/docker-compose.yml`. If you rename or move that file, update the README in the same PR.
- The standalone Docker Compose file (`files/docker-compose.standalone.yml`) is referenced from install docs; keep it in sync with the main `docker-compose.yml`.

## Authoring Help

Invoke the `mintlify` skill for:

- MDX component reference (Cards, CodeGroup, Tabs, etc.)
- `docs.json` configuration (navigation, themes, redirects)
- Writing standards and tone guidance

## Tests

No automated tests. Pre-merge checks:

```bash
mint broken-links --check-anchors --check-redirects
mint validate
```
