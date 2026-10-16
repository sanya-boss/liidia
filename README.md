# Liidia

Сайт гостевого дома **Liidia Puhkemaja** на реке Раннапунгерья (Ида-Вирумаа, Эстония). Языки: ET (по умолчанию), RU, EN (`?lang=et|ru|en`).

## Структура

- `site/` — статический сайт, который деплоится на GitHub Pages
  - `index.html` — лендинг
  - `house-rules.html` — правила проживания
  - `404.html` — страница 404
  - `assets/` — фото, логотипы, паттерны; `assets/slots/` — фото, выбранные клиентом
  - `support.js`, `image-slot.js` — рантайм дизайн-компонентов; `vendor/` — React 18.3.1 (локально, без CDN)
- `docs/HANDOFF.md` — дизайн-хендофф: токены, поведение, открытые вопросы перед запуском
- `docs/source/` — исходный бриф и оригинальный паттерн

## Локальный запуск

```sh
cd site && python3 -m http.server 8000
# http://localhost:8000
```

## Деплой

Workflow `.github/workflows/pages.yml` публикует папку `site/` на GitHub Pages при каждом пуше в `main`.
Один раз нужно включить Pages: **Settings → Pages → Build and deployment → Source: GitHub Actions**.

## Перед запуском (из хендоффа)

Реальные фото бани/кухни/санузлов, точная метка на карте, вычитка ET/EN носителем, продакшн-домен для hreflang/OG.
По хендоффу продакшн-версию рекомендуется со временем пересобрать на Astro/Next.js с роутами `/et`, `/ru`, `/en`.
