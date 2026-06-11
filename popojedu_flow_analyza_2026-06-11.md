# Hloubková analýza flow a CTA — dev.popojedu.cz (11. 6. 2026)

Metodika: programový průchod obrazovku po obrazovce (desktop ~1500 px i mobil 390 px), na každé obrazovce automaticky spočítány viditelné zelené (primární) CTA. Stav po Martinových průběžných úpravách z 10.–11. 6. (nová navigace bez „Konfigurátoru", +Kontakt/Blog, kontaktní formulář ve funnelu, kontextová mobilní lišta).

## 1. Diagnóza — proč web působí chaoticky

### 1a. Tři zelené CTA na jedné obrazovce (potvrzeno měřením)

| Stránka / obrazovka | Viditelné zelené CTA současně |
|---|---|
| /kalkulator — obr. 2 a 3 | **3**: header „Spočítat cenu" + karta „Rezervovat vůz" + formulář „Rezervovat vůz" |
| / (homepage) — obr. builderu | **3**: header „Spočítat cenu" + „Rezervovat vůz" (karta) + „Rezervovat vůz" (formulář) |
| /vuz/* — obr. 1 | 2: header „Spočítat cenu" + „Spočítat přesnou cenu" |
| /vozy, /cenik — poslední obr. | 2: header „Spočítat cenu" + „Spustit konfigurátor" |

Uživatel u spočítané ceny vidí tři stejně silná tlačítka se dvěma různými texty — neví, které je „to pravé", a header ho navíc láká začít znovu.

### 1b. Šest názvů pro jednu akci

Vstup do téhož kalkulátoru se jmenuje: „Spočítat cenu", „Spočítat cenu →", „Spočítat přesnou cenu →", „Spočítat cenu pronájmu" (mobilní lišta), „Spustit konfigurátor →", dříve „Sestavit nabídku". K tomu dokončení „Rezervovat vůz" 2× na obrazovce. Šest slov pro jeden krok = roztříštěná komunikace.

### 1c. Dva plné funnely vedle sebe

Homepage obsahuje **kompletní** konfigurátor včetně kontaktního formuláře — a totéž běží na /kalkulator-pronajmu-auta (jiné pořadí kroků). Dva celé procesy = dvojí údržba, dvojí měření konverzí, a uživatel přicházející z homepage builderu do kalkulátoru (přes header) začíná od nuly.

### 1d. Ztráta kontextu mezi stránkami

Z detailu vozu vede „Spočítat přesnou cenu" na kalkulátor **bez předvybraného vozu** — uživatel si vůz vybral a musí ho v kroku 1 hledat znovu. Stejně tak ceník nepředává režim (standard/kurýr).

## 2. Co je naopak správně (zachovat)

- Koncept funnelu „cena → nezávazná poptávka v jednom procesu" už na /kalkulator existuje (kroky + kontakt + „Odesláním se k ničemu nezavazujete") — přesně to, co chceme. Problém není koncept, ale duplicity okolo.
- Sticky price card s průběžnou cenou vpravo — dobrý pattern.
- Mobilní lišta už je kontextová (na kalkulátoru „Rezervovat vůz" → #cfg-form) — správný směr.
- Nová navigace (bez Konfigurátoru, s Kontaktem a Blogem) — hotovo dle zadání.

## 3. Optimální řešení — jeden proces, jedna primární akce, jeden slovník

### 3a. Jeden funnel
**/kalkulator-pronajmu-auta = jediný plný proces** (kroky: vůz/účel → doba → najetí → extras → kontakt). Homepage builder zkrátit na **teaser o 2 krocích** (účel + doba → orientační cena) s CTA „Pokračovat k přesné ceně →", které předá vyplněné hodnoty do funnelu (query parametry). Homepage tak neobsahuje formulář ani „Rezervovat vůz".

### 3b. Pravidlo jedné primární CTA na obrazovce
- **Header na běžných stránkách:** jediné zelené tlačítko „Spočítat cenu".
- **Header na /kalkulator:** zelené tlačítko skrýt (uživatel už ve funnelu je) — místo něj telefon jako textový odkaz.
- **Ve funnelu:** primární je karta „Rezervovat vůz" (anchor na formulář). Jakmile je formulář ve viewportu (IntersectionObserver), tlačítko karty se ztlumí na outline „↓ Dokončete níže" a jedinou zelenou zůstane **submit formuláře**. Nikdy dvě zelené najednou.
- **Mobil:** sticky lišta = jediná primární; v hero skrytá; ve funnelu „Rezervovat vůz" → formulář; skrýt, když je formulář na obrazovce.

### 3c. Jeden slovník (závazně)
- Vstup do funnelu: vždy **„Spočítat cenu"** — header, hero, vozy, ceník, detail vozu, mobilní lišta. Zrušit „Spustit konfigurátor", „Spočítat přesnou cenu", „Spočítat cenu pronájmu", „Sestavit nabídku".
- Dokončení: vždy **„Rezervovat vůz"** — existuje jen uvnitř funnelu a viditelná max 1×.
- Mikrocopy pod dokončením: „Nezávazně — potvrdíme dostupnost a ozveme se."

### 3d. Předávání kontextu (jeden souvislý proces napříč webem)
- /vuz/{slug} → „Spočítat cenu" s `?vuz={slug}` → funnel startuje krokem 2 s vybraným vozem
- /cenik (karta kurýři) → `?rezim=kuryr`
- homepage teaser → `?ucel=…&doba=…`
- Po odeslání: děkovací stav se shrnutím (vůz, termín, cena) + co bude následovat

### 3e. Výsledné journeys
1. **Chci cenu:** kdekoliv „Spočítat cenu" → funnel → 1 formulář → hotovo (3 kliky + vyplnění).
2. **Chci si prohlédnout auta:** Vozy → detail (fotky, parametry) → „Spočítat cenu" s předvybraným vozem → funnel krok 2.
3. **Zajímá mě ceník:** Ceník → „Spočítat cenu" s režimem → funnel.
Všechny cesty ústí do **téhož jednoho formuláře** — žádná větev nekončí slepě ani duplicitně.

## 4. Dopad na rozdělanou práci

Tento návrh upřesňuje body 2, 3, 5 a 6 z tasku 869dnb36p (CTA hierarchie + jeden konfigurátor): homepage funnel se nedubluje, ale zkracuje na teaser; pravidlo jedné zelené se rozšiřuje i na header (skrýt ve funnelu) a na vztah karta × formulář. Slovník (3c) je nové závazné pravidlo.
