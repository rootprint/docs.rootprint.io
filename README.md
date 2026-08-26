# Rootprint docs site

The [Mintlify](https://mintlify.com) documentation site for Rootprint, served at
[docs.rootprint.io](https://docs.rootprint.io).

## Local development

Install the Mintlify CLI:

```bash
npm i -g mint
```

Run the docs site from the repository root:

```bash
mint dev
```

Preview the site at `http://localhost:3000`.

## Before opening a pull request

```bash
mint broken-links --check-anchors --check-redirects
mint validate
```

Also run `mint dev` and check the changed pages locally.

## Writing guidelines

- Use active voice and address the reader as "you"
- Sentence case for headings
- Lead with the task or outcome, then explain context
- Keep setup steps concrete and copy-pasteable
- Update screenshots, examples, and navigation when behavior changes

## Resources

- Site config (navigation, theme, redirects): `docs.json`
- Contribution guide: [`CONTRIBUTING.md`](CONTRIBUTING.md)
- Repository conventions and terminology: [`AGENTS.md`](AGENTS.md)
- Rootprint itself: https://github.com/rootprint/rootprint
- Mintlify docs: https://mintlify.com/docs
