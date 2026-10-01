# Examples

**Status:** Accepted
**Updated:** 2026-09-30
**Owner:** Brian Lapp
**Method:** Saved copy of the claude.ai artifact <https://claude.ai/code/artifact/c4c39458-5da8-4db2-a41f-260e6212cbea>, version of 2026-09-30. Byte-for-byte; not edited.

## `uncard-demo/`

The **working mockup of UNCARD** and the project's line of truth (`../docs/decisions/0005-demo-is-source-of-truth.md`). Open `uncard-demo/index.html` in a browser, or the live copy on the wiki site at `/examples/uncard-demo/`.

- 10 pages in both brand directions (Matinee chosen — `../docs/decisions/0004-brand-direction.md`) plus a brand guide each
- Two playable sample uncards: Riley, 9 and Jamie, 40
- One self-contained HTML file (~1 MB, fonts embedded, no network calls)

The product itself is built in [`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter) (`../docs/decisions/0001-source-of-truth.md`). This mockup is what it should become.

**For agents:** don't read this file whole — it is ~1 MB, mostly embedded fonts. Its content is already extracted into `../docs/product/experience.md`, `../docs/catalogue/samples.md` and `../docs/brand/directions.md`. If the artifact is updated, save the new version here and re-check those docs for drift.
