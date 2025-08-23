# Obsidian Web Clipper templates
This is a community collection of templates for the official [Obsidian Web Clipper extension](https://github.com/obsidianmd/obsidian-clipper). We are still under construction.

**Helpful resources**
- What is Obsidian Clipper? [Read about it here](https://obsidian.md/clipper).
- Come chat about Obsidian Web Clipper in the `#obsidian-clipper` channel on the [Obsidian Discord](https://discord.gg/obsidianmd).
- Have an issue with Obsidian Web Clipper? Report it at the [Obsidian Web Clipper GitHub](https://github.com/obsidianmd/obsidian-clipper/issues?q=sort%3Aupdated-desc+is%3Aissue+is%3Aopen).

## Quick start

1) Install the Obsidian Web Clipper extension (Chrome/Firefox/Safari).
2) In the extension, open Templates → “New Template”.
3) Copy JSON from this repo’s `templates/` and paste into your template.
4) Visit a matching site (per the template’s “triggers”), then clip using that template.

Tip: Validate your JSON before saving:

- Windows (PowerShell):

```powershell
Get-Content -Raw .\templates\<file>.json | ConvertFrom-Json > $null
```

## Template catalog (examples)

- `templates/medium-concise-summary-clipper.json`  
  Medium articles → concise summary + key points

- `templates/github-releases-clipper.json`  
  GitHub Releases markdown body

- `templates/youtube-with-transcript-clipper.json`  
  YouTube with transcript extraction

See all templates in `templates/`.

## Template schema (at a glance)

Templates here use this structure:

```json
{
  "schemaVersion": "0.1.0",
  "name": "Example",
  "behavior": "create",
  "noteNameFormat": "{{published|date:\"YYYY-MM-DD\"}} EXAMPLE {{title|safe_name}}",
  "path": "webclips",
  "context": "{{selectorHtml:article|markdown|slice:0,8000|trim}}",
  "properties": [{ "name": "Source", "value": "{{url}}", "type": "text" }],
  "triggers": ["https://example.com", "schema:@Article"],
  "noteContentFormat": "# {{title}}\n\n{{context}}"
}
```

Conventions:

- Use `selectorHtml:article` with sensible fallbacks (e.g., `main, .pw-post-body`) and cleanup filters (remove media tags, collapse >2 newlines, strip code fences).
- Include both hostname regex and `schema:@Article` in `triggers` where possible.
- Keep `noteNameFormat` predictable and `path` organized by source.

## Contributing

We welcome new templates and improvements. Read [CONTRIBUTING.md](./CONTRIBUTING.md).

PR checklist:

- Valid JSON (lint/validate)
- Accurate `triggers`, robust selectors
- Reasonable `noteNameFormat` and `path`
- Tested on 2+ example pages
- Add notes if special behaviors or caveats apply

## Troubleshooting

- Content missing or “insufficient context”?  
  The site DOM may differ. Update `selectorHtml` fallbacks and cleanup filters.
- Site updated and template broke?  
  Open an issue with URL + expected output and we’ll adjust selectors.

## Folder structure

- `templates/` — JSON templates (primary)
- `Template-guides/` — How-to guides for specific sites/templates
- `Clipper-guides/` — General clipper walkthroughs
- `Resources/` — Reference docs (selectors, clipper docs)
- `Images/` — Screenshots for guides

## License

See [LICENSE](./LICENSE).
