# Design system

Read from `index.html` (the `:root` variables and the CSS under them). The look, in the words of
the CSS's opening comment: the live site's page order, rebuilt as a night rink. Dark only
(`color-scheme: dark`); there is no light theme.

## Colors

Tokens on `:root`. Use these before any literal value.

| Token | Value | Use |
|---|---|---|
| `--bg` | `#05070A` | Page background, `theme-color` |
| `--bg-2` | `#0A0E14` | Alternate bands (offers, blog), card bodies |
| `--panel` | `rgba(170,210,255,.045)` | Glass panels, ghost buttons, tiles |
| `--panel-2` | `rgba(170,210,255,.085)` | Panel hover |
| `--line` | `rgba(190,220,255,.11)` | Hairline borders and dividers |
| `--fg` | `#F1F5FA` | Main text, nav pill background |
| `--soft` | `#B4BECB` | Secondary text, nav links, sub-headings |
| `--muted` | `#8A95A5` | Labels, captions, footer text |
| `--ice` | `#A6E9FF` | Accent, focus outline, gradient text |
| `--ice-2` | `#4CB6FF` | Deeper ice blue, selection, glows |
| `--gold` | `#E2C26A` | Brand gold: eyebrows, calls to action, active dot |
| `--gold-2` | `#B8902F` | Dark end of the gold gradient |
| `--red` | `#FF3D4F` | Rink red: center line, pulse dots, "limited spots" notice |

Literal colors that sit outside the tokens:

| Value | Where |
|---|---|
| `#F6DE93`, `#FFF4D2` | Light ends of the gold button and gold text gradients |
| `#1A1203` | Text on gold buttons |
| `#00111d` | Selected text color |
| `#D6DEE8` | Quote text on player cards |
| `#FF7A86` | The "Confidence" blog keyword |
| `#0d1117`, `#070a0f`, `#0b0b0b`, `#0d4f8a` | Photo placeholder, blog canvas base, puck, dark end of the orb gradient |

Gradients:

- `.grad` text: `#fff` to `--ice` to `--ice-2`, at 100deg.
- `.gold-txt` text: `#FFF4D2` to `--gold` to `--gold-2`, at 100deg.
- `.btn-gold`: `#F6DE93` to `--gold` to `--gold-2`, top to bottom, with a gold glow shadow.

Player card tones (`--tone`, an RGB triple per card): `232,238,246` (silver), `255,92,104` (red),
`92,214,120` (green), `110,150,255` (blue), `255,170,60` (orange); default `166,233,255` (ice).
The tone tints the card, its level badge, the journey end dot and the "Read more" link.

## Typography

| Token | Stack | Use |
|---|---|---|
| `--display` | Inter Tight, then SF Pro Display, system sans | Headings, lede, brand |
| `--body` | Inter, then SF Pro Text, system sans | Body text, buttons |
| `--mono` | JetBrains Mono, then SF Mono, Menlo | Eyebrows, tags, badges, numbers |
| `--cond` | Barlow Condensed (mostly italic), then Arial Narrow | League strip, player names, journey steps, blog keywords, footer tagline |

Fonts load from Google Fonts: Inter Tight 500 to 800, Inter 400 to 600, JetBrains Mono 400 and
500, Barlow Condensed 600 and 700 in roman and italic.

| Style | Size | Weight and spacing |
|---|---|---|
| Body | 16px, line height 1.55 | 400 |
| Hero `h1` | `clamp(44px, 9.2vw, 116px)`; phones `clamp(38px, 11.4vw, 52px)` | 800, letter spacing -.035em, line height 1 |
| Final `h2` | `clamp(44px, 8.4vw, 104px)` | 800 |
| Section `.h2` | `clamp(36px, 6vw, 72px)`; phones `clamp(32px, 9.4vw, 42px)` | 700 |
| Offer `h3` | `clamp(32px, 4.6vw, 56px)` | 700 |
| Lede | `clamp(18px, 2.4vw, 26px)`, uppercase | 600, letter spacing .02em |
| Sub text `.sub` | `clamp(17px, 1.8vw, 20px)`, max 56ch | 400, `--soft` |
| Eyebrow `.mono` | 12px, uppercase | letter spacing .16em |
| Tags and badges | 10.5px mono, uppercase | letter spacing .12em to .16em |
| Buttons | 15px, uppercase; phones 14px | 700, letter spacing .08em (.06em on phones) |

