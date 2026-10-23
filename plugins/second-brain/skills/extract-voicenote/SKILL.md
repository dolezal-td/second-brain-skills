---
name: extract-voicenote
description: Vytěží syrový přepis hlasovky do tematicky uspořádaného extraktu: každý řádek zařazen k tématu, vyčištěný, související myšlenky seskupené, žádná myšlenka vynechaná. Použij, když řekneš „vytěž hlasovku“, „rozsekej přepis“, „přepis do sekcí“, nebo máš v _inbox/hlasovky/ nový přepis.
allowed-tools: Read, Write, Glob, Grep, Bash
---

# Extract Voicenote

Vrstva **tidy**: syrový přepis → uklizený tematický extrakt. Není to shrnutí ani destilace, to dělá `brain-ingest`. Je to **přeskládání bez ztráty**. Výstup je vstup pro `brain-ingest`.

**Železné pravidlo:** žádná myšlenka z originálu se nesmí ztratit.

Kořen druhého mozku (složka s `_inbox`, `_wiki` a `resources`) najdi v globálních instrukcích, sekce „Druhý mozek“, řádek `KOŘEN:`. Když chybí, zeptej se.

## Postup

1. Načti syrový přepis z `_inbox/hlasovky/`. Když v něm není žádná replika delší než 60 znaků, je to fragment: nevytěžuj, odpověz „fragment“ a skonči.
2. Zeptej se uživatele na kontext nahrávky (kde byl, s kým, k jakému tématu), pokud ho přepis neříká. Bez odpovědi nech kontext prázdný a označ ho v výstupu.
3. Projdi celý přepis a zmapuj témata (skoky, příběhy, opakování).
4. Vytvoř číslované sekce `## N. Téma` a každý řádek zařaď do jedné z nich.
5. Vyčisti každý řádek: oprav zjevné chyby přepisu tam, kde je význam jistý. Jména a pojmy ověř v `_wiki/`. Nejisté nech označené `(?)`.
6. Přidej sekce `Otevřené smyčky` (akční věci z proudu jako `- [ ]`) a `ASR poznámky a nejistoty`.
7. Ulož jediný soubor do `resources/hlasovky/{YYYY-MM-DD} {popisný název}.md`: nahoře extrakt, dole doslovný přepis ve sbaleném callout.
8. Raw přepis v `_inbox/` needituj ani nemaž. Z inboxu ho odstraní až `brain-ingest`.

## Princip úplnosti

Každý řádek originálu skončí ve výstupu, včetně fragmentů, vsuvek z reálného světa a opakování. Ty vsuvky dej do sekce `## Mezičas (vsuvka)`. Opakování slij pod jednu sekci.

Test hotového výstupu: jde z něj zrekonstruovat každá myšlenka originálu? Pokud ne, něco chybí.

## Čištění

| Udělej | Nedělej |
|---|---|
| Oprav zjevné chyby přepisu (rozpoznaná slova, která dávají nesmysl) | Nehádej nejisté názvy |
| Nejisté nech s `(?)` | Neparafrázuj do spisovné češtiny |
| Oprav gramatiku a interpunkci | Nezkracuj a neabstrahuj myšlenky |
| Zachovej hovorové tvary a důraz | Nepoužívej em dash (—) |

Hovorovost je záměr. Je to extrakt, ne finální text.

## Struktura výstupu

```markdown
# {Výstižný název}

**Datum:** {YYYY-MM-DD}
**Kontext:** {kde, jak dlouhá, situace}
**Status:** vytěženo do tematických sekcí

---

## 1. {Téma}
- {vyčištěný řádek}

---

## Otevřené smyčky
- [ ] {akční věc}

---

## ASR poznámky a nejistoty
- **{termín}**: {co je nejisté a co ověřit}

---

> [!quote]- Doslovný přepis (nezpracovaný)
> {celý syrový přepis 1:1, každý řádek s prefixem `> `}
```

Sbalený přepis zapiš jako `[!quote]-`, aby extrakt zůstal hlavním obsahem a raw byl po ruce.

## Časté chyby

| Chyba | Oprava |
|---|---|
| Vynechání „nedůležitých“ řádků | To je práce pro `brain-ingest`. Tady je pokrytí 1:1 |
| Dva soubory (raw zvlášť a vytěžený zvlášť) | Jeden soubor, extrakt nahoře, přepis dole |
| Doslovný přepis zkrácen | Zkopíruj ho celý do callout |
| Úprava raw souboru v `_inbox/` | Vytěžuj do nového souboru v `resources/` |
| Tvorba stránek ve wiki | To dělá `brain-ingest` |

Na konci napiš jednou větou, že extrakt je připraven pro `brain-ingest`.
