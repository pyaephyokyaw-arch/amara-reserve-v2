# Amara Reserve — Design Guide

Bilingual (English / Myanmar) marketplace for Visa, Medical, Wellness, Aesthetics and Leisure experiences in Thailand.

- **Prototype:** `Amara Reserve.dc.html`
- **Base system:** shadcn/ui (new-york-v4), loaded from `_ds/shadcn-ui-design-system-4ab00c99-…/`
- **Brand overrides:** `_theme/theme.css` (load after the design-system stylesheets)

---

## 1. Brand colour

| Token | Value | Use |
|---|---|---|
| `--primary` | **`#BF854C`** (light and dark) | Buttons, links, prices, checkmarks, stars, active tabs, accent lines, step numbers |
| `--primary-foreground` | `oklch(0.25 0.031 63.9)` ≈ `#2C1E11` (light) / `oklch(0.2 0.02 63.9)` (dark) | Text and icons on `#BF854C` |
| `--ring` | `#BF854C` | Focus outline |
| `--selection` | `#BF854C` (light) | Text selection |

White text on `#BF854C` fails contrast (≈2.9:1). Always put dark text on the brand colour.
`#BF854C` as small text on white (≈2.9:1) is below WCAG AA for body sizes. Use it for large text, icons and fills. If AA small text is required, add a darker text-only shade.

## 2. Neutrals (warm, hue 63.9)

Every neutral shares hue 63.9, which gives a slight warm tint.

**Light**
| Token | Value | Hex ≈ |
|---|---|---|
| `--background` / `--card` | `oklch(1 0 0)` | `#FFFFFF` |
| `--foreground` | `oklch(0.25 0.031 63.9)` | `#2C1E11` |
| `--secondary` | `oklch(0.955 0.01 63.9)` | `#F5EFE9` |
| `--muted` | `oklch(0.97 0.002 63.9)` | `#F6F4F3` |
| `--muted-foreground` | `oklch(0.52 0.021 63.9)` | `#72675D` |
| `--accent` (hover fill) | `oklch(0.965 0.003 63.9)` | `#F4F2F1` |
| `--border` / `--input` | `oklch(0.925 0.005 63.9)` | `#E9E5E3` |
| `--surface` | `oklch(0.98 0.002 63.9)` | `#F9F8F7` |

**Dark** (`data-theme="dark"` on `<html>` or `class="dark"` on a subtree)
| Token | Value |
|---|---|
| `--background` | `oklch(0.15 0.01 63.9)` ≈ `#0E0A07` |
| `--card` | `oklch(0.17 0.01 63.9)` |
| `--foreground` | `oklch(0.98 0 0)` |
| `--muted` | `oklch(0.25 0.007 63.9)` |
| `--muted-foreground` | `oklch(0.75 0.015 63.9)` |
| `--border` | `oklch(0.29 0.007 63.9)` |

In a dark page, inverted bands (`class="dark"`) lift to `oklch(0.19 0.01 63.9)` so they stay distinct.

## 3. Semantic colours (not brand)

| Colour | Where | Reason |
|---|---|---|
| Red `#FF4842` / `--destructive` | Wishlist heart, wishlist count, unread dot, errors | Alert and state |
| Green / yellow | Community "Housing" and "Notices" labels | Category coding |
| Black overlays, white text | On photos and video | Readability over imagery |

## 4. Typography

| Role | Font | Notes |
|---|---|---|
| Headings (h1–h6) | **Onest** 600 | Tracking −0.025em on display sizes |
| Body / UI | **Geist** 400–700 | 14px base (`--text-sm`) |
| Myanmar | **Noto Sans Myanmar** 400–700 | Primary face when `data-lang="mm"`; h1 line-height 1.55–1.6 for stacked diacritics |

Loaded from Google Fonts: `Geist`, `Onest`, `Noto Sans Myanmar` (400/500/600/700).

**Scale (desktop → phone ≤640px)**
- Hero display: 64px → reduced hero
- Section H2 / CTA: 40–48px → 28px
- Category page H1: 40px → 28px
- Card title: 16–20px
- Body: 14px; muted descriptions 14px `--muted-foreground`
- Kicker / meta: 11–12px, 600, uppercase tracking 0.08–0.18em
- Form inputs: 16px on phone (prevents iOS zoom)

## 5. Shape and elevation

- `--radius`: 0.75rem (12px) → sm 8 / md 10 / lg 12 / xl 16 / 2xl 24
- Buttons (`data-slot="button"`) and pills: fully rounded (`999px`)
- Cards and image tiles: `--radius-xl`; menus and popovers: `--radius-lg`
- Borders: 1px `--border`
- Shadows: warm-tinted ramp `--shadow-xs` → `--shadow-2xl` (`oklch(0.55 0.015 63.9 / 0.05–0.15)`); cards `sm`, popovers `md`, dialogs and mobile panel `lg`

