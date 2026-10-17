# Handoff: Liidia guest house website (landing + house rules + 404)

## Overview
Marketing site for **Liidia**, a guest house on the Rannapungerja river near Lake Peipus (Ida-Virumaa, Estonia). One-page landing whose single goal is a **phone call** (+372 5815 2876) to check dates — no online booking or payments. Plus a separate **House rules** page and a **404** page. Three languages: **ET (default)**, RU, EN. **Estonian naming: always "Liidia Puhkemaja" / "puhkemaja" (never "külalistemaja").**

## About the design files
Files in `site/` are **design references built in HTML** (a small in-house "Design Component" runtime: `*.dc.html` + `support.js`). They show the intended look, copy and behaviour — they are **not production code to ship**. Recreate them in the target stack (recommended for a static brochure site: **Astro** or **Next.js static export**, plain CSS/Tailwind, i18n routing `/et`, `/ru`, `/en`). Open `site/Liidia Landing.dc.html` in a browser (via a local static server) to see the reference.

`image-slot.js` + `.image-slots.state.json` are a design-tool image placeholder mechanism. **Do not port them.** Use plain `<img>`/`<picture>` with the files listed under *Assets*. Images the client dropped into slots were extracted to `site/assets/slots/<slot-id>.webp` — these **override** the `src` written in the HTML (see table below).

## Fidelity
**High-fidelity.** Final colours, type, spacing, copy and interactions. Recreate pixel-close.

## Pages

### 1. Landing — `Liidia Landing.dc.html`
Full-width layout (no max container), side padding `clamp(20px,4vw,48px)`. Section rhythm: top padding `clamp(64px,9vw,120px)`.

**Layout rule (important):** on desktop every text column sits in a **right-hand column** of width `clamp(480px,38vw,680px)`, aligned to the right page edge; images/titles fill the remaining left space (`flex:1 1 400px`), gap `clamp(32px,6vw,96px)`. Wraps to one column on narrow screens. Photos have capped heights so they don't balloon on wide monitors.

Sections in order:
1. **Header** (sticky, bg `rgba(246,243,236,.96)`, bottom border `#D4D8CE`, height `clamp(68px,8vw,84px)`): logo `liidia-logo11-green.svg` (h 44–54px) · nav (О доме, Размещение, Баня, Галерея, Контакты — 40px tall pills, hover = bg `rgba(40,75,60,.09)` + colour `#284B3C`, 0.3s, **no underline, no movement**) · language dropdown (flag + code + chevron, 48px tall, menu with ET/RU/EN + flags from flagcdn.com) · phone · CTA "Уточнить даты" **hidden until the hero CTA scrolls out of view**, then expands in (grid-template-columns 0fr→1fr + opacity + translateX(16px→0), 0.6s ease-in-out both ways). Mobile (<960px): logo · language dropdown · green 48px burger; menu drops down animated (grid-rows 0fr→1fr, opacity, translateY), Esc closes.
2. **Hero:** eyebrow (13px, 600, .14em, uppercase, `#9B5139`) · H1 Lora 500 `clamp(42px,6.4vw,86px)`/1.04, second line italic `#284B3C` · right column: lead 18–21px, primary CTA "Уточнить свободные даты" (54px, radius 7, `#284B3C`→hover `#1B3529`), text link "Посмотреть размещение", "Размещение от 55 € за ночь" · full-width photo 16:8 (max-h `clamp(320px,40vw,620px)`, radius 12). Faint pattern band (7% opacity) behind the first heading line; on mobile centred vertically behind the H1.
3. **Facts strip** (dl, 4 cells divided by 1px `#D4D8CE`): На берегу реки · 4 км до пляжа · От 55 € / ночь · До 40 спальных мест.
4. **About:** wide photo 4:3 (max-h `clamp(340px,38vw,560px)`) + right column text + host quote (Lora italic, `#284B3C`) — Жанна Орлова, Хозяйка дома.
5. **Rooms:** heading spans 2/3, intro paragraph starts exactly at the 3rd card's left edge (desktop grid `2fr 1fr`, gap 0). 3 cards in a row (border-top `#222B25`, separators `#D4D8CE`): На двоих 55 € · На троих 70 € · На четверых 85 € per night; outline button "Уточнить даты" (sets an "interest" note in Contacts). Info box (bg `#E8DDCE`): shared showers/toilets; link "Правила проживания →".
6. **Amenities card** (bg `#E6EBE2`, radius 14): 6 items, **3 columns × 2 rows** (2 cols <1024, 1 col <720), Lucide icons in `#284B3C`. Faint pattern band at heading level.
7. **Sauna** (full-bleed bg `#3A2417`, white text, eyebrow `#E3B98F`, dividers `rgba(232,200,170,.3)`): photo left, text right; Баня с купелью 50 €/час (min 2 h), Баня без купели 35 €/час; light button "Уточнить время для бани". Vertical sand pattern band (10% baked alpha) centred on the photo.
8. **Activities:** two cards 16:9 (boat photo; "4 км" typographic card with faint pattern band at top) + 4 text items.
9. **Groups:** huge "40" (Lora, `#9B5139`) + text right, outline CTA.
10. **Gallery:** desktop = autoplaying muted looping YouTube video (`aGRQcjyf5hg`, cover-cropped to the height of the 2 stacked photos on the right) + row of 3 photos. Mobile (<720): video 16:9 full width, then the 3 bottom photos, then the 2 others. Clicking any photo opens a **lightbox** (←/→, swipe, Esc, backdrop click, focus trap, counter "n / N"). Video iframe loads only when the gallery is ~600px from the viewport; YouTube thumbnail is the poster.
11. **FAQ:** 8 accordions; open = grid-rows 0fr→1fr 0.4s + fade/slide of text, "+" rotates 45°.
12. **Contacts card** (bg `#E8DDCE`): monogram, heading, interest note (if a room/sauna/group button was clicked), huge tel link, "Позвонить в Liidia" + "Скопировать номер" (clipboard with success/failure message), WhatsApp + Viber buttons; right: Google Maps embed + address + link to the client's share link. Large pattern band at the bottom fading out upward (mask linear-gradient transparent→#000 75%).
13. Pattern band (full-colour green, h `clamp(110px,11vw,170px)`) then **footer** (`#222B25`): logo without tagline (`liidia-logo-light.svg`) + "Гостевой дом у реки Раннапунгерья" (one line) · links Размещение · Баня · **Правила проживания** (right on desktop, left on mobile, no underline, hover `#E8DDCE`) · bottom row "© YEAR Гостевой дом Liidia" / "Designed by Mežennõi" → https://sanya-boss.github.io/portfolio/.
14. Mobile sticky call bar (slides up after hero CTA leaves view, hides near Contacts).

