---
name: brain-ingest
description: Zpracuje surový zdroj (hlasovku, konverzaci, článek) do stránek ve wiki druhého mozku. Použij, když chceš zdroj zařadit do wiki nebo řekneš „ingestuj“, „zařaď do wiki“, „zpracuj tenhle zdroj“.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Brain Ingest

Zpracuj jeden zdroj do wiki: z něj vytáhni pojmy, entity a srovnání, založ nebo rozšiř stránky a propoj je.

## Kořen druhého mozku

Kořen je složka, ve které leží `_inbox`, `_wiki` a `resources`. Cestu najdi v globálních instrukcích, sekce „Druhý mozek“, řádek `KOŘEN:`. Když chybí nebo je pořád zástupný text `DOPLŇ_CESTU…`, zeptej se uživatele na cestu a navrhni ji zapsat do globálních instrukcí.

Všechny cesty níže jsou vzhledem ke KOŘENI:

```
INBOX:     _inbox/          # syrové zdroje ve frontě
RESOURCES: resources/       # vytěžené čisté zdroje
WIKI:      _wiki/
EVERGREEN: _wiki/evergreen/ # trvalé pojmy a srovnání
```

Když `_wiki/evergreen/` ještě neexistuje, vytvoř ho. Chybí-li `index.md` nebo `log.md`, založ je s prázdnou kostrou.

## Vstup

Uživatel zadá konkrétní soubor (z `_inbox/` nebo `resources/`). Když nic neurčil, vypiš soubory v `_inbox/` a zeptej se, který zpracovat.

---

## Fáze 1: Načti kontext

1. Přečti `EVERGREEN/index.md`, ať víš, co ve wiki už je.
2. Přečti `EVERGREEN/log.md`, ať víš, co už bylo zpracováno.
3. Přečti zadaný zdroj.

### Typ zdroje

- **Hlasovka** (`_inbox/hlasovky/`): vezmi celý obsah, je to čistý myšlenkový proud.
- **Konverzace s AI** (export chatu): vezmi jen zprávy uživatele, rozhodnutí a myšlenky. Ignoruj výpisy kódu, nástrojů a odpovědi asistenta, pokud nenesou závěr.
- **Článek nebo import** (`_inbox/`): vezmi celý obsah.
- **Hotový výzkum** (`resources/`): je to už čistý zdroj. Odkazuj na něj přímo, samostatnou souhrnnou stránku nedělej.

---

## Fáze 2: Extrakce

Z obsahu zjisti:

- **Koncepty:** témata, principy, metodiky, mentální modely, názory.
- **Entity:** nástroje, produkty, organizace, lidé z pohledu jejich role v tématu.
- **Srovnání:** když zdroj porovnává dva a více přístupů, vznikne srovnávací stránka.
- **Citáty:** silné formulace uživatele zachovej doslovně.

Osobní údaje o konkrétních lidech, firmách a projektech nepatří do evergreen. Zapiš je jako stránku ve `_wiki/` mimo `evergreen/`, nebo se zeptej, jestli se mají zapsat vůbec.

---

## Fáze 3: Stránky

- Jedna stránka = jeden koncept. Raději víc krátkých než jedna dlouhá.
- Název česky, s mezerami: `Znalostní systém.md`, ne `znalostni-system.md`.
- Existující stránku **rozšiř (merge), nepřepisuj**. Aktualizuj pole `aktualizováno`.
- Každá stránka má frontmatter:

```
---
název: {Název}
typ: koncept        # koncept, entita, nebo srovnání
vytvořeno: {YYYY-MM-DD}
aktualizováno: {YYYY-MM-DD}
tagy: [{tagy}]
---
```

- Piš přirozenou češtinou. Na konec přidej sekci `## Vazby` s odkazy na související stránky. Sekci `## Zdroje` nedělej, zdroj uveď inline.
- Datum zjisti přes `date +"%Y-%m-%d"`, nikdy ho nehádej.

---

## Fáze 4: Propojení

- Každý zmíněný koncept nebo entita, která má stránku, je `[[wikilink]]`.
- Stránky linkují na sebe navzájem tam, kde to dává smysl. Raději víc odkazů než méně.

---

## Fáze 5: Index a log

- `EVERGREEN/index.md`: nové stránky přidej do správné sekce jako `- [[Název]] — krátký popis`.
- `EVERGREEN/log.md`: na konec připiš:

```markdown
## [{YYYY-MM-DD}] ingest | {Název zdroje}
- Nové stránky: [[Koncept 1]], [[Koncept 2]]
- Aktualizované: [[Existující stránka]]
```

---

## Fáze 6: Git (jen když je KOŘEN git repozitář)

Commitni jen soubory tohoto ingestu, ne `git add -A`, ať nesebereš rozdělanou práci. Nepushuj bez pokynu uživatele.

```bash
git add "<soubor1>" "<soubor2>" && git commit -m "ingest: {název zdroje}" -- "<soubor1>" "<soubor2>"
```

Jeden commit = jeden zdroj. Commit message česky.

---

## Pravidla

1. **Zdroj v `_inbox/` se needituje.** Až po zpracování ho uživatel přesune nebo smaže sám.
2. **Atomické koncepty.** Jeden koncept, jedna stránka.
3. **Inkrementální růst.** Existující stránky se rozšiřují, nepřepisují.
4. **Zachovej hlas uživatele.** Citáty doslovně, formulace blízké originálu.
5. **Nehádej.** Co není jisté (jméno, datum, číslo), označ `(?)` a zeptej se.
6. **Žádné hádání osobních údajů do evergreen.**
