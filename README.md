# Bulwark Mail Themes

Custom themes for [Bulwark Mail](https://github.com/bulwarkmail/webmail).

## Quick start

1. Copy `theme-template/` and rename it
2. Edit `manifest.json` with your theme info
3. Edit `theme.css` with your colors
4. ZIP the folder contents (`manifest.json` and `theme.css` must be at the root of the ZIP)
5. Upload via **Admin → Themes** in Bulwark Mail

## Theme structure

```
my-theme/
├── manifest.json    # Theme metadata (required)
├── theme.css        # CSS custom properties (required)
└── preview.png      # Preview image shown in settings (optional, max 512x512)
```

## manifest.json

```json
{
  "id": "my-theme",
  "name": "My Theme",
  "version": "1.0.0",
  "author": "Your Name",
  "description": "A short description of your theme",
  "type": "theme",
  "variants": ["light", "dark"],
  "preview": "preview.png",
  "minAppVersion": "1.0.0"
}
```

### Fields

| Field           | Required | Description                                                                                                            |
| --------------- | -------- | ---------------------------------------------------------------------------------------------------------------------- |
| `id`            | Yes      | Unique identifier. Lowercase alphanumeric + hyphens, min 2 chars. Must match pattern: `/^[a-z0-9][a-z0-9-]*[a-z0-9]$/` |
| `name`          | Yes      | Display name shown in settings                                                                                         |
| `version`       | Yes      | Semantic version (e.g. `1.0.0`)                                                                                        |
| `author`        | Yes      | Author name                                                                                                            |
| `description`   | Yes      | Short description                                                                                                      |
| `type`          | Yes      | Must be `"theme"`                                                                                                      |
| `variants`      | Yes      | Array of `"light"`, `"dark"`, or both                                                                                  |
| `preview`       | No       | Relative path to preview image in the ZIP                                                                              |
| `minAppVersion` | No       | Minimum Bulwark Mail version required                                                                                  |

## theme.css

Themes work by overriding CSS custom properties. Define colors for `:root` (light mode) and `.dark` (dark mode).

### All CSS variables

```css
:root {
  /* Borders & inputs */
  --color-border: #e2e8f0; /* Default border color */
  --color-input: #e2e8f0; /* Input field border */
  --color-ring: #3b82f6; /* Focus ring color */

  /* Base colors */
  --color-background: #ffffff; /* Page background */
  --color-foreground: #0f172a; /* Default text color */

  /* Primary - buttons, links, active states */
  --color-primary: #3b82f6; /* Primary action color */
  --color-primary-foreground: #fff; /* Text on primary */

  /* Secondary - secondary buttons, tags */
  --color-secondary: #f1f5f9; /* Secondary surfaces */
  --color-secondary-foreground: #0f172a;

  /* Muted - disabled states, subtle backgrounds */
  --color-muted: #f1f5f9; /* Muted backgrounds */
  --color-muted-foreground: #64748b; /* Muted text */

  /* Accent - hover states, highlights */
  --color-accent: #3b82f6; /* Accent color */
  --color-accent-foreground: #fff; /* Text on accent */

  /* Destructive - delete, error states */
  --color-destructive: #ef4444; /* Error/danger color */
  --color-destructive-foreground: #fff;

  /* Popover - dropdowns, tooltips, modals */
  --color-popover: #ffffff; /* Popover background */
  --color-popover-foreground: #0f172a;
}

.dark {
  /* Override all variables for dark mode */
  --color-border: #334155;
  --color-input: #334155;
  --color-ring: #60a5fa;
  --color-background: #0f172a;
  --color-foreground: #f8fafc;
  --color-primary: #60a5fa;
  --color-primary-foreground: #0f172a;
  --color-secondary: #1e293b;
  --color-secondary-foreground: #f8fafc;
  --color-muted: #1e293b;
  --color-muted-foreground: #94a3b8;
  --color-accent: #1e293b;
  --color-accent-foreground: #60a5fa;
  --color-destructive: #f87171;
  --color-destructive-foreground: #0f172a;
  --color-popover: #1e293b;
  --color-popover-foreground: #f8fafc;
}
```

### Rules

- Only `:root`, `.dark`, `@font-face`, `@keyframes`, and `@media` selectors are allowed
- No `@import` statements
- No external URLs (`url(https://...)`)
- No `javascript:` URIs
- No `expression()`, `-moz-binding`, or `behavior:`
- Maximum ZIP size: **1 MB**

## Available themes

| Theme                       | Variants    | Description                                              |
| --------------------------- | ----------- | -------------------------------------------------------- |
| [Dracula](dracula/)         | Light, Dark | Famous vampire-inspired palette                          |
| [Gruvbox](gruvbox/)         | Light, Dark | Retro groove color scheme                                |
| [Tokyo Night](tokyo-night/) | Light, Dark | Clean dark Tokyo-inspired palette                        |
| [Rosé Pine](rose-pine/)     | Light, Dark | Soho vibes with natural, muted colors                    |
| [Bolt](bolt/)               | Light, Dark | Looks like the Thunderbird desktop app (v2)              |

### Built-in themes (included with Bulwark Mail)

- **Nord** — Arctic, north-bluish palette
- **Catppuccin** — Soothing pastel (Latte/Mocha)
- **Solarized** — Precision colors by Ethan Schoonover

## Theme API v2 (advanced manifests)

Themes can also be authored entirely in `manifest.json`, with no `theme.css` at all.
Set `"apiVersion": 2` and declare your colors as a structured `tokens` block;
the host compiles them into safe `:root` / `.dark` CSS at install time.

This is the recommended format for new themes. It's shorter, easier to lint,
and unlocks the optional `derive`, `density`, `radii`, and `typography` fields.

### Minimal example

```json
{
  "id": "minimal",
  "name": "Minimal",
  "version": "1.0.0",
  "author": "Your Name",
  "description": "A theme with one colour, foregrounds derived automatically.",
  "type": "theme",
  "variants": ["light", "dark"],

  "apiVersion": 2,
  "derive": true,
  "tokens": {
    "light": { "primary": "#1373d9", "background": "#ffffff" },
    "dark":  { "primary": "#58c9ff", "background": "#1a202c" }
  }
}
```

With `derive: true`, missing `*-foreground` tokens are filled in automatically
based on the contrast of their background colour, so you only have to declare
the bits you actually care about.

### Full example with structural tokens

```json
{
  "id": "my-theme",
  "name": "My Theme",
  "version": "1.0.0",
  "author": "Your Name",
  "description": "...",
  "type": "theme",
  "variants": ["light", "dark"],

  "apiVersion": 2,
  "derive": true,
  "density": "compact",
  "radii":      { "sm": "2px", "md": "4px", "lg": "8px", "full": "9999px" },
  "typography": { "fontSans": "Inter, system-ui, sans-serif", "baseFontSize": "14px" },

  "tokens": {
    "common": { "ring": "#3b82f6" },
    "light":  { "primary": "#3b82f6", "background": "#ffffff", "muted": "#f1f5f9" },
    "dark":   { "primary": "#60a5fa", "background": "#0f172a", "muted": "#1e293b" }
  }
}
```

### Manifest fields (v2 additions)

| Field         | Type                                  | Effect                                                                                       |
| ------------- | ------------------------------------- | -------------------------------------------------------------------------------------------- |
| `apiVersion`  | `1` \| `2`                            | Opt into the structured pipeline. Defaults to `1`.                                           |
| `tokens`      | `{ common?, light?, dark? }`          | Maps of token name → CSS value. Keys without a prefix are sugared to `--color-<name>`.       |
| `derive`      | `boolean`                             | When `true`, missing standard `*-foreground` tokens are derived from contrast.               |
| `extends`     | `string` (theme id)                   | Inherit a parent theme's compiled CSS (built-in or installed) and override on top.           |
| `density`     | `"compact"` \| `"normal"` \| `"touch"` | Emits `--density-row-height`, `--density-control-height`, `--density-spacing-1..3`.          |
| `radii`       | `{ sm?, md?, lg?, xl?, full? }`        | Emits `--radius-sm`, …, `--radius-full`.                                                     |
| `typography`  | `{ fontSans?, fontMono?, fontDisplay?, baseFontSize? }` | Emits `--font-sans`, `--font-mono`, `--font-display`, `--font-size-base`. |

Token keys with these prefixes are emitted as-is (with `--` prepended): `color-`,
`font-`, `radius-`, `density-`. Anything else gets the `--color-` prefix
automatically. You can also write the full custom-property name (`--my-token`)
to bypass both rules.

### Auto-derived tokens (with `derive: true`)

If you supply the base, the foreground is derived if missing (white for dark
backgrounds, near-black for light ones):

```
primary  →  primary-foreground
secondary →  secondary-foreground
muted    →  muted-foreground
accent   →  accent-foreground
destructive → destructive-foreground
popover  →  popover-foreground
card     →  card-foreground
sidebar  →  sidebar-foreground
success / warning / info  →  *-foreground
background  →  foreground   (page text colour)
```

### Adding `theme.css` on top

You can still ship a `theme.css` alongside an advanced manifest. Its contents
are appended after the compiled output. Use it for things the structured API
doesn't cover: `@font-face` rules, `@keyframes`, `@media (prefers-contrast)`
overrides, etc. The same selector rules apply: only `:root`, `.dark`,
`@font-face`, `@keyframes`, and `@media` blocks are allowed.

### Component-level overrides via `skin.css`

Token swaps only let you change colors. To restyle actual components
(toolbars, list rows, buttons) ship a `skin.css` file alongside the manifest.
Skins are an opt-in v2 feature, loaded only when the manifest sets
`"apiVersion": 2`, and they go into a separate `<style>` tag injected after
the colour block, so they win specificity but get torn down cleanly on
theme switch.

```
my-theme/
├── manifest.json    # apiVersion: 2
├── theme.css        # (or skip it; manifest tokens are enough)
├── skin.css         # NEW: component-level overrides
└── preview.png
```

Stable selectors you can target from a skin:

| Selector                            | What it is                                  |
| ----------------------------------- | ------------------------------------------- |
| `body[data-theme-skin="<id>"]`      | Body when your theme is active              |
| `[data-tour="sidebar"]`             | Folder/mailbox tree pane                    |
| `[data-tour="email-list"]`          | Email list pane                             |
| `[data-tour="email-viewer"]`        | Email viewer pane                           |
| `[data-tour="composer"]`            | New message composer                        |
| `[data-tour="search-input"]`        | Top search field                            |
| `[data-tour="compose-button"]`      | Compose / "Write" button                    |
| `[data-tour="storage-quota"]`       | Quota indicator                             |
| `[data-tour^="nav-"]`               | Navigation rail items (`nav-mail`, etc.)    |
| `[role="navigation"]`               | Navigation rail container                   |
| `[role="toolbar"]`                  | Toolbars (file browser, etc.)               |
| `[role="menu"]`, `[role="menuitem"]`| Context menus and menu items                |

Skin CSS still goes through the script-injection sanitizer:

- No `@import`, `@charset`, or `@namespace`
- No external `url(https://…)` or `url(data:…)`
- No `expression()`, `-moz-binding`, `behavior:`, or `javascript:`
- 256 KB cap on the skin file itself; 2 MB cap on the whole ZIP

But unlike `theme.css`, **any selector is allowed**: you can target real
components, not just `:root`/`.dark`. With great power comes great
responsibility: only ship skins you've tested across light/dark + all the
panes the user can open.

### Hooking into theme application

Plugins with the `app:lifecycle` permission can transform a theme's CSS just
before it's injected, via the `themeHooks.onThemeBeforeApply` transform hook:

```js
api.themeHooks.onThemeBeforeApply.register((css, ctx) => {
  // ctx = { themeId: string | null, variant: 'light' | 'dark' }
  // Return a new CSS string to override, or undefined to pass through.
  if (ctx.themeId === 'bolt' && ctx.variant === 'dark') {
    return css + '\n.dark { --color-primary: #88e0ff; }';
  }
});
```

## Building a ZIP

```bash
cd my-theme/
zip -r ../my-theme.zip manifest.json theme.css preview.png
```

Or on Windows:

```powershell
cd my-theme
Compress-Archive -Path manifest.json, theme.css, preview.png -DestinationPath ..\my-theme.zip
```

> **Important:** Files must be at the root of the ZIP, not nested in a subfolder.

## Tips

- Start from `theme-template/` for a ready-to-go starting point
- Test both light and dark variants
- Use sufficient contrast between foreground/background colors
- The `--color-ring` is used for keyboard focus indicators, so keep it visible
- The `--color-muted-foreground` should be readable but clearly less prominent than `--color-foreground`
- Preview images are displayed at small sizes, so use simple designs

## License

All themes in this repository are released under the [GNU Affero General Public License v3](LICENSE).
