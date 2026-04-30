# Cythera Components

A shadcn-compatible component registry themed with the [Cythera design system](https://herrhelms.github.io/cythera-design-system). Drop-in replacements for shadcn/ui components with neon-dark and pastel-light dual-mode styling, WCAG AA+ contrast, and signature glow effects -- all powered by oklch color tokens.

## Features

- **87 components** -- 59 Radix UI + 28 Base UI variants
- **shadcn CLI compatible** -- add components with `npx shadcn@latest add`
- **Dual theme** -- neon dark / pastel light, automatic via `.dark` class
- **WCAG AA+** -- every text-on-surface pair clears 4.5:1 contrast in both modes
- **oklch color space** -- perceptually uniform tokens for consistent vibrancy
- **Tailwind v4** -- zero inline styles, `@theme inline` bridge included
- **shadcn v4 patterns** -- `data-slot`, `cn()`, `cva`, `React.ComponentProps`, TypeScript throughout
- **Glow hover effects** -- layered `box-shadow` on primary actions, no `filter: blur`
- **Alpha-channel borders** -- subtle transparency that adapts to any surface

## Quick Start

### 1. Add the registry

Add the Cythera registry to your project's `components.json`:

```json
{
  "registries": {
    "@cythera": {
      "url": "https://raw.githubusercontent.com/herrhelms/cythera-components/main/registry/{name}.json"
    }
  }
}
```

Then pull components via the shadcn CLI:

```bash
npx shadcn@latest add @cythera/button
npx shadcn@latest add @cythera/dialog
npx shadcn@latest add @cythera/card
```

Or add a component directly without configuring the registry first:

```bash
npx shadcn@latest add https://raw.githubusercontent.com/herrhelms/cythera-components/main/registry/button.json
```

### 2. Install the theme

Copy the theme files into your project:

```
theme/
  globals.css    -- CSS variables (light + dark)
  tailwind.css   -- Tailwind v4 @theme inline bridge
```

Import `tailwind.css` as your main stylesheet (it imports `globals.css` internally):

```css
/* app/globals.css or equivalent */
@import "path/to/theme/tailwind.css";
```

### 3. Configure fonts

The theme loads four font families from Google Fonts via the CSS import in `globals.css`. If you prefer self-hosting, replace the `@import url(...)` with local `@font-face` declarations for:

| Token            | Family           | Purpose                     |
| ---------------- | ---------------- | --------------------------- |
| `--font-sans`    | Rajdhani         | UI text, body copy          |
| `--font-display` | Orbitron         | Headings, wordmarks         |
| `--font-mono`    | Geist Mono       | Code blocks, telemetry      |
| `--font-tech`    | Share Tech Mono  | Small-caps technical labels |

### 4. Toggle dark mode

Add or remove the `dark` class on `<html>`:

```html
<html class="dark">
```

All tokens swap automatically -- no additional configuration needed.

## Project Structure

```
cythera-components/
├── registry.json              # Registry index (all items listed)
├── registry/                  # Per-component registry-item JSON files
│   ├── button.json            #   Declares dependencies, files, CSS vars
│   ├── dialog.json
│   └── ...                    #   (59 files — one per component)
├── components/
│   ├── ui/                    # Radix UI component source (default)
│   └── ui-base/               # Base UI component source (alternative)
├── lib/utils.ts               # cn() helper (clsx + tailwind-merge)
├── hooks/use-mobile.ts        # Responsive viewport hook
├── theme/
│   ├── globals.css            # Cythera CSS variables (oklch, light + dark)
│   └── tailwind.css           # Tailwind v4 @theme inline bridge
└── package.json
```

The `registry/` folder contains one JSON manifest per component. These are the files the shadcn CLI fetches when you run `npx shadcn@latest add @cythera/button` -- each declares the component's npm dependencies, registry dependencies (other cythera components it needs), source file paths, and any CSS variables to inject.

## Components

### Layout

| Component | Description |
| --------- | ----------- |
| `aspect-ratio` | Constrain content to a desired aspect ratio |
| `card` | Container with header, content, and footer slots |
| `resizable` | Resizable panel groups with keyboard support |
| `scroll-area` | Custom cross-browser scrollbar styling |
| `separator` | Visual or semantic content divider |
| `sidebar` | Collapsible navigation sidebar |

### Forms

| Component | Description |
| --------- | ----------- |
| `button` | Primary action element with 6 variants and 8 sizes |
| `button-group` | Grouped buttons with shared borders |
| `calendar` | Date field built on react-day-picker |
| `checkbox` | Toggle control for checked/unchecked state |
| `combobox` | Autocomplete input with suggestion list |
| `date-picker` | Date picker with range and presets |
| `field` | Form field wrapper with label, description, error |
| `input` | Text input field |
| `input-group` | Input with prefix/suffix addons or icons |
| `input-otp` | Accessible one-time password input |
| `label` | Accessible label associated with controls |
| `native-select` | Styled native HTML select element |
| `radio-group` | Mutually exclusive radio button set |
| `select` | Dropdown option picker via Radix primitives |
| `slider` | Range value selector |
| `switch` | Binary toggle control |
| `textarea` | Multi-line text input |
| `toggle` | Two-state on/off button |
| `toggle-group` | Set of toggleable buttons |

### Feedback

| Component | Description |
| --------- | ----------- |
| `alert` | Contextual callout with variants |
| `alert-dialog` | Modal requiring user response |
| `empty` | Empty state placeholder with icon and message |
| `progress` | Task completion indicator |
| `skeleton` | Loading placeholder |
| `sonner` | Toast notifications via Sonner |
| `spinner` | Loading spinner with size/color variants |
| `toast` | Temporary notification message |

### Overlays

| Component | Description |
| --------- | ----------- |
| `dialog` | Modal window overlay |
| `drawer` | Slide-out panel built on Vaul |
| `hover-card` | Link preview on hover |
| `popover` | Rich content portal triggered by a button |
| `sheet` | Side panel extending from Dialog |
| `tooltip` | Informational popup on hover/focus |

### Navigation

| Component | Description |
| --------- | ----------- |
| `breadcrumb` | Hierarchical path navigation |
| `command` | Composable command palette via cmdk |
| `context-menu` | Right-click action menu |
| `dropdown-menu` | Button-triggered action menu |
| `menubar` | Persistent desktop-style menu bar |
| `navigation-menu` | Website link collection |
| `pagination` | Page navigation with prev/next |
| `tabs` | Tabbed content panels |

### Data Display

| Component | Description |
| --------- | ----------- |
| `accordion` | Collapsible content sections |
| `avatar` | User image with fallback |
| `badge` | Status or category indicator |
| `chart` | Data visualization via Recharts |
| `data-table` | Datagrid built on TanStack Table |
| `table` | Responsive HTML table |
| `carousel` | Swipeable content slider via Embla |
| `collapsible` | Expandable/collapsible panel |
| `item` | Generic list item with consistent styling |
| `kbd` | Keyboard shortcut display |
| `typography` | Typographic component set |

### Utilities

| Component | Description |
| --------- | ----------- |
| `direction` | LTR/RTL directional context provider |

## Base UI Variants

The `components/ui-base/` directory contains 28 components built on [Base UI](https://base-ui.com/) primitives instead of Radix UI. These provide the same Cythera styling with Base UI's unstyled primitive approach.

Available Base UI components:

`accordion` `alert-dialog` `aspect-ratio` `avatar` `checkbox` `collapsible` `context-menu` `dialog` `direction` `dropdown-menu` `hover-card` `label` `menubar` `navigation-menu` `popover` `progress` `radio-group` `scroll-area` `select` `separator` `sheet` `slider` `switch` `tabs` `toast` `toggle` `toggle-group` `tooltip`

Use Base UI variants when you want a lighter runtime or need deeper control over the underlying primitives.

## Design Tokens

### Semantic Colors

| Token | Light | Dark | Purpose |
| ----- | ----- | ---- | ------- |
| `--primary` | Deep indigo | Cyan | Main actions, links |
| `--secondary` | Purple | Pink | Supporting actions |
| `--accent` | Teal | Lime | Highlights, accents |
| `--destructive` | Red-orange | Warm red | Errors, destructive actions |
| `--success` | Green | Lime-green | Success states |
| `--warning` | Amber | Golden | Warning states |
| `--info` | Deep indigo | Cyan | Informational |
| `--muted` | Pale gray | Dark gray | Subdued elements |

### Signature Colors

| Token | Purpose |
| ----- | ------- |
| `--cythera-cyan` | Primary brand accent |
| `--cythera-lime` | Success and energy |
| `--cythera-orange` | Warmth and attention |
| `--cythera-purple` | Secondary brand accent |

### Shadows

Six shadow levels from `--shadow-xs` through `--shadow-xl`, plus `--shadow-glow` for the signature Cythera glow effect. Light-mode shadows use cyan-tinted oklch values; dark-mode shadows use neutral black.

### Border Radius

Base radius `--radius: 0.625rem` with computed variants:

| Tailwind Class | Value |
| -------------- | ----- |
| `rounded-sm` | `calc(var(--radius) - 4px)` |
| `rounded-md` | `calc(var(--radius) - 2px)` |
| `rounded-lg` | `var(--radius)` |
| `rounded-xl` | `calc(var(--radius) + 4px)` |

## Cythera Signature Styling

### Glow Hover Effects

Primary buttons use layered `box-shadow` on hover for the signature Cythera glow:

```css
hover:shadow-[0_0_0_1px_oklch(var(--primary)/0.6),0_6px_18px_-2px_oklch(var(--primary)/0.5),0_0_28px_oklch(var(--primary)/0.45)]
```

Combined with a subtle `hover:-translate-y-px` lift. No `filter: blur` is used -- all effects are `box-shadow` based and reduced-motion-safe.

### Alpha-Channel Borders

Borders use oklch with alpha transparency rather than solid colors, allowing them to adapt to any surface:

```css
--border: oklch(0.85 0.04 230 / 0.35);  /* light */
--border: oklch(0.7 0.1 200 / 0.18);    /* dark */
```

### Typography Scale

Components use the `font-sans` (Rajdhani) family by default. Use the Tailwind utilities to apply other families:

```html
<h1 class="font-display">Orbitron heading</h1>
<code class="font-mono">Geist Mono code</code>
<span class="font-tech">SHARE TECH LABEL</span>
```

## Utilities

### `cn()` -- Class Name Merger

Located at `lib/utils.ts`. Combines `clsx` and `tailwind-merge` for conditional, conflict-free class composition:

```tsx
import { cn } from "@/lib/utils"

<div className={cn("p-4 bg-card", isActive && "ring-2 ring-primary")} />
```

### `useIsMobile()` -- Responsive Hook

Located at `hooks/use-mobile.ts`. Returns `true` when viewport width is below 768px:

```tsx
import { useIsMobile } from "@/hooks/use-mobile"

const isMobile = useIsMobile()
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Follow existing patterns: `data-slot`, `cn()`, `cva` for variants, `React.ComponentProps` for prop types
4. Never hardcode colors -- use design tokens
5. Ensure WCAG AA (4.5:1) contrast in both light and dark modes
6. Submit a pull request

## Links

- [Design System Showcase](https://herrhelms.github.io/cythera-design-system)
- [Design System Repository](https://github.com/herrhelms/cythera-design-system)
- [Component Registry Repository](https://github.com/herrhelms/cythera-components)

## License

MIT
