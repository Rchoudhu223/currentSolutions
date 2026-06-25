# AGENTS.md

## Cursor Cloud specific instructions

This is a **documentation-only repository**. It contains Markdown notes (a "tech stack canvas") and no application code:

- `README.md` — index/landing page.
- `moulton-niguel-water-district-tech-stack-canvas.md` — the canvas: Markdown tables plus a single Mermaid `flowchart` diagram.

Because there is no application, there are **no dependencies to install, and no build, test, or lint commands**. The update script is intentionally a no-op.

### Viewing / "running" the content

The product is the rendered Markdown. To verify changes, view it in any Markdown renderer that supports Mermaid:

- The simplest path is GitHub's web UI, which renders both Markdown tables and Mermaid diagrams.
- To preview locally with the Mermaid diagram rendered, use a viewer that runs Mermaid (e.g. a small `marked` + `mermaid` HTML page served over a local HTTP server). Non-obvious gotchas when building such a preview:
  - With `marked` v16+, the custom `code` renderer receives a **token object** (`token.lang`, `token.text`), not the legacy `(code, infostring)` arguments. Detect Mermaid fences via `token.lang === "mermaid"` and emit `<pre class="mermaid">…</pre>`, otherwise the block renders as plain text.
  - Load Mermaid as an ES module (`mermaid.esm.min.mjs`) and call `await mermaid.run({ querySelector: ".mermaid" })` explicitly; relying on `startOnLoad` can race with inline module scripts.
