# Mobilní UX audit — dev.popojedu.cz (2026-06-10)

Metodika: viewport 390 px (iPhone), automatizované měření všech 14 stránek (horizontal overflow, tap targety < 34 px, texty < 12 px, texty nalepené na okraj, rozbité obrázky) + manuální průchod klíčových flow (homepage, kalkulátor, vozy, detail vozu, FAQ, kontakt, blog, účet).

## Verdikt

Základ je velmi dobrý — responsivní grid funguje, žádný horizontal scroll na podstránkách, velká primární CTA, sticky lišta s telefonem je pro mobil správný pattern. Brání tomu být „top" čtyři plošné vady a jedna obsahová díra (prázdný blog).

---

## P0 — opravit před launchem

### 1. Intro blok podstránek bez bočního paddingu (12 stránek)
H1 + úvodní odstavec jsou nalepené na levý okraj displeje na: /vozy, /kalkulator-pronajmu-auta, /cenik, /caste-dotazy, /kontakt, /blog, /muj-ucet, /pronajem-aut-pro-firmy, /pronajem-vozu-pro-bolt-a-uber-v-praze, /pronajem-vozu-pro-kuryry…, /vyzvednuti-vozu, /predani-vozu.
Homepage a /vuz/* jsou v pořádku → chyba je ve sdíleném page-intro komponentu (chybí px-5/px-6 pod sm breakpointem). Jedna oprava, 12 stránek.

### 2. Blog je prázdný
/blog nemá jediný článek (0 odkazů, test URL vrací 404). Produkce má rankující články — bez migrace obsahu při launchi ztratíme organiku. Souvisí: články pak doplnit i do sitemap.xml.

### 3. Mrtvá CTA (z dřívějšího auditu, na mobilu kritičtější)
„Rezervovat vůz", „Zobrazit všechny vozy", 4× „Zjistit více", „Detail nabídky" → href="#". Na mobilu je to konec cesty bez záchrany (na desktopu si uživatel pomůže nav lištou).

### 4. Sticky lišta — kontextová logika
- Na /kalkulator-pronajmu-auta nabízí „Spočítat cenu pronájmu" → odkaz na tutéž stránku (smyčka).
- V builderu u spočítané ceny konkuruje tlačítku „Rezervovat vůz".
- V hero zdvojuje hero CTA.
Pravidlo: skrýt v hero, skrýt/přepnout na „Rezervovat" v builderu a na kalkulátoru. (Viz HTML návrh, piny 2 a 3.)

## P1 — výrazně zlepší použitelnost

### 5. Footer odkazy = tap target 15 px
Všech ~15 odkazů v patičce má klikatelnou výšku 15 px (doporučení Apple/Google: 44–48 px). Na každé stránce webu. Řešení: `padding-block` na odkazech, ne větší font.

### 6. Hero floating badge přetéká viewport
`hero-floating-2` („Bez skrytých poplatků") na homepage vyčnívá doprava mimo 390px viewport — jediný horizontal overflow na webu.

### 7. Texty pod 12 px
Homepage 45 prvků, /vozy 26, kalkulátor 17, detail vozu 13 (badge, meta řádky, popisky). Na mobilu sjednotit minimum na 12 px.

### 8. Mobilní menu bez Kontaktu a Blogu
Hamburger nabízí jen 6 položek bez Kontaktu (je jen v patičce). Na mobilu je „Kontakt" druhá nejhledanější položka — přidat (+ Blog).

## P2 — nice to have

9. Reveal-on-scroll animace: při rychlém swipe se obsah dokresluje se zpožděním — zvážit kratší animace / menší offset na mobilu.
10. Demo data builderu (2 vs 6 měsíců, „na 2 měsíců"), stale „Volný od: 12. 11. 2025", překlep „kuryře" — obsahové opravy (viz hlavní seznam).
11. Konfigurátor zabírá ~10 000 px scrollu (pinned sekce) — na mobilu zvážit kompaktnější krokování bez pinningu.

## Co funguje dobře (nechat)

- Žádný horizontal scroll na podstránkách, gridy stackují správně
- Sticky CTA lišta + telefon jako ikona — správný mobilní pattern (po doplnění logiky z bodu 4)
- Detail vozu: breadcrumb, foto s disclaimerem, atributové chips — vzorové
- /vozy: nativní selecty pro filtry (na mobilu nejlepší volba)
- Kontaktní formulář kompletní (jméno, tel, e-mail, zpráva, souhlas)
- FAQ akordeon funkční, čitelný

## Vazba na celkový seznam změn

Tento audit doplňuje body Z1–Z12 z popojedu_cta_navrh_vs_dev.html (ClickUp task 869dnb36p).