## 6. Layout and spacing

- Content container: `max-width:1200px; margin:0 auto; padding:0 24px` (16px on phone)
- 4px spacing grid; section top spacing 72–96px (40px on phone)
- Grids use `data-g` markers so breakpoints can reflow them:

| `data-g` | Desktop | ≤1180px | ≤1024px (tablet) | ≤640px (phone) |
|---|---|---|---|---|
| `bento` (home categories) | 4-col bento | 2-col, first tile full width | 2-col | 1-col |
| `4` | 4 | 3 | 2 | 1 |
| `3` | 3 | 3 | 2 | 1 |
| `2` | 2 | 2 | 2 | 1 |
| `side` (content + sidebar) | 2 tracks | 2 tracks | stacked | stacked |
| `foot` | 4 | 4 | 2 | 2 |
| `cats` | 5 | 5 | 3 | 2 |

Breakpoints: **1180px** (small laptop), **1024px** (tablet), **640px** (phone).

## 7. Navigation

**Desktop (>1024px):** Logo · Experiences dropdown · Hub · Help · language · theme · Sign in · Send inquiry.

Experiences menu structure:
- **Visa**
  - Tourist visa
  - Education visa ▾ (dropdown)
    - All Education visa
    - Language school · School · College · University · International school
- **Medical**, **Wellness**, **Aesthetics**, **Leisure** (Nature & Escape, Culture & Craft, Taste of Thailand, Movement & Mastery)

**Tablet (641–1024px):** a hamburger button replaces Experiences, Hub, Help and Sign in. The menu opens as a 420px panel from the right over a 40% black scrim.
**Phone (≤640px):** the hamburger also absorbs language, theme and Send inquiry. The menu opens full-screen.

Mobile menu pattern:
- Categories are 52px accordion rows with a ▾ chevron that rotates 180° (200ms).
- Expanded category: "All [category]", then items as 44px rows.
- Education visa nests one level deeper, with a 2px `#BF854C` guide line.
- Hub, Help and Sign in are full-width rows.
- The bottom bar stays pinned: language switch, theme toggle, full-width Send inquiry.

## 8. Components

Built on shadcn/ui classes (`data-slot` / `data-variant`):
- **Button:** primary `#BF854C` fill with dark text; outline and ghost fill with `--accent` on hover
- **Badge:** breadcrumb chips on category heroes, "In demand" tag (18% `#BF854C` tint, foreground text)
- **Tabs:** category group filters (`role="tab"` buttons); scroll sideways on phone
- **Input group:** hero search (44px)
- **Cards:** experience cards (image 152px + body), top-pick cards, step cards with a cursor spotlight
- **Dialogs:** sign-in, inquiry, hero video (scrim `rgba(0,0,0,0.75)`); max width `100vw − 24px` on phone

Imagery uses `<image-slot>` placeholders, so real photos can be dropped in.

## 9. Motion

- Colour and shadow: 150ms ease
- Popovers and menus: 150–200ms fade + scale 0.95 → 1 (`fxPop`, `fxZoom`)
- Section reveal: 6px rise + fade (`fxRevealIn`)
- Chevrons: 200ms rotate
- No bounce or spring. All non-essential motion is disabled under `prefers-reduced-motion`.

## 10. Accessibility

- "Skip to main content" link (EN/MM), appears on first Tab
- `<main id="main">`, `<header>`, `<nav aria-label>` landmarks; breadcrumbs as `<nav aria-label="Breadcrumb">`
- Focus: 2px `#BF854C` outline, 2px offset, on every interactive element
- Clickable cards: `role="button" tabindex="0"`, and Enter or Space activates them
- `aria-current="page"` on active Hub and Help; `aria-expanded` on menus and dropdowns
- Touch targets ≥44px on tablet and phone
- `<html lang>` switches between `en` and `my`

## 11. SEO

- Default title: "Amara Reserve | Visa, Medical, Wellness & Leisure Experiences in Thailand"
- Per-page title `[H1] | Amara Reserve`; meta description taken from the page intro
- Open Graph and Twitter card tags; `og:locale` switches `en_US` / `my_MM`
- JSON-LD `TravelAgency` (areaServed TH, MM; languages en, my)
- `theme-color` `#BF854C`

## 12. Content and voice

- **Naming:** "Experiences" (not Services), "Wellness" (not Beauty & Refreshment)
- Sentence case for buttons and titles; plain, direct second person
- No emoji, no exclamation marks
- Every UI string has English and Myanmar versions; untranslated keys fall back to English
- Prices in Thai baht (`฿4,500`); `฿0` shows as "On request"

## 13. Open items

- Logo files and approval (`assets/logo-dark.png`, `logo-light.png`); the logo doesn't load on first paint
- Leisure package prices (placeholders)
- Education "School" price (placeholder ฿35,000)
- Native review of Myanmar copy for Leisure packages and the new Education visa sub-menu labels
