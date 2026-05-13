# Design System: Preminuta · Reunión 14 Mayo

## 1. Visual Theme & Atmosphere
A restrained, executive-dark interface with confident asymmetric layouts and fluid CSS motion. The atmosphere is professional and serious — like a dimly lit boardroom with a single warm accent light. Density is balanced (5/10): information-dense grids are offset by generous vertical rhythm and generous negative space. Variance is moderate (6/10): asymmetric hero watermark offsets an otherwise grid-driven document structure. Motion is restrained (5/10): scroll-driven reveals with spring-physics easing, never gratuitous.

## 2. Color Palette & Roles
- **Deep Charcoal** (#0d0d0d) — Primary background surface, near-black warmth
- **Surface Dark** (#111111) — Table headers, elevated surface backgrounds
- **Card Surface** (#161616) — Insight card background, subtle elevation from canvas
- **Hover Surface** (#131313 / #141414) — Interactive hover states for cards and rows
- **Structural Border** (#1e1e1e) — 1px grid lines, section separators, card outlines
- **Burnt Orange Accent** (#ff4f01) — Single accent for labels, numbers, decorative gradients, and interactive feedback. High saturation but grounded — not neon
- **Pure White** (#ffffff) — Primary text, headings, high-emphasis content
- **Muted Stone** (rgba(255,255,255,.5)) — Secondary text, body copy, descriptions
- **Subtle Text** (#666 / #555) — Tertiary text, metadata, footer, timestamps
- **Semantic Red** (#c51a1a / #d52b1e) — Danger/dolor indicators, competitor tags
- **Semantic Green** (#1a7a3a) — Success/solution indicators, vegan/CF badges
- **Semantic Amber** (#c5561a) — Warning/caution indicators, medium-risk tags
- **Semantic Blue** (#75aadb) — Brand A (Otowill) identity color, used sparingly
- **Hero Canvas** (#ff4f01) — Hero section background; full-bleed accent creates dramatic entry
- **Ink on Hero** (#000000) — Hero headline and body text (high contrast on orange)
- **(Banned)** Pure `#000000` is only used on hero for contrast necessity, never on dark canvas. No purple, no neon gradients, no `#0D1117` GitHub imitation

## 3. Typography Rules
- **Display/Numbers:** System font stack (`-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto`) — pragmatic choice for a printed/prepared document. Weight-driven hierarchy (800 for hero, 300 for body)
- **Mono:** `SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace` — for all numerical data, tags, labels, section markers, timestamps
- **Hero Headline:** 72px at max, 32px at min, `clamp(32px,5vw,72px)`. Tight leading (0.94). Negative letter-spacing (-1.5px). Heavy weight (800)
- **Section Headlines:** 48px at max, `clamp(24px,3.5vw,48px)`. Tight leading (0.96). Letter-spacing -1px
- **Section Sub-labels:** 9px uppercase, 2px letter-spacing, mono-adjacent weight (600). Preceded by accent-colored 16px rule
- **Body:** 11-14px, relaxed leading (1.5-1.6), 500-650px max-width for readability
- **Metadata/Tags:** 8-9px, uppercase, 1.5-2px letter-spacing. Used for tags, stat labels, column headers
- **(Banned)** Inter — system stack preferred for document-readiness. Generic serifs banned entirely (this is a business document, not editorial)

## 4. Component Stylings
- **Navigation:** Fixed glass-nav with `rgba(13,13,13,.95)` + `backdrop-filter: blur(16px)`. Bottom border separation. Links are 11px uppercase, muted by default, brighten to white on hover. Underline indicator animates in from left on hover via `::after` pseudo-element (0.35s cubic-bezier)
- **Hero Section:** Full-bleed accent background (#ff4f01). Large watermark mono numeral (14·V) positioned absolutely at right, 6% opacity. Headline and metadata left-aligned. Bottom padding creates generous breathing room
- **Insight Cards (.cloe-insight):** 1px bordered containers with 28px padding. Subtle gradient top border line (`linear-gradient(90deg, transparent, #ff4f01, transparent)`). On hover, 1px accent-toned box-shadow appears (0.4s transition). Color-coded left accent per brand (blue/amber/red)
- **Info Grid Cells (.infoc):** 2-column grid with 1px gap. Each cell has a left accent line that grows from 0 to 100% on hover (0.35s cubic-bezier). Background darkens on hover (#131313)
- **Comparison Grid (.grid2):** 2-column labeled grid with 1px gaps. Header rows colored by brand. Row backgrounds alternate with `display: contents`
- **Dolor Grid (.dolor-grid):** 3-column labeled grid with color-coded headers (red/orange/green). Rows darken on hover (#141414)
- **Scene Cards (.scene):** Dark cards in 3-column grid. Lift 4px on hover with diffused shadow (`0 20px 40px -12px rgba(0,0,0,.5)`). Tag badges with colored borders
- **Agenda Items:** 2-column grid (time + content). Left padding shifts 8px on hover, border-color lightens, title shifts to accent color
- **Question Cards (.q):** 2-column grid. Left padding increases on hover, dot indicator scales up and turns white (0.4s cubic-bezier)
- **Metric Items (.mc):** Centered mono numbers in accent color. Text brightens on hover
- **Table:** Standard bordered table with 12px padding. Rows brighten subtly on hover
- **Footer:** Two-element flex row (logo + copyright). Minimal at 9-11px

## 5. Layout Principles
- **Grid-First:** CSS Grid used for all multi-column layouts (info, cloe, comparison, dolor, scenes, questions)
- **Max-Width Containment:** All content sections constrained to 1000px centered (`margin: 0 auto`)
- **Responsive Breakpoints:**
  - 900px: Dolor grid collapses to single column
  - 768px: All multi-column grids collapse to single column. Section padding reduces from 60px to 40px. Hero padding reduces proportionally
- **1px Grid Gaps:** All grid systems use `gap: 1px` with #1e1e1e background to create structural lines without explicit borders
- **Section Rhythm:** 60px vertical padding per section. Hero is 60vh minimum
- **Print:** Nav hidden, hero collapses, background switches to white

## 6. Motion & Interaction
- **Scroll Reveal:** Sections and child elements fade up 24px on viewport entry via IntersectionObserver (threshold 0.06). `cubic-bezier(.22,1,.36,1)` easing — a custom spring-like curve. 0.7s transition duration
- **Staggered Cascades:** Child elements within sections use delay classes (`reveal-delay-1` through `reveal-delay-5`, each +0.1s) for waterfall reveals
- **Hero Parallax:** Large watermark translates vertically at 0.12x scroll speed, creating subtle depth. `requestAnimationFrame`-throttled for performance
- **Navigation Underline:** Width animates from 0-100% on hover (0.35s cubic-bezier)
- **Card Lifts:** Scene cards lift 4px with shadow expansion on hover (0.4s cubic-bezier)
- **Accent Lines:** Info cells reveal left accent line growing full height on hover (0.35s cubic-bezier)
- **Row Brightening:** All interactive rows/items darken background on hover (0.25-0.3s ease)
- **Question Dots:** Scale 1.5x and shift to white on card hover (0.4s cubic-bezier)
- **Reduced Motion:** `prefers-reduced-motion` media query disables all animations — reveal elements snap to visible, parallax disabled, all transitions zeroed
- **(Performance)** All animations use `transform` and `opacity` exclusively. `will-change: transform` on hero watermark. No `top/left/width/height` animations

## 7. Anti-Patterns (Banned)
- No emojis in UI chrome (emojis appear only in data content as country flags and checkmarks — acceptable for their semantic role)
- No Inter font — system stack is intentional for document portability
- No generic serif fonts — this is a business document, not editorial
- No neon/outer glow shadows — shadows are diffused and dark-tinted
- No purple/blue neon AI aesthetic
- No 3-column equal card layouts (scenes grid is intentionally content-driven, not decorative)
- No generic names — all names and data are real business information
- No fabricated data or fake metrics — every number is verified market intel
- No AI copywriting clichés ("Elevate", "Seamless", "Next-Gen")
- No filler UI text ("Scroll to explore", bouncing chevrons, scroll arrows)
- No `LABEL // YEAR` formatting conventions
- No broken image links or placeholder imagery
- No overlapping elements — watermark is intentionally 6% opacity and non-interactive
- No custom mouse cursors
- No circular spinners or loading animations
