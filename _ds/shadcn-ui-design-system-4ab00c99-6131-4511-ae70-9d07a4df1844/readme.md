# shadcn/ui Design System

A complete, dependency-light recreation of **shadcn/ui** (new-york-v4 registry, default neutral theme) as a portable design system: every UI component family, all states and variants, the full token set, and the lucide icon system.

## Sources

- **User-provided repo:** `github.com/kaunghs-fluxion/AdminUI-master` — attached as the design-system input. At build time this repo contained only a README placeholder ("AdminUI — Admin UI shadcn") and no code, tokens, or assets; it identifies shadcn/ui as the intended system but contributes no overrides.
- **Ground truth:** `github.com/shadcn-ui/ui` — `apps/v4/registry/new-york-v4/ui/*.tsx` (component values) and `apps/v4/app/globals.css` (tokens). All numeric values (heights, paddings, radii, shadows, oklch colors) were copied verbatim from that source. Explore these repos further to refine designs based on this system.

If AdminUI-master gains real product code later, re-run the design-system build against it — product-specific screens and any theme overrides should win over stock shadcn defaults.

## What this system is

shadcn/ui is a neutral, monochrome component system: near-black primary on white, one accent-free gray ramp, one red for destruction, and a blue ramp reserved for charts. Personality comes from precision — consistent 36px controls, 14px text, quiet 1px borders and very soft shadows — not from color.

## CONTENT FUNDAMENTALS

- **Tone:** plain, direct, product-neutral. Sentences are short and instructional: "Enter your email below to login to your account." "Make changes to your profile here. Click save when you're done."
- **Casing:** sentence case everywhere — buttons ("Save changes", "Create account"), titles ("Edit profile"), menu items ("Log out"). Proper nouns keep their casing (GitHub, Next.js).
- **Person:** second person ("your account", "your changes"); the product never says "I" or "we" except in legal-ish lines ("You agree to our Terms of Service").
- **Confirmations** are stern and explicit: "Are you absolutely sure?" / "This action cannot be undone."
- **No emoji, no exclamation marks** in UI copy (a single "Success!" style prefix in alerts is the ceiling).
- **Shortcuts** shown as mac glyphs: ⌘K, ⇧⌘P, inside `Kbd` or menu shortcut slots.
- Descriptions live in `muted-foreground` 14px under 14px medium labels.

## VISUAL FOUNDATIONS

- **Color:** all neutrals in oklch with zero chroma. Light: white background, near-black `--primary`, `.97` grays for secondary/muted/accent, `.922` borders. Dark (`.dark` scope): `.145` background, `.205` cards/popovers, white-ish primary, borders as `white/10%` alpha. Destructive is the only saturated UI color (`oklch(.577 .245 27.3)`). Charts use a 5-step blue ramp.
- **Type:** system sans (`ui-sans-serif, system-ui`), no webfont shipped. UI sits at 14px/500 for controls and labels, 14px/400 muted for body, 12px for badges/meta, 18px/600 for dialog titles. Tracking slightly tight (-0.025em) on large headings only.
- **Spacing:** 4px grid. Control heights: 24 (xs), 32 (sm), 36 (default), 40 (lg). Paddings: 12px h-padding on inputs, 16px on default buttons, 24px card padding, 4px menu padding with 6×8px items.
- **Radii:** derived from a single `--radius: 0.625rem` → sm 6 / md 8 / lg 10 / xl 14. Controls use md, cards xl, dialogs/menus lg/md, pills & switches full.
- **Borders:** 1px `--border` everywhere; inputs use `--input` (same value in light). No 2px borders, no colored left-border accents.
- **Shadows:** extremely soft black-alpha ramp — xs on buttons/inputs, sm on cards, md on popovers/menus, lg on dialogs/sheets. Never colored shadows.
- **Backgrounds:** flat solid colors only. No gradients, no textures, no imagery baked into components. Overlay scrim is `black/50%`.
- **Hover states:** solid → `color-mix` 90% of the same color; quiet surfaces (ghost/outline/menu items) fill with `--accent`. Links underline on hover with 4px underline offset.
- **Press/active:** no scale or color change distinct from hover (state changes are instant).
- **Focus:** 3px outer ring of `--ring` at 50% opacity plus ring-colored border; invalid fields swap to `--destructive` at 20%.
- **Motion:** fast and subtle — 150ms ease on color/shadow, 200ms fade+zoom-in (scale .95→1) for popovers/dialogs, 300ms slides for sheets/drawers, 200ms chevron rotations. No bounces, no springs.
- **Transparency/blur:** none in components (alpha only in dark-mode borders and overlays). No glassmorphism.
- **Selection:** inverted — near-black background, white text.
- **Cards:** white surface, 1px border, xl radius, shadow-sm, 24px padding, 24px internal gap.
- **Disabled:** 50% opacity + pointer-events none, universally.

