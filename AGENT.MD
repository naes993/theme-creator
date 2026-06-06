# Theme Creator — Agent Notes

## Project Overview

Theme Creator is a self-contained, single-file HTML/CSS/JavaScript web app for visually building color themes and exporting them to multiple formats.

The app is intended to be public and app-agnostic. Avoid branding it as being for one specific app.

## Main Files

- `theme-creator.html` — complete standalone web app. All CSS and JavaScript are inline.
- `AGENT.MD` — this project guidance file.

## Core Principles

1. **Single-file app**
   - No external CDN dependencies.
   - No network requests or `fetch()` calls.
   - Must work by opening `theme-creator.html` directly in a browser.

2. **App-agnostic public branding**
   - Use the name **Theme Creator**.
   - Avoid references to any specific host app in the UI.
   - The live preview should look like a generic modern assistant/app interface.

3. **Polished visual editor**
   - Two-column layout: editor on the left, live preview on the right.
   - Preview panel should remain sticky on desktop while scrolling through editor options.
   - Color fields include both native color inputs and text inputs for hex/CSS color values.
   - Surface colors are collapsible.

4. **Accessible theme validation by preview**
   - Preview should include common UI surfaces:
     - sidebar/navigation
     - chat/message cards
     - buttons
     - badges
     - input bar
     - success and destructive states
     - code block / syntax highlighting preview
     - link preview using the accent color
   - Link visibility matters. Accent colors may look fine on buttons but fail as text links.

## Supported Export Formats

Current export targets:

1. **App Theme JSON**
   - Original structured app theme format.
   - Includes metadata, supported modes, Shiki theme names, light palette fields, and optional dark palette.

2. **VS Code Theme JSON**
   - Exports a single-mode VS Code color theme based on the currently selected preview mode.
   - Uses the visual palette for workbench colors and the Shiki preview palette for token colors.

3. **CSS Variables**
   - Exports `:root` variables for light colors.
   - Adds `[data-theme="dark"]` variables when dark mode is supported.

4. **Design Tokens JSON**
   - Portable design-token style JSON.
   - Useful as an interchange/source-of-truth format for future exporters.

## Theme Fields

The app currently edits these color fields for both light and dark modes:

### Core Colors

- `background`
- `foreground`
- `accent`
- `info`
- `success`
- `destructive`

### Surface Colors

- `paper`
- `navigator`
- `input`
- `popover`
- `popoverSolid`

## Metadata Fields

- `name`
- `description`
- `author`
- `license`
- `supportedModes`
- `shikiTheme.light`
- `shikiTheme.dark`

## Shiki Preview Notes

The app does **not** load Shiki. Instead, it contains lightweight local palette approximations for popular Shiki themes so the syntax preview changes visually without external dependencies.

The exported JSON still uses official Shiki theme names.

## Development / Validation Checklist

After editing `theme-creator.html`:

1. Confirm no app-specific branding remains if keeping it public/app-agnostic.
2. Validate inline JavaScript syntax:

   ```bash
   python3 - <<'PY'
   from pathlib import Path
   s = Path('theme-creator.html').read_text()
   start = s.index('<script>') + len('<script>')
   end = s.index('</script>', start)
   Path('/tmp/theme-creator-script.js').write_text(s[start:end])
   PY
   node --check /tmp/theme-creator-script.js
   ```

3. Open `theme-creator.html` directly in a browser.
4. Test:
   - Light and dark editor tabs.
   - Preview light/dark toggle.
   - Native color input and text color input sync.
   - Import JSON paste/upload.
   - All export targets.
   - Sticky preview while scrolling editor.
   - Link contrast in both light and dark palettes.

## Suggested Next Improvements

Potential public-release improvements:

1. **Contrast warnings**
   - Show WCAG contrast scores for foreground/background, accent links, buttons, and badges.
   - Especially important because accent is used for links.

2. **Dedicated link preview / contrast panel**
   - Keep a visible link sample near the color editor.
   - Optionally warn when accent color is too low contrast against background/paper.

3. **Copy-to-clipboard export**
   - Add a button to copy generated output without downloading.

4. **Export preview modal**
   - Let users inspect generated JSON/CSS before downloading.

5. **Additional exporters**
   - Windows Terminal JSON
   - iTerm2 `.itermcolors`
   - Ghostty config
   - Kitty config
   - Alacritty TOML
   - Tailwind config snippet
   - Figma/design-token compatible variants
   - Zed theme JSON
   - Sublime Text color scheme

6. **Theme presets**
   - Include a few built-in starting palettes.
   - Allow random palette generation.

7. **Local autosave**
   - Save draft state to `localStorage`.
   - Add reset/clear draft controls.

8. **Better VS Code export**
   - More complete workbench color coverage.
   - Optional paired light/dark export as two separate files or a small extension scaffold.

## Naming Guidance

Use:

- Theme Creator
- App Theme JSON
- Live Preview
- Theme Studio / Assistant in simulated UI

Avoid:

- Branding the public app around a single specific product.
- Making the generic exporter sound exclusive to one platform.