### 2. House rules — `House Rules.dc.html`
Header (sticky on desktop ≥960px; logo, "← На главную", same flag language dropdown as landing — right-aligned on mobile) · hero (eyebrow, H1, intro, fading pattern band) · desktop: sticky numbered table of contents (left, 300px, active section highlighted via IntersectionObserver) + 11 numbered rule sections (right, max 820px); bold for quiet hours and phone numbers; link to Riigi Teataja (KorS). Help box: "Администрация +372 5815 2876" + "Экстренная помощь 112". Closing thank-you line. Footer: logo · "© YEAR Liidia Puhkemaja" (localised) · "Designed by Mežennõi" link. Full copy in ET/RU/EN is in the file's logic (`RULES` object).

### 3. 404 — `404.dc.html`
Centred: huge "404" (Lora, green), title, text, "На главную" + phone; pattern band at the bottom; ET/RU/EN. For GitHub Pages, ship as `404.html`.

## Interactions & behaviour (summary)
- Scroll reveal: blocks fade + rise 16px (0.5–0.55s, `cubic-bezier(.2,.7,.2,1)`, 70ms stagger), once.
- Pattern bands drift very slowly (one tile per 70s, linear, infinite).
- **All motion disabled under `prefers-reduced-motion`.**
- Language: default **ET**; `?lang=et|ru|en` in URL; choice persisted in `localStorage['liidia-lang']`; `<html lang>`, `<title>`, meta description/OG localised. In production implement as real localised routes with hreflang (absolute URLs once the domain is known).
- Skip link "Skip to content" on focus. Min touch target 44px.

## State (landing)
`lang`, `menu` (mobile menu), `langOpen`, `interest` ({type: room|sauna|group, idx}), `open` (FAQ map), `copyMsg`, `heroOut` / `contactsIn` (IntersectionObserver flags for header CTA + mobile bar), `lb` (lightbox items + index), `vidReady`. No data fetching.

