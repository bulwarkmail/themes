# Bolt Theme

Makes Bulwark Mail look like the [Thunderbird](https://www.thunderbird.net/)
desktop app, using the palette of its "Bolt" design system. Light + dark
variants. Not affiliated with or endorsed by Mozilla.

This theme demonstrates the **Theme API v2** advanced manifest format. Every
color is declared as a structured token in `manifest.json`, plus a sibling
`theme.css` is shipped as a v1 fallback so the same folder works on hosts that
haven't enabled v2 yet.

## What's mapped from Thunderbird

The color values come straight from Thunderbird's upstream Bolt tokens
(`mail/themes/shared/mail/colors.css`):

| Bulwark Mail token              | Light (Bolt)                         | Dark (Bolt)                           |
| ------------------------------- | ------------------------------------ | ------------------------------------- |
| `--color-primary`               | `#1373d9` (Thunderbird blue)         | `#58c9ff` (lighter for dark surfaces) |
| `--color-background`            | `#feffff` (`surface-base-light`)     | `#1a202c` (`surface-base-dark`)       |
| `--color-foreground`            | `#1a202c` (`text-base-light`)        | `#eeeef0` (`text-base-dark`)          |
| `--color-muted`                 | `#f7f7f7` (`surface-subtle-light`)   | `#262d3b` (`surface-subtle-dark`)     |
| `--color-muted-foreground`      | `#737584` (`text-muted-light`)       | `#7f94ac` (`text-muted-dark`)         |
| `--color-accent`                | `#f0f8ff` (`primary-soft-light`)     | `#262c40` (`primary-soft-dark`)       |
| `--color-border`                | `#d9d9de` (`surface-border-light`)   | `#3d4d67` (`surface-border-dark`)     |
| `--color-destructive`           | `#991b1b` (`critical-default-light`) | `#fca5a5` (`critical-default-dark`)   |
| `--color-success`               | `#1d783b` (`success-default-light`)  | `#55d37e` (`text-success-dark`)       |
| `--color-warning`               | `#facc15` (`warning-default-light`)  | `#fdd847` (`warning-pressed-dark`)    |

Plus structural fields exposed by the advanced API:

- `density: "compact"` — Thunderbird's default uidensity preset
- `radii.md: "3px"` — matches Thunderbird's `--button-border-radius`
- `typography.fontSans: system-ui` — Thunderbird uses the OS font

## What's in `skin.css`

A color swap alone can't make the webmail UI look like Thunderbird,
spacing, density, and component shapes also have to change. The bundled
`skin.css` (a Theme API v2 component-level override) targets the app's
stable component anchors to reshape the chrome:

- **Compact 28 px list rows** — Thunderbird's classic table density
- **No avatars in the message list** — matches Thunderbird's default columns
- **Strong selection color** — solid primary blue, not a tinted background
- **Flat 3 px-radius toolbar buttons** with subtle hover borders
- **Tight folder tree** at 13 px with the active pane indicated by a left bar
- **Squared menu items**, monospace dates, native-style 10 px scrollbars
- **System-font input fields** with crisp 1 px borders + outline focus

If your host is on Theme API v1 only, the `skin.css` is silently ignored and
you still get the Bolt color palette via `theme.css`.

## Installation

```bash
cd bolt
zip -r ../bolt.zip manifest.json theme.css skin.css
```

Or on Windows:

```powershell
cd bolt
Compress-Archive -Path manifest.json, theme.css, skin.css -DestinationPath ..\bolt.zip
```

Upload `bolt.zip` via **Admin → Themes** in Bulwark Mail.

## Attribution

Thunderbird is a registered trademark of the Mozilla Foundation. The Bolt
design tokens reproduced here come from the publicly-available
[Thunderbird Desktop source tree](https://github.com/thunderbird/thunderbird-desktop)
(MPL-2.0). This theme adapts those tokens to the Bulwark Mail variable system
and is distributed under the same AGPL-3.0 licence as the rest of this repo.
