# Workflow: Ako pracovat s Royal Bay projektom

> Tento dokument vysvetluje kde co zije, ako sa spracovavaju nahravky, a ako drzat PACT + Git pokope.

---

## Kde co zije

```
PACT (Cursor, lokalny disk)                 Git repo (GitHub → Claude Code + mobil)
─────────────────────────                    ─────────────────────────────────────────
VitarSport2026/Projects/                     github.com/jurajgiacko/royalbay-shopify
  royalbay-eshop-shopify/
  ├── KNOWLEDGE_BASE.md  ←── stratégia      ├── TODO.md  ←── mobilné tasky
  ├── 2026-03-*.md       ←── meetingy       ├── seo/     ←── SEO analýzy
  ├── contracts/         ←── zmluvy         ├── products/ ←── kategórie, dáta
  └── BRIEF-*.md         ←── brief          ├── design/  ←── HTML makety
                                             └── docs/    ←── meeting summaries
```

**Pravidlo:** Citlive veci (zmluvy, plne transcripty, financie) → PACT. Pracovne artefakty (SEO, produkty, tasky) → Git.

---

## Ked pride nahravka z PLAUD

### Krok 1: Spracuj v Cursore
Nahraj transkript do `VitarSport2026/Transcripts/` → meeting-coach rule ho automaticky spracuje:
- Vygeneruje strukturovany zapis (rozhodnutia, ulohy, insights)
- Ulozi do `VitarSport2026/Projects/royalbay-eshop-shopify/`
- Aktualizuje `ALL_TASKS.md`

### Krok 2: Sync do Git repo
Po spracovani povedz agentovi:
> "sync meeting do royalbay git repo"

Agent:
1. Vytiahne klucove rozhodnutia a ulohy z meeting zapisu
2. Vytvori stručný summary v `docs/meeting-summaries/YYYY-MM-DD-nazov.md`
3. Aktualizuje `TODO.md` o nove tasky
4. Commitne a pushne na GitHub

### Krok 3: Mobile
Otvor GitHub app → `royalbay-shopify` → `TODO.md` → vidis nove tasky, mozes checkovat.

---

## Ked pracujes na mobile

**GitHub app** (iOS/Android):
- Otvor repo `jurajgiacko/royalbay-shopify`
- `TODO.md` — checkuj hotove tasky, pridavaj nove
- `seo/`, `products/` — review SEO analyzov a kategorii
- Mozes editovat priamo v app (pencil icon)

**Co NEROBIT na mobile:**
- Neupravuj `KNOWLEDGE_BASE.md` v PACT — to rob len v Cursore
- Neupravuj zmluvy

---

## Ked Claude Code pracuje na Git repo

Claude Code ma pristup len ku Git repo, nie k PACT. Preto:

### Co mu mozes zadat:
- "Urob SEO keyword research pre kompresne podkolenky"
- "Navrhni URL strukturu pre Shopify"
- "Vygeneruj HTML maketu kategorii"
- "Analyzuj produktove data a navrhni cross-sell strom"

### Co Claude Code NEVIE (a netreba):
- Meeting transcripty (su v PACT)
- Zmluvy a cenove ponuky
- Interne financie firmy

### Ak Claude Code potrebuje kontext:
Skopiruj relevantnu cast z PACT `KNOWLEDGE_BASE.md` do Git repo `docs/` — len to co je potrebne, nie vsetko.

---

## Sync medzi PACT a Git

### PACT → Git (po meetingu, po rozhodnuti)
1. Meeting summary → `docs/meeting-summaries/`
2. Nove tasky → `TODO.md`
3. Nove rozhodnutia → aktualizuj `seo/` alebo `products/`

### Git → PACT (po praci Claude Code)
1. Hotovy SEO output → referencia v `KNOWLEDGE_BASE.md`
2. Nove learnings → `KNOWLEDGE_BASE.md` sekcia learnings
3. Dolezite rozhodnutia → `KNOWLEDGE_BASE.md`

### Kedy synchronizovat:
- **Po kazdom meetingu** s Mime Digital
- **Ked Claude Code dokoncí velku ulohu** (SEO analyza, kategorizacia)
- **Pred design meetingom** — uisti sa ze Git ma najnovsie podklady

---

## Priklad: Typicky tyzden

```
Pondelok rano:
  → Otvoris GitHub app, pozries TODO.md
  → Checknes co je hotove z minuleho tyzdna

Streda (PLAUD meeting s Mime):
  → Po meetingu: nahras transkript do Cursora
  → meeting-coach spracuje → zapis do PACT
  → "sync meeting do royalbay git repo"
  → TODO.md sa aktualizuje

Stvrtok:
  → Claude Code: "urob SEO analyzu pre nové kategorie"
  → Output ide do Git repo /seo/
  → Review na mobile alebo v Cursore

Piatok:
  → Design meeting → rovnaky flow
  → Pred meetingom: pull z Git → mas najnovsie podklady
```
