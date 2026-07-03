# Theme Creator

A polished, self-contained visual theme builder for creating and exporting color themes across multiple formats.

Live app: https://themecreator.netlify.app

## Features

- Visual light and dark theme editor
- Built-in palette presets, including an OpenClaw-inspired default
- Save custom palette presets locally in your browser
- Native color pickers plus manual CSS color inputs
- Collapsible surface color controls
- Sticky live preview with:
  - sidebar/navigation
  - message cards
  - buttons and badges
  - input bar
  - destructive and success states
  - link visibility preview
  - syntax highlighting preview
- Import existing theme JSON by paste or file upload
- Export to multiple formats:
  - App Theme JSON
  - VS Code Theme JSON
  - CSS Variables
  - Design Tokens JSON

## Use Locally

No build step is required.

Open `index.html` or `theme-creator.html` directly in your browser.

```bash
open index.html
```

## Files

- `index.html` — main app entry point
- `theme-creator.html` — standalone copy of the app

## Presets

Palette presets change the full UI color palette for light mode, dark mode, the active editor tab, or both modes. Shiki themes are separate and only affect the syntax-highlighted code preview/export metadata.

Current built-in presets include:

- Default Violet
- OpenClaw Default
- Woodsmoke

Custom presets are saved to `localStorage` in the current browser.
- `AGENT.MD` — project notes for AI-assisted development

## Export Formats

### App Theme JSON

Exports the app-style theme schema with metadata, supported modes, Shiki theme names, light colors, and optional dark colors.

### VS Code Theme JSON

Exports a single-mode VS Code theme based on the currently selected preview mode.

### CSS Variables

Exports `:root` variables for light mode and `[data-theme="dark"]` variables when dark mode is enabled.

### Design Tokens JSON

Exports a portable design-token structure for use in design systems or custom build pipelines.

## Development Notes

Theme Creator is intentionally dependency-free:

- no CDN dependencies
- no package install
- no network requests
- all CSS and JavaScript inline

After editing, you can validate the inline JavaScript with:

```bash
python3 - <<'PY'
from pathlib import Path
s = Path('index.html').read_text()
start = s.index('<script>') + len('<script>')
end = s.index('</script>', start)
Path('/tmp/theme-creator-script.js').write_text(s[start:end])
PY
node --check /tmp/theme-creator-script.js
```

## License

MIT
