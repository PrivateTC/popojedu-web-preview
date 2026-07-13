# CI → dev: zadání (logo, favicon, og:image, font)

Schválené logo A0 + CI manuál v2.0 (13. 7. 2026, schválil RF). Kompletní balíček včetně binárek (PNG, ICO, og-image, manuál PDF, podpisy, faktura) je na Drive ve složce `POPOJEDU/logo-ci` — soubor `popojedu-ci-balicek.zip` (nasdílí RF). Zde v repu jsou zdrojové SVG.

## Co zakomponovat do dev

1. **Favicon + ikony** — soubory ze složky `web/` balíčku nahrát do rootu webu (dnešní `public/favicon.ico` na dev má 0 B). Head snippet:

```html
<link rel="icon" href="/favicon.ico" sizes="48x48">
<link rel="icon" href="/favicon.svg" type="image/svg+xml">
<link rel="apple-touch-icon" href="/apple-touch-icon-180.png">
```

`favicon.svg` je i zde v repu (`web/favicon.svg`).

2. **og:image** — `og-image-1200x630.png` z balíčku do rootu a do layoutu:

```html
<meta property="og:image" content="https://www.popojedu.cz/og-image-1200x630.png">
```

3. **Webfont Inter** — dnes se nenačítá (jede systémový stack, na každém OS jinak). Přidat do `<head>`:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
```

a v CSS: `font-family:'Inter',-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;`

4. **Logo v hlavičce a patičce** — nahradit CSS značku (`.logo-mark` + text) souborem `logo/popojedu-logo.svg` (výška 32–36 px v navbaru). Inverzní verze pro navy patičku = tentýž SVG se změnou `fill="#0A1F3F"` na `fill="#FFFFFF"` u wordmark path (v balíčku hotová jako `logo/popojedu-logo-inverzni.svg`).

Barvy a typografická škála se nemění — dev už odpovídá design tokenům. Detaily a pravidla v CI manuálu (PDF v balíčku).
