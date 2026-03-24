# Bulwark Mail Themes

Custom themes for [Bulwark Mail](https://github.com/nicholasgriffintn/jmap-webmail).

## Quick Start

1. Copy `theme-template/` and rename it
2. Edit `manifest.json` with your theme info
3. Edit `theme.css` with your colors
4. ZIP the folder contents (`manifest.json` and `theme.css` must be at the root of the ZIP)
5. Upload via **Admin → Themes** in Bulwark Mail

## Theme Structure

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

| Field | Required | Description |
|-------|----------|-------------|
| `id` | Yes | Unique identifier. Lowercase alphanumeric + hyphens, min 2 chars. Must match pattern: `/^[a-z0-9][a-z0-9-]*[a-z0-9]$/` |
| `name` | Yes | Display name shown in settings |
| `version` | Yes | Semantic version (e.g. `1.0.0`) |
| `author` | Yes | Author name |
| `description` | Yes | Short description |
| `type` | Yes | Must be `"theme"` |
| `variants` | Yes | Array of `"light"`, `"dark"`, or both |
| `preview` | No | Relative path to preview image in the ZIP |
| `minAppVersion` | No | Minimum Bulwark Mail version required |

## theme.css

Themes work by overriding CSS custom properties. Define colors for `:root` (light mode) and `.dark` (dark mode).

### All CSS Variables

```css
:root {
  /* Borders & inputs */
  --color-border: #e2e8f0;           /* Default border color */
  --color-input: #e2e8f0;            /* Input field border */
  --color-ring: #3b82f6;             /* Focus ring color */

  /* Base colors */
  --color-background: #ffffff;       /* Page background */
  --color-foreground: #0f172a;       /* Default text color */

  /* Primary - buttons, links, active states */
  --color-primary: #3b82f6;          /* Primary action color */
  --color-primary-foreground: #fff;  /* Text on primary */

  /* Secondary - secondary buttons, tags */
  --color-secondary: #f1f5f9;        /* Secondary surfaces */
  --color-secondary-foreground: #0f172a;

  /* Muted - disabled states, subtle backgrounds */
  --color-muted: #f1f5f9;            /* Muted backgrounds */
  --color-muted-foreground: #64748b; /* Muted text */

  /* Accent - hover states, highlights */
  --color-accent: #3b82f6;           /* Accent color */
  --color-accent-foreground: #fff;   /* Text on accent */

  /* Destructive - delete, error states */
  --color-destructive: #ef4444;      /* Error/danger color */
  --color-destructive-foreground: #fff;

  /* Popover - dropdowns, tooltips, modals */
  --color-popover: #ffffff;          /* Popover background */
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

## Available Themes

| Theme | Variants | Description |
|-------|----------|-------------|
| [Dracula](dracula/) | Light, Dark | Famous vampire-inspired palette |
| [Gruvbox](gruvbox/) | Light, Dark | Retro groove color scheme |
| [Tokyo Night](tokyo-night/) | Light, Dark | Clean dark Tokyo-inspired palette |
| [Rosé Pine](rose-pine/) | Light, Dark | Soho vibes with natural, muted colors |

### Built-in Themes (included with Bulwark Mail)

- **Nord** — Arctic, north-bluish palette
- **Catppuccin** — Soothing pastel (Latte/Mocha)
- **Solarized** — Precision colors by Ethan Schoonover

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
- The `--color-ring` is used for keyboard focus indicators — keep it visible
- The `--color-muted-foreground` should be readable but clearly less prominent than `--color-foreground`
- Preview images are displayed at small sizes, so use simple designs

## License

All themes in this repository are released under the [MIT License](LICENSE).
