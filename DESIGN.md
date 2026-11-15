# DESIGN.md — Atul's portfolio

Direction: **clean, minimal**. Type-led, generous white space, flat surfaces. The games, the artwork and the career story supply the colour; the interface stays quiet. Light and dark modes with a toggle. Every font, icon and tool is free.

Three content areas get equal weight: **Games** (shipped titles, role, player counts), **Journey** (3D intern to project manager) and **Art** (ArtStation work), plus **Recognition** (GamingCon Bharat, IGDC Indie 60).

Pages use token names, never raw values. Tokens live in `tokens.css`.

## Color

One primary, one accent, neutrals for everything else. All text pairs below pass WCAG AA (4.5:1); ratios are measured against the page background.

| Token | Light | Dark | Role |
| --- | --- | --- | --- |
| `--bg` | `#FFFFFF` | `#0E0F11` | Page background |
| `--surface` | `#F6F6F4` | `#17181B` | Cards, image placeholders, alternate sections |
| `--border` | `#E4E4E0` | `#2A2C31` | Hairlines and dividers (decorative) |
| `--border-strong` | `#8C8C86` | `#6E727A` | Input and secondary-button outlines (3:1) |
| `--text` | `#141413` (18.4:1) | `#F1F1EF` (17.0:1) | Headings and body |
| `--text-muted` | `#6B6B66` (5.4:1) | `#A0A3AA` (7.6:1) | Meta, captions, nav at rest |
| `--primary` | `#1F4FD8` (6.6:1) | `#8FAEFF` (8.8:1) | Links, focus ring, active nav. Nothing else |
| `--on-primary` | `#FFFFFF` | `#0E0F11` | Text on a primary fill |
| `--accent` | `#B45309` (5.0:1) | `#F2B25C` (10.3:1) | Recognition only: award and event labels |
| `--success` | `#1A7F4B` | `#5BD08F` | Contact form sent |
| `--warning` | `#8A5A00` | `#E3B341` | Form warnings |
| `--error` | `#C0362C` | `#FF8A80` | Form errors |

Rules
- The primary button is **ink**, not blue: `--text` fill with `--bg` label. Blue is reserved for links and focus so it always means "this goes somewhere".
- Accent appears at most once per screen.
- No gradients, no tinted section backgrounds beyond `--surface`.
- Dark mode follows the system setting first, then the toggle; the choice is saved per visitor. Theme is set with `data-theme="dark"` on `<html>`.

## Typography

| Family | Use | Source |
| --- | --- | --- |
| **Hanken Grotesk** (400, 500, 600) | Headings and body | Google Fonts, free |
| **JetBrains Mono** (400) | Meta lines only: role, engine, platform, dates, player counts | Google Fonts, free |

| Token | Size / line height | Weight | Use |
| --- | --- | --- | --- |
| `--text-display` | 56 / 60 (36 / 40 on mobile) | 600, tracking -0.02em | Home hero only |
| `--text-h1` | 40 / 46 (30 / 36 on mobile) | 600, tracking -0.015em | Page titles |
| `--text-h2` | 28 / 34 | 600 | Section titles |
| `--text-h3` | 22 / 28 | 500 | Card titles, timeline roles |
| `--text-lead` | 18 / 28 | 400 | Intro paragraphs |
| `--text-body` | 16 / 26 | 400 | Body |
| `--text-small` | 14 / 20 | 400 | Captions, footer |
| `--text-meta` | 13 / 20 mono, tracking 0.02em | 400 | Meta lines |

- Prose measure: 68 characters maximum.
- Headings are left-aligned and sentence case. No all-caps, no gradient text.

## Spacing

4-based scale, used everywhere: `4, 8, 12, 16, 24, 32, 48, 64, 96, 128`.

| Token | Value | Use |
| --- | --- | --- |
| `--content` | 1120px | Maximum content width |
| `--gutter` | 24px (16px on mobile) | Page side padding |
| `--section` | 96px (64px on mobile) | Vertical gap between sections |
| `--grid-gap` | 24px | Card and gallery grids |

Layout is a 12-column grid, left-aligned. Hero text spans 8 columns; it is not centred.

## Shape and depth

| Token | Value | Use |
| --- | --- | --- |
| `--radius-sm` | 4px | Tags, inputs |
| `--radius-md` | 8px | Cards, images |
| `--radius-pill` | 999px | Buttons, theme toggle |
| `--shadow-overlay` | `0 8px 24px rgb(0 0 0 / 0.12)` | Mobile menu and artwork lightbox only |

Cards are flat: `--surface` fill or a `--border` hairline, never both, never a shadow.

## Components

