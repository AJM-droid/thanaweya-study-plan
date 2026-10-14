# Bondly Club — Thanaweya Amma Landing Page: WIRED Editorial Design System

Single static page (`index.html`, inline CSS, no framework, no build step). This document records the
WIRED-inspired visual tokens and how they were adapted for an Arabic RTL audience.

## Color tokens

| Token       | Value     | Usage                                                        |
|-------------|-----------|--------------------------------------------------------------|
| Primary     | `#000000` | Headings, primary text, prices, top announcement bar         |
| Secondary   | `#5F5F5F` | Supporting text, captions, metadata (6.39:1 on white)        |
| Tertiary    | `#0064FF` | Primary CTAs, links, focus rings, step/check accents (4.92:1 with white) |
| Neutral     | `#F2EFE8` | Alternating section bands, wallet-number field background    |
| Surface     | `#FFFFFF` | Page background, cards, QR container                         |
| On-primary  | `#FFFFFF` | Text on blue buttons and black bands                         |

Supporting brand accents (used sparingly so the navy/yellow eBook cover feels coherent):
navy ink and warm yellow appear **only** inside the book-cover and product-mockup images, plus two
functional survivors — WhatsApp green `#1FAA55` (recognizable payment action) and signal red `#C4271B`
(problem-list ✕ markers). No other accent colors. No gradients.

In CSS these map onto the existing variable names (`--teal` is now the blue accent,
`--teal-dark` resolves to Primary, `--teal-light` is a 10% blue tint, `--line` is a fine black
hairline). Dividers are 1px; depth comes from borders, not shadows (all card shadows removed).

## Typography (adapted for Arabic)

Reference tokens (Latin): Display Source Serif 4 6.25rem/900/−0.04em · H1 Source Serif 4 3rem/800 ·
Body Source Serif 4 1.05rem/1.65 · Label JetBrains Mono 0.72rem.

**Adaptation — verified by test, not assumed:** a canvas glyph test rendered the Arabic headline
in Source Serif 4 vs generic serif and produced byte-identical widths (616 = 616), with the webfont
registering zero usable faces — Source Serif 4 has no Arabic glyphs and cannot render this page.
JetBrains Mono has the same limitation. Therefore:

- **Arabic headings + body: Cairo** (already loaded by the project in weights 400–900; rendering
  verified in-browser). Headings stay weight 900 for high-contrast editorial hierarchy; body 400.
- Latin/technical fragments fall back through the existing stacks (system serif/sans/monospace).
- The Latin −0.04em display tracking and mono label spacing are **not** applied to Arabic text
  (Arabic shaping, RTL alignment, and punctuation are preserved; existing `-.3px` heading nudge kept).
- The 6.25rem display size is **not** forced anywhere: the hero uses the existing responsive
  `clamp(27px, 7vw, 40px)` scale, so mobile headings stay in the 27–40px band.

## Spacing, corners, components

- Spacing: 8px small · 16px medium · 32px large (existing section rhythm preserved).
- Corners: buttons, pills, badges, toast → 0 (sharp); cards, boxes, details, inputs, QR frame → 2px.
  The circular WhatsApp float and numbered step/check dots keep their round functional shapes.
- Primary buttons: `#0064FF` background, white text, 12px 20px padding, sharp corners, flat
  (3D press-shadows removed); hover/active via brightness filter, which also respects
  `prefers-reduced-motion` (transitions disabled there).
- Cards: white background, black text, 2px radius, ~24px padding on the offer panel.
- Focus: 3px solid `#0064FF` outline everywhere (visible on white and neutral).
- Images: lifestyle photos use `object-fit: cover` at 4:3; the book cover and mockups use
  `object-fit: contain` so the full product stays visible; explicit dimensions keep layout stable;
  below-the-fold images lazy-load; Arabic alt text throughout.

## Layout notes

- Desktop: RTL two-column hero (copy right, cover left); stacked, CTA-first order on mobile.
- Six-step illustration is preserved unflipped (it contains numerals); the numbered HTML list below
  it carries the authoritative LTR 1→6 order.
- Authentic PDF previews and testimonial screenshots keep captioned pride of place; illustrative
  tool images sit in a smaller subordinate grid.
- Payment: InstaPay QR stays on an uncluttered white frame; recipient `Ahmed Gomaa`, wallet
  `01552268432`, InstaPay URL, and WhatsApp `+20 150 045 5750` links are byte-identical to the
  verified original. Meta Pixel `1783713612490810` and its events are untouched.
