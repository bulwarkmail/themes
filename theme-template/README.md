# Theme Template

Starter template for creating a Bulwark Mail theme.

## Usage

1. Copy this folder and rename it to your theme name
2. Update `manifest.json`:
   - Change `id` to a unique lowercase identifier (e.g. `my-awesome-theme`)
   - Change `name`, `author`, `description`
   - Set `variants` to `["light"]`, `["dark"]`, or `["light", "dark"]`
3. Edit `theme.css` and replace all color values with your palette
4. Optionally add a `preview.png` (max 512×512) and reference it in `manifest.json`
5. ZIP the contents and upload via Admin → Themes

## CSS Variables Reference

| Variable                         | Purpose                               |
| -------------------------------- | ------------------------------------- |
| `--color-border`                 | Default border color                  |
| `--color-input`                  | Input field borders                   |
| `--color-ring`                   | Focus ring / outline                  |
| `--color-background`             | Page background                       |
| `--color-foreground`             | Default text color                    |
| `--color-primary`                | Primary buttons, links, active states |
| `--color-primary-foreground`     | Text on primary backgrounds           |
| `--color-secondary`              | Secondary surfaces (buttons, tags)    |
| `--color-secondary-foreground`   | Text on secondary surfaces            |
| `--color-muted`                  | Muted/disabled backgrounds            |
| `--color-muted-foreground`       | Muted text, placeholders              |
| `--color-accent`                 | Hover highlights, selected items      |
| `--color-accent-foreground`      | Text on accent backgrounds            |
| `--color-destructive`            | Error, danger, delete actions         |
| `--color-destructive-foreground` | Text on destructive backgrounds       |
| `--color-popover`                | Dropdown/modal backgrounds            |
| `--color-popover-foreground`     | Text in dropdowns/modals              |

## Tips

- Ensure 4.5:1 contrast ratio between foreground and background colors (WCAG AA)
- Test with both system light and dark modes
- The `--color-ring` should be visible on both `--color-background` and `--color-muted`
