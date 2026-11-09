# Markdown source style

Use the [technical-writing skill](https://github.com/riekelt/technical-writer/blob/main/plugins/technical-writer/skills/technical-writing/SKILL.md) for substantive technical prose. This guide covers Markdown source layout only; project documents may require their own metadata and structure.

- Write each prose paragraph on one physical line, with a blank line between paragraphs. Let the editor soft-wrap long lines instead of inserting manual line breaks.
- Keep each list item's prose on one physical line. Preserve structural line breaks for separate items, nested lists, table rows, link definitions, fenced blocks, and diagrams.
- Leave a blank line between headings and their content and around lists and fenced blocks. Do not force prose breaks with trailing spaces, backslashes, or HTML `<br>` tags.
- Use language-tagged code fences. Format code inside them with the project's code conventions.
- Use relative links between files in the same repository and descriptive link text. Check that local links resolve.
- Configure Markdown formatters to preserve single-line paragraphs and list items.
