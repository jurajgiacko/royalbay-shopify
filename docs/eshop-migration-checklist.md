# E-shop Migration to Shopify — Universal Checklist

> Reusable checklist pre migráciu e-shopu na Shopify.
> Vytvorené na základe Royal Bay migrácie (FastCentrik → Shopify, 2026).
> Cieľ: Dodať agentúre kompletné podklady pre setup a spustenie.

---

## Fáza 0: Príprava projektu

### Repo & workflow
- [ ] Vytvoriť Git repo (`{brand}-shopify`)
- [ ] Nastaviť GitHub Pages (public repo) pre zdieľanie HTML deliverables s agentúrou
- [ ] Vytvoriť `TODO.md` pre mobilný task management (GitHub app)
- [ ] Nastaviť PACT ↔ Git workflow (citlivé = PACT, pracovné artefakty = Git)

### Zmluvné & obchodné
- [ ] Zmluva s agentúrou podpísaná
- [ ] Platobná brána vybraná (Comgate / Shopify Payments / iné)
- [ ] Doprava — prepravci a cenníky (Zásilkovna, GLS, PPL...)
- [ ] Osobný odber — áno/nie
- [ ] Fakturačný systém — napojenie (Pohoda, ABRA, iné) + middleware (Make/Zapier)

---

## Fáza 1: Produktový katalóg

### Export z existujúcej platformy
- [ ] Získať XML/CSV export zo starej platformy (FastCentrik, Shoptet, WooCommerce...)
- [ ] Rozparsovať export — extrahovat:
  - [ ] Master produkty (nie varianty)
  - [ ] SKU kódy (reálne, nie odhadované)
  - [ ] Názvy produktov
  - [ ] Ceny (aktuálne + stará cena ak existuje)
  - [ ] Farebné varianty + dostupné veľkosti
  - [ ] Produktové popisy
  - [ ] Obrázky (URL alebo export)

### Produktový plán (28 produktov → X produktov)
Pre každý produkt definovať:
- [ ] **Identifikácia:** SKU, názov, produktová línia, typ
- [ ] **Shopify názov** — optimalizovaný pre e-shop (kratší, s pipe separátorom)
- [ ] **SEO title** — `{Produkt} | {Brand} — {USP}` (max 60 znakov)
- [ ] **LLM description** — popis optimalizovaný pre AI vyhľadávače (GEO)
- [ ] **Cena** — aktuálna + stará (pre zobrazenie zľavy)
- [ ] **Parametre:**
  - [ ] Typ kompresie / hlavný parameter produktu
  - [ ] Trieda / úroveň
  - [ ] Aktivity / použitie
  - [ ] Farby (hex kódy!)
  - [ ] Veľkosti
  - [ ] Materiál
  - [ ] Ďalšie features (custom per brand)

### Rozhodnutia o portfóliu
- [ ] Ktoré produkty NEBUDÚ v novom e-shope? (bundles, discontinued...)
- [ ] Outlet kolekcia — áno/nie? Ktoré produkty?
- [ ] Nové produkty plánované pred launchom?

---

## Fáza 2: Kategórie & navigácia

### Strom kategórií
Definovať 4 typy kolekcií:
- [ ] **Podľa typu produktu** (hlavná navigácia) — podkolenky, návleky, ponožky...
- [ ] **Podľa aktivity** — beh, cyklistika, trail, fitness, cestovanie...
- [ ] **Podľa použitia** — športové, medicínske, každodenné...
- [ ] **Špeciálne** — outlet, novinky, bestsellery, gift cards

### Pre každú kategóriu definovať:
- [ ] Shopify collection handle (URL slug)
- [ ] SEO title + meta description
- [ ] H1 heading
- [ ] Úvodný text (SEO copywriting)
- [ ] INDEX/NOINDEX pravidlo
- [ ] Canonical URL pravidlo

### Menu / navigácia
- [ ] Hlavné menu (mega menu / burger menu / štandard)
- [ ] Breadcrumbs štruktúra
- [ ] Footer navigácia

---

## Fáza 3: Parametrické filtre (Shopify Metafields)