## ICONOGRAPHY

- **System:** [Lucide](https://lucide.dev) — 16×16 rendering (12px in xs contexts), 24×24 viewBox, 2px stroke, round caps/joins, `currentColor`. This is the icon set shadcn/ui uses throughout.
- **Implementation here:** `components/icons/Icon.jsx` embeds lucide path data inline (~45 common glyphs) and renders by name: `<Icon name="chevron-down" />`. Add more glyphs to its `iconPaths` registry by copying path data from lucide.dev. This inline approach was chosen over a CDN icon font so cards and kits work offline; it is the one **intentional addition** beyond the shadcn inventory.
- **Color:** icons inherit text color; muted contexts (menu item icons, select chevrons) use `--muted-foreground` or 50% opacity.
- **No emoji, no unicode-as-icon, no PNG icons.**
- **Logo:** none. Neither source repo ships a brand mark. Render product names in plain 14px/600 type where a logo would sit (e.g. sidebar header). Do not invent a mark.

## Component inventory (all shadcn/ui families)

Namespace: `window.ShadcnUiDesignSystem_4ab00c`. Styling is plain CSS keyed off `data-slot`/`data-variant`/`data-size`/`data-state` attributes (mirroring the source's data attributes), so states are inspectable and even non-React HTML can reuse the classes.

- `components/icons/` — Icon (lucide)
- `components/buttons/` — Button, ButtonGroup (+Text/Separator), Toggle, ToggleGroup(+Item)
- `components/inputs/` — Input, Textarea, Label, InputGroup (+Addon/Button/Text/Input/Textarea), InputOTP (+Group/Slot/Separator), NativeSelect (+Option/OptGroup), Field family (FieldSet/Legend/Group/Field/Content/Label/Title/Description/Separator/Error)
- `components/selection/` — Checkbox, RadioGroup(+Item), Switch, Slider, Select family, Combobox, Calendar
- `components/display/` — Card family, Badge, Avatar (+Image/Fallback/Badge/Group/GroupCount), Separator, Skeleton, AspectRatio, Progress, Kbd(+Group), Spinner, Empty family, Item family
- `components/layout/` — Table family, Accordion family, Collapsible family, Tabs family, ScrollArea, Resizable (PanelGroup/Panel/Handle), Carousel family
- `components/overlays/` — Dialog, AlertDialog, Sheet, Drawer, Popover, HoverCard, Tooltip (each with full sub-part families)
- `components/menus/` — DropdownMenu family (checkbox/radio items, submenus), ContextMenu family, Command family (+CommandDialog)
- `components/navigation/` — Breadcrumb family, Pagination family, NavigationMenu family, Menubar family, Sidebar family (Provider/Sidebar/Trigger/Header/Content/Footer/Group/Menu/…)
- `components/feedback/` — Alert(+Title/Description), Toaster + `toast()` (sonner-style)

Simplifications vs. upstream (visuals faithful, engines simplified): Carousel has no drag physics; Drawer has no drag-to-dismiss; ScrollArea uses native thin scrollbars; Sidebar omits offcanvas/mobile modes; Calendar reimplements react-day-picker's default month grid; positioning is anchor-relative CSS (no collision detection).

## Index

- `styles.css` — global entry; imports everything below
- `tokens/` — colors.css (light+dark), radius.css, typography.css, shadows.css
- `css/` — per-family component CSS (base, buttons, inputs, selection, display, layout, navigation, overlays, menus, feedback, sidebar)
- `components/` — React components (+ `.d.ts` contracts + `.prompt.md` usage notes + one card HTML per directory)
- `guidelines/` — foundation specimen cards (colors, type, radius, shadows, spacing, states)
- `ui_kits/admin/` — admin dashboard UI kit (sidebar shell, stat cards, data table, form dialog)
- `SKILL.md` — agent skill entry point

## Using the system

```html
<link rel="stylesheet" href="styles.css">
<script src="_ds_bundle.js"></script>
<script type="text/babel">
  const { Button, Card, Icon } = window.ShadcnUiDesignSystem_4ab00c;
</script>
```

Dark mode: add `class="dark"` to `<body>` (or any subtree).