Headings use `text-wrap: balance`.

## Spacing and layout

- One column, `--wrap: 1160px`, side gutters `max(20px, safe-area inset)`.
- Section bands: `padding-block: clamp(80px, 12vw, 150px)`; 72px on phones.
- Card grids: 3 columns with an 18px gap, one column below 960px (resources) and 900px (blog).
- Radii: 999px for pills, buttons and inputs; 34px offer card; 30px player card; 28px tile; 26px
  post; 22px on phones for tiles and posts; 50% for the arrow buttons, small dots, avatars and the
  portrait; 3px for the rail position dots.
- Breakpoints: 640px (phone layout), 760px (nav links hide), 820px (footer one column), 860px
  (offer and coach one column), 900px and 960px (grids one column).
- Safe-area insets are respected at the top bar, the sides and the footer.

## Motion

- Easing: `--ease: cubic-bezier(.2,.7,.1,1)`.
- Sections fade up 26px over 1s when scrolled into view (`.rv` to `.rv.in`).
- Hover lifts: pill -1px, buttons -2px, tiles and posts -4px, player cards -6px; cards do not lift
  on phones.
- Loops: league marquee 32s, coach halo spin 40s, red pulse 2.4s; offer ring fills over 2.4s.
- `prefers-reduced-motion: reduce` turns off all of it.

## Components

| Component | Class | Notes |
|---|---|---|
| Nav bar | `.nav`, `.brand`, `.nav-links`, `.pill` | Sticky, blurred glass, 60px tall (56px on phones) |
| Scroll progress | `.progress` | 2px gold bar at the top of the window |
| Buttons | `.btn` with `.btn-gold`, `.btn-ghost`, `.btn-wide` | Pill shape, 54px tall (52px on phones, full width) |
| Eyebrow | `.mono.eyebrow` | Gold mono label above a heading |
| Hero | `.hero`, `#rink`, `.hero-logo`, `.lede`, `.trust` | Canvas rink behind centered text |
| League strip | `.leagues`, `.lg` | Masked, endless marquee |
| Player card | `.pc`, `.ph`, `.nm`, `.lvl`, `.jr`, `.q`, `.more` | Tone-tinted card on a snap rail (`.rail`), with `.arrows` and `.dots` |
| Offer card | `.offer`, `.ring` | Gold and ice radial glows, SVG ring |
| Tile | `.tile`, `.tag` | Resource card |
| Email form | `.sub-form`, `.letter`, `.note` | Pill input, gold button, `aria-live` note |
| Post card | `.post`, `.art`, `.kw`, `.by` | Canvas art with a big condensed keyword |
| Portrait | `.halo`, `.socials` | Round photo in a spinning SVG ring, social pills |
| Notice | `.limit` | Red-tinted box with a pulsing dot |
| Footer | `.foot`, `.tagline`, `.legal`, `.concept` | Two columns, one on phones |

Styles that exist with no markup using them yet: `.lessons`, `.mmark` (with `.orb`).

## Accessibility

- Focus: `:focus-visible` shows a 2px `--ice` outline with a 3px offset.
- Tap targets are at least 44px tall (pills, social links, legal links, "Read more").
- The hero rink canvas, the offer ring, the coach halo SVG and the final circle carry
  `aria-hidden="true"`. The blog art canvases and the icon SVGs inside buttons and social links do
  not. The arrows have `aria-label`s; form notes are `aria-live="polite"`.
