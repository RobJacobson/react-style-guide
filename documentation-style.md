# Markdown and project documentation style

Use the [technical-writing skill](https://github.com/riekelt/technical-writer/blob/main/plugins/technical-writer/skills/technical-writing/SKILL.md) for substantive technical prose. This guide covers Markdown source layout and the required project directory tree; project documents may require their own metadata and structure.

## Markdown source layout

- Write each prose paragraph on one physical line, with a blank line between paragraphs. Let the editor soft-wrap long lines instead of inserting manual line breaks.
- Keep each list item's prose on one physical line. Preserve structural line breaks for separate items, nested lists, table rows, link definitions, fenced blocks, and diagrams.
- Leave a blank line between headings and their content and around lists and fenced blocks. Do not force prose breaks with trailing spaces, backslashes, or HTML `<br>` tags.
- Use language-tagged code fences. Format code inside them with the project's code conventions.
- Use relative links between files in the same repository and descriptive link text. Check that local links resolve.
- Configure Markdown formatters to preserve single-line paragraphs and list items.

## Project directory tree

- Include a fenced `text` tree of the main directories. Add a brief comment describing the purpose of each listed directory. Include only representative files that help readers find an important entry point or understand a boundary.
- By default, place the tree in the project's root `README.md`, immediately after the title. A project's `AGENTS.md` may name another location or file, such as `FILES.md`, so a public-facing README can open with an introduction.
- Count the repository root as depth 0 and show branches through depth 3 by default. A project's `AGENTS.md` may specify another depth, for example: `Show the project directory tree through depth 4 (root = 0).` Extend an individual branch when another level is needed to explain an important entry point or boundary.
- Update the tree when the documented structure changes. Keep it curated rather than listing every file.

```text
project/                 # Repository root (0)
├── src/                 # Application source (1)
│   ├── components/      # Shared UI (2)
│   │   └── Button.tsx   # Representative component (3)
│   └── features/        # Domain modules (2)
└── tests/               # Behavior tests (1)
```