## Design tokens
Colours: bg `#F6F3EC` · ink `#222B25` · green `#284B3C` (hover `#1B3529`, deep `#1F3D30`) · sage `#E6EBE2` / line `#C9D0C3` · sand `#E8DDCE` · line `#D4D8CE` · muted text `#62685E`, `#4B5248`, `#3A4237` · terracotta accent `#9B5139` (dark `#7E4029`) · sauna brown `#3A2417` / `#2A190F`, honey `#E3B98F` · footer `#222B25`.
Type: **Lora** (400/500/600, italic) for display/headings; **Manrope** (400–700) for UI/body. Body 17px/1.6. H2 `clamp(32px,4vw,52px)`/1.1, -0.015em. Eyebrows 13px/600/.14em uppercase.
Radii: 7 buttons · 8 inputs/pills · 10 gallery · 12 photos · 14 cards. Shadow only on dropdown/lightbox (`0 12px 32px rgba(34,43,37,.14)`).
Easing: `cubic-bezier(.2,.7,.2,1)`.

## Assets (`site/assets/`)
- Photos (WebP, from client's drone/photo folder): liidia-hero, liidia-about, liidia-boat, liidia-gal-*.
- **Client-replaced slot images** (`assets/slots/`, use these instead of the HTML src): `liidia-gal-2`, `liidia-gal-4`, `liidia-sauna`, `liidia-gal-1`, `liidia-gal-6`, `liidia-about`, `liidia-gal-5`. liidia-sauna is a placeholder-quality photo — replace with a real one before launch.
- Logos (client SVGs, recoloured): logo11 = "Liidia resting place" (header), logo-light = wordmark without tagline (footer), logo10 = "L" monogram (favicon, contacts).
- Pattern (client brand pattern, recoloured, seamless tile 433×520): `liidia-pattern-green.png`, `-green-soft.png` (12% baked alpha), `-sand.png`, `-sand-v.png` (vertical, 10% alpha). Original: `source/pattern-original.png`.
- Icons: Lucide (lucide-static@0.460.0) via CSS mask; WhatsApp/Viber from Simple Icons; flags from flagcdn.com.
- Original brief: `source/Liidia_Website_Brief.md`.

## Open items before launch
Real sauna/kitchen/bathroom photos · exact map pin (client share link: https://share.google/zL2gMesDWh2t9Z2pa) · native-speaker review of ET/EN copy ("купель" translated as hot tub / kümblustünn) · production domain for hreflang/OG absolute URLs · Telegram handle, social links, reviews (not provided — don't invent).

## Files
- `site/Liidia Landing.dc.html` — landing (template + logic incl. full ET/EN dictionary `DICT` keyed by RU source text, and per-language data `T`)
- `site/House Rules.dc.html` — house rules (ET/RU/EN in `RULES`)
- `site/404.dc.html` — 404
- `site/support.js`, `site/image-slot.js`, `site/.image-slots.state.json` — design-tool runtime (reference only)


## Update — 2026-10-17
- **All client photos are now real files** in `site/assets/photos/<slot-id>.webp` (WebP, ≤1920px, q≈0.82) and referenced via `src` in the HTML. `assets/slots/` is obsolete. Crop offsets the client set (object-position) live in `.image-slots.state.json` (`x`,`y` in %) — apply them as `object-position` when porting.
- **Gallery** now has 4 tabs: Väljas / Sees / Toad / Mets ja kalapüük (RU: Снаружи / Внутри / Комнаты / Лес и рыбалка). Desktop: 5-col grid (4-col <1100px), first item featured 2×2; mobile: 2×2 tab chips + horizontal snap scroller (touch + mouse-drag). Below: "Rohkem fotosid…" + Facebook button.
- **YouTube video** now has native controls (play/pause/seek/fullscreen), autoplay muted.
- **Hero**: minimal layout — H1 left, lead/links right, full-width photo filling the viewport, round CTA "Küsi vabu kuupäevi ↓" straddling the photo's top-right edge.
- **About photo**: annotation pill "Me peidame end siin" + arrow pointing at the houses.
- **Facebook**: https://www.facebook.com/p/Peipsi-resting-place-Liidia-Ltd-100083404779288/ (gallery CTA + footer; also `sameAs` in JSON-LD).
- **SEO/social**: `assets/og-cover.jpg` (1200×630) as og:image, og:type/site_name/locale(+alternates), twitter:card, theme-color, apple-touch-icon (`assets/apple-touch-icon.png`), hero preload. House rules page has its own OG tags. In production: absolute URLs for og:image/hreflang/canonical; render ET meta server-side (currently static meta is RU and localised client-side).
- Tap highlight / iOS callout / double-tap zoom disabled; pattern drift on all pages (45s per tile).