### Filter schema
Pre každý filter definovať:
- [ ] **Shopify metafield namespace + key** (napr. `custom.compression_type`)
- [ ] **Typ** (single_line_text, list.single_line_text, number_integer...)
- [ ] **Hodnoty** — zoznam možností
- [ ] **Zobrazenie** — dropdown / checkboxy / swatche / range slider
- [ ] **Indexovanie** — filtrovné URL = NOINDEX (vždy!)

### Štandardné filtre pre fashion/sport:
| Filter | Metafield | Typ |
|--------|-----------|-----|
| Farba | `option.color` | list.single_line_text + swatche |
| Veľkosť | `option.size` | list.single_line_text |
| Aktivita | `custom.activity` | list.single_line_text |
| Cena | `filter.price` | range |
| Dostupnosť | `filter.availability` | boolean |

---

## Fáza 4: Variant stratégia

### Rozhodnutie o zobrazení variantov:
- [ ] **Farebné varianty:** Master produkt + color swatche (odporúčané) ALEBO samostatné karty
- [ ] **Veľkostné varianty:** Dropdown / grid na produkt stránke
- [ ] **Shopify variant limit:** max 100 variantov / produkt (3 options × kombinácie)

### Swatche setup:
- [ ] Definovať COLOR_MAP — názov farby → hex kód (vrátane neon/špeciálnych)
- [ ] Rozhodnúť: obrázkové swatche vs. farebné bodky
- [ ] Na kategóriách: zobraziť swatche pod kartou produktu

---

## Fáza 5: Cross-sell & Upsell

### Pre každý produkt definovať:
- [ ] **Súvisiace (cross-sell)** — iný typ produktu, rovnaká aktivita
  - Metafield: `custom.complementary_products` (list.product_reference)
  - Príklad: podkolenky → ponožky, návleky → šortky
- [ ] **Alternatívne (upsell)** — rovnaký typ, iná línia/úroveň
  - Metafield: `custom.related_products` (list.product_reference)
  - Príklad: Energy podkolenky → Therapy podkolenky, Air → Extreme

### Zobrazenie:
- [ ] Na produkt karte (tagy/badges) — viditeľné aj v prehľade
- [ ] Na produkt stránke (sekcia "Mohlo by sa vám hodiť" + "Alternatívy")
- [ ] V košíku (upsell popup alebo sekcia)

---

## Fáza 6: Bundle & zľavová stratégia

### Rozhodnutie:
- [ ] Standalone bundle produkty — áno/nie? (Royal Bay: NIE)
- [ ] **Shopify Bundles app** (free) — dynamické balíčky
- [ ] **Automatic Discounts** — zľava pri kúpe X+ kusov
- [ ] Zľavové kódy — štruktúra a pravidlá
- [ ] Outlet pravidlá — stála zľava vs. kódy

---

## Fáza 7: Gender stratégia

### Rozhodnutie:
- [ ] Separátne M/Ž produkty? (Royal Bay: NIE, všetko Unisex)
- [ ] Separátne M/Ž kategórie? (odporúčané: NIE pri unisex produktoch)
- [ ] Gender targeting cez:
  - [ ] Blog články ("Najlepšie kompresné podkolenky pre bežkyne")
  - [ ] Homepage sekcie / bannery
  - [ ] Email segmentácia
  - [ ] Meta tags (nepotrebné pre Shopify SEO ak unisex)

---

## Fáza 8: SEO & LLM optimalizácia

### Technické SEO
- [ ] URL štruktúra — čisté, krátke, bez parametrov
- [ ] 301 redirecty — stará platforma → nové URL (kompletná mapa!)
- [ ] Sitemap.xml — automatický Shopify
- [ ] Robots.txt — NOINDEX pre filtre, paginaci, variantné URL
- [ ] Canonical URL — pre varianty a filtrované stránky
- [ ] Schema.org markup — Product, BreadcrumbList, Organization

### Indexovanie pravidlá
| Typ stránky | INDEX? | Canonical |
|---|---|---|
| Hlavná kategória | ✅ INDEX | self |
| Aktivitná kolekcia | ✅ INDEX | self |
| Filtrovaná URL | ❌ NOINDEX | parent kategória |
| Paginacia (?page=2) | ❌ NOINDEX | page 1 |
| Variant URL | ❌ NOINDEX | master produkt |
| Outlet | ✅ INDEX | self |

