# architecture-to-c4

Generate C4 architecture output as Structurizr DSL from structured architecture Markdown.

## What it does

```text
Architecture Markdown
  -> Markdown structure validation
  -> Architecture Model parsing
  -> Architecture Model validation
  -> Structurizr DSL generation
  -> Structurizr validation
  -> .dsl output
```

The core model and transformation are independent from WordPress and consuming repositories.

## Requirements

- Node.js
- npm
- Docker

Structurizr validation uses the pinned official image `structurizr/structurizr:2026.06.28-noble`.

## Install

```bash
npm ci
```

## Generate

```bash
npm run generate -- <architecture-markdown-path>
npm run generate -- <architecture-markdown-path> <architecture-dsl-path>
```

When the output path is omitted, the tool writes a `.dsl` file beside the input Markdown using the same base name. Markdown, model, and Structurizr validation must all succeed before the requested output is replaced. Temporary validation files are removed when generation finishes.

## Validate existing DSL

```bash
npm run validate -- <architecture-dsl-path>
```

## Test and typecheck

```bash
npm run typecheck
npm test
```

## Architecture Markdown contract

The input document must contain exactly one H1. Its text becomes the Structurizr workspace name.

The machine-readable architecture data is taken from these established headings and tables:

- `3. Context and Scope > External Context`
- `4. Solution Strategy > Process Flow Views`
- `5. Building Block View > Responsibility Inventory`
- `5. Building Block View > Ownership Boundaries`
- `5. Building Block View > Dependencies`
- optional `5. Building Block View > Dependency Views`
- `5. Building Block View > Responsibility Details`
- `6. Runtime View`

Table column names and embedded IDs are validated by the implementation. See `fixtures/example.md` for a minimal representative document.

Generated DSL is an output artifact. Edit the architecture Markdown and regenerate instead of hand-editing generated DSL.

## License

GPL-2.0-or-later. See `LICENSE`.
