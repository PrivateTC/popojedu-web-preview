# PTC V4 — Private Tours Czech redesign

50+ stránek statického webu v V4 designu. Plně klikatelný preview pro revizi RF + Martina, připraveno k nasazení.

## Stránky

**Main:** index.html · tour-detail.html · tour-builder.html · tour-listing.html · tour-share.html · napady.html · vlastni-tour.html  
**Company:** o-nas.html · reference.html · blog.html · blog-detail.html · kontakt.html  
**Booking:** rezervace.html · thank-you.html · hledat.html  
**Partner:** partnersky-program.html · prihlaseni.html · partner-dashboard.html · newsletter-subscribe.html  
**Legal:** vop.html · gdpr.html · cookies.html · partner-tos.html · zero-tolerance.html · safety.html  
**Utility:** 404.html  
**SEO landing:** kolik-dni-v-praze.html · skryta-mista-prahy.html · praha-s-detmi.html · prohlidka-prahy-2026.html · dan-brown-praha.html · pocasi-v-praze.html  
**Tour variants (19):** tour-prague-full-day · tour-prague-half-day · tour-cesky-krumlov (= tour-detail.html) · tour-karlovy-vary · tour-kutna-hora · tour-karlstejn · tour-bohemian-switzerland · tour-terezin · tour-dresden · tour-vienna · tour-konopiste · tour-pilsner-brewery · tour-moravia-vineyards · tour-krivoklat-krusovice · tour-wedding-photo-tour · tour-family-tour-prague · tour-airport-tour-transfer · tour-krivoklat-skryje · tour-olomouc · tour-tabor-bechyne

## Review toolkit

Každá stránka má:
- **Cmd+B** otevře sidebar navigator (všech 50+ stránek seskupené)
- **💬 Komentovat FAB** vpravo dole — anotace per stránka
- **Status setter** v top baru — ✓ Schváleno / ↻ Iterovat / ! Blokováno
- **Viewport switcher** — Desktop / Tablet / Mobile simulace
- **📋 Export vše** — markdown výpis všech komentářů + statusů
- **🍪 Cookie consent banner** + **↑ Back-to-top** + **☰ Mobile hamburger**

## Deploy na GitHub Pages

Tato branch (`ptc-v4`) je v repo `popojedu-web-preview`. Pro samostatný `ptc-v4-web` repo:
```bash
cd /Users/Macbook12/Můj\ disk\ \(booking@privatetoursczech.cz\)/Private\ Tours\ Czech/Tour\ Marathon\ V4/web
git init
git branch -M main
git add .
git commit -m "Initial PTC V4 web"
git remote add origin https://github.com/PrivateTC/ptc-v4-web.git
git push -u origin main
```

Nebo v existující branch ptc-v4: Pages → Source: deploy from `ptc-v4` → folder `/ptc-v4-web/` → Save.

## Brand identity

Layer abstraktovaná do 5 míst:
- `<a class="td-logo">` v site headeru + footeru
- `Organization` / `TravelAgency` JSON-LD schema
- `<title>` v `<head>`
- Hero kicker v `index.html`

Global swap připraveno pro privatetravel.ai pokud RF schválí dual domain.