### LLM / GEO optimalizácia
- [ ] Každý produkt má `llmDesc` — popis v prirodzenom jazyku pre AI vyhľadávače
- [ ] Kategórie majú úvodný text (nie len zoznam produktov)
- [ ] FAQ sekcia na kľúčových stránkach
- [ ] Brand story stránka (About) — buduje E-E-A-T

---

## Fáza 9: Interaktívny planner (HTML deliverable)

### Taby / sekcie:
- [ ] **All Products** — karty všetkých produktov s parametrami
- [ ] **Unassigned** — produkty bez kategórie (pre kontrolu)
- [ ] **Category Tree** — vizualizácia stromu kolekcií
- [ ] **Variant Strategy** — zobrazenie farebných variantov
- [ ] **Filter Preview** — mockup e-shop kategórie (sidebar filtre + product grid)
- [ ] **Shopify Setup** — menu štruktúra, metafield schema
- [ ] **SEO & LLM Guide** — pravidlá indexovania, meta šablóny

### Funkcie planneru:
- [ ] Vyhľadávanie a filtrovanie produktov
- [ ] Export: JSON, CSV, Markdown (+ Download All button)
- [ ] Cross-sell & upsell tagy na kartách produktov
- [ ] SKU kódy (italic, v zátvorkách)
- [ ] Color swatche (reálne hex farby)
- [ ] localStorage persistence

### Zdieľanie s agentúrou:
- [ ] Push na GitHub
- [ ] GitHub Pages URL → poslať agentúre
- [ ] Agentúra vie stiahnuť dáta v JSON/CSV pre import

---

## Fáza 10: Pred-launchový checklist

### Obsah
- [ ] Jazykové mutácie (SK, EN...)
- [ ] Size guide (tabuľky veľkostí)
- [ ] Recenzie — import alebo fresh start?
- [ ] Legal: Obchodné podmienky, GDPR, cookies
- [ ] Kontakt, doprava, vrátenie — info stránky

### Technické
- [ ] 301 redirecty nasadené a otestované
- [ ] Shopify Collaborator prístup pre agentúru
- [ ] Testovacia objednávka (celý flow)
- [ ] Platobná brána — test transakcia
- [ ] Doprava — test výpočet
- [ ] Email notifikácie — šablóny nastavené
- [ ] Google Search Console — nový sitemap
- [ ] Google Analytics / GA4 — tracking nasadený
- [ ] Facebook Pixel / Meta — ak relevantné

### Launch
- [ ] DNS presmerovanie na Shopify
- [ ] SSL certifikát aktívny
- [ ] Monitoring prvých 48h — 404ky, broken redirects, chyby v objednávkach

---

## Výstupné artefakty pre agentúru

Po dokončení checklistu by agentúra mala dostať:

| Deliverable | Formát | Účel |
|---|---|---|
| Interaktívny planner | HTML (GitHub Pages) | Vizuálny prehľad celého setupu |
| Produktové dáta | JSON + CSV | Import do Shopify |
| Kategórie & SEO | Markdown + HTML | Štruktúra kolekcií + meta tagy |
| Cross-sell mapa | JSON (v planneri) | Nastavenie related products |
| Filter schema | JSON (v planneri) | Metafield konfigurácia |
| 301 redirect mapa | CSV | Migrácia URL |
| Meeting notes | Markdown | Kontext rozhodnutí |

---

## Časový odhad (pri 28 produktoch)

| Fáza | Kto | Trvanie |
|---|---|---|
| 0. Príprava | Owner | 1 deň |
| 1. Katalóg | Owner + Claude | 2-3 hodiny |
| 2. Kategórie | Owner + Claude | 1-2 hodiny |
| 3-7. Filtre, varianty, cross-sell, bundles, gender | Owner + Claude | 2-3 hodiny |
| 8. SEO | Owner + Claude | 1-2 hodiny |
| 9. Planner HTML | Claude | 2-4 hodiny |
| 10. Pred-launch | Owner + Agentúra | priebežne |

**Celkovo: ~2 pracovné dni pre kompletné podklady** (pri existujúcom XML exporte).

---

*Template vytvorený z Royal Bay Shopify migrácie. GitHub: jurajgiacko/royalbay-shopify*
