# Contribute to the Rootprint documentation

This repository is the [Mintlify](https://mintlify.com) site served at
[docs.rootprint.io](https://docs.rootprint.io). Pages are MDX files with YAML frontmatter;
navigation and theming live in `docs.json`.

## How to contribute

### Option 1: Edit directly on GitHub

1. Navigate to the page you want to edit.
2. Click the pencil icon to edit the file.
3. Make your changes and open a pull request.

### Option 2: Local development

1. Fork and clone this repository.
2. Install the Mintlify CLI: `npm i -g mint`
3. Create a branch for your changes.
4. Run `mint dev` from the repository root and preview at `http://localhost:3000`.
5. Commit your changes and open a pull request.

## Before opening a pull request

Run both checks from the repository root:

```bash
mint broken-links --check-anchors --check-redirects
mint validate
```

`mint` parses every `.md` file under the repository root, not just documentation pages. Move
scratch or process-artifact directories aside before a run, or the check aborts on a parse error
before reaching any real page.

There are no automated tests.

## Writing guidelines

- **Use active voice**: "Run the command", not "The command should be run".
- **Address the reader directly**: use "you", not "the user".
- **Sentence case for headings**: "Send logs over HTTP", not "Send Logs Over HTTP".
- **Keep sentences concise**: one idea per sentence.
- **Lead with the goal**: start instructions with what the reader wants to accomplish.
- **Use consistent terminology**: see the Terminology section of `AGENTS.md` for the agreed terms
  (index, view, ingest API key, span store, query API key, and others). Don't alternate between
  synonyms.
- **Include examples**: show, don't just tell.
- **Bold for UI elements**: "Click **Settings** → **API keys**".
- **Code formatting** for file names, commands, paths, environment variables, and code references.

Update screenshots, examples, and navigation when behavior changes.