**Buttons** (height 44px, padding 0 20px, `--radius-pill`, 15px / 500)
- Primary: `--text` fill, `--bg` label. Hover: 88% opacity. One per screen.
- Secondary: transparent, 1px `--border-strong`, `--text` label. Hover: `--surface` fill.
- Quiet: text only, underlined on hover. Use for "View all".
- Focus (all): 2px `--primary` outline, 2px offset. Disabled: 40% opacity, no pointer.

**Links**: `--primary`, underlined with 1px line and 3px offset; hover thickens to 2px. External links (ArtStation, store pages) carry an arrow icon.

**Navigation**: name on the left; Games, Journey, Art, Contact and the theme toggle on the right. 64px tall, `--bg` with a `--border` bottom line once scrolled. Active item is `--text` with a 2px `--primary` underline; others `--text-muted`. Below 720px it collapses to a menu button.

**Game card**: 16:9 key art (`--radius-md`), title in `--text-h3`, one mono meta line (`Project manager · Quest · Unreal`), one headline number (players or downloads) in `--text-h2`, quiet link to the case page. Two columns on desktop, one on mobile. Each card states your role.

**Journey timeline**: single vertical 1px `--border` line on the left; each entry has a mono year range, role in `--text-h3`, two lines of body. The current role gets a `--primary` dot; the rest are `--border-strong`.

**Art gallery**: 4-column grid of square thumbnails (3 on tablet, 2 on mobile), `--grid-gap`, with title and software beneath each. Click opens a lightbox that shows the full uncropped image from ArtStation.

**Recognition row**: event name in `--accent`, year in mono, one line of context. Text rows separated by hairlines, not logo tiles.

**Stat**: number in `--text-h1`, label in `--text-small` muted. Maximum four in a row.

**Tag**: mono 13px, `--surface` fill, `--radius-sm`, 4px 8px padding. For engine and platform only.

**Input** (contact form): 44px, 1px `--border-strong`, `--radius-sm`, label above in `--text-small`. Error text in `--error` below the field.

**Footer**: one row with email, ArtStation and LinkedIn links on the left and a copyright line on the right, in `--text-small` muted.

## Extended motion

Added at the owner's request; the site now leans expressive, so add nothing further without removing something.

- **Intro**: the name draws once per browser session (about 1.3s), then the page appears.
- **Hero**: headline words rise from a mask, a pen stroke draws under "3D Artist", a platform word rotates, and the key art drifts slightly on scroll.
- **Lines**: section dividers draw left to right; a wireframe draws beside the 3D art title; the career line and retention curves draw once.
- **Games**: art wipes in from the left, cards tilt toward the mouse, and corner brackets appear on hover (also on art tiles).
- **Other**: a ticker of game names, chart rows slide when re-sorted, skill tags cascade, the page shade shifts on the process and skills sections.
- **Mouse only**: a cursor ring and magnetic buttons. Touch devices skip these and the tilt.
- **Reduced motion**: all of the above is disabled and everything shows in its final state.

## Data graphics

All graphics use real figures from the store dashboards and animate once when they scroll into view.

- **Install split**: donut on `--surface`; Paintball `--primary`, MMA `--accent`, Centipede `--text`. Every segment is also labelled with name, value and share, so colour is never the only cue.
- **Catalogue chart**: horizontal bars in `--text` on a `--border` track, with metric tabs.
- **How I ship a game**: four numbered stages on a line that fills in `--primary`, each with one result from the catalogue.
- **Career line**: a `--primary` line across five roles, spaced by months in each role; height shows the share of production work.
- **Retention curves**: one line per game from install to day 30 on a log scale; the best week-1 game is in `--primary`, the rest in `--border-strong`, all labelled.
- **Journey line**: fills in `--primary` as the reader scrolls the timeline.

Accent appears in graphics as a data colour; in text it is still reserved for recognition.

## Imagery and icons

- **Icons**: Lucide, 1.5px stroke, 20px, `currentColor`. No emoji.
- **Game art**: official key art or gameplay captures at 16:9. No device frames, no overlays.
- **Artwork**: shown uncropped at native aspect ratio. Never tinted or filtered.
- **Portrait**: one photo on the Journey page, square, `--radius-md`.
- **Motion**: 150ms ease-out on hover and focus; 200ms fade for the lightbox. Sections fade and rise 18px once as they scroll into view (700ms, 70ms stagger). Numbers count up once. A 2px `--primary` bar at the top shows scroll progress. With `prefers-reduced-motion`, everything appears in its final state with no animation.
- No stock photos, no decorative illustrations, no background patterns.

## Avoid

Purple-to-blue gradients, glass blur, centred everything, three identical feature cards, shadows on cards, more than one primary button per screen.
