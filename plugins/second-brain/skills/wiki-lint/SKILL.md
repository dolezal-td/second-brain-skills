---
name: wiki-lint
description: Čtecí kontrola zdraví wiki druhého mozku: rozbité odkazy, osiřelé stránky, chybějící pole ve frontmatteru, zastaralé stránky a rozpor v indexu. Opravy nedělá. Použij, když řekneš „zkontroluj wiki“, „lint“, „je wiki v pořádku“, nebo po každých zhruba deseti zpracovaných zdrojích.
allowed-tools: Read, Grep, Glob, Bash
---

# Wiki Lint

Zkontroluj wiki a vypiš nálezy. Nic neopravuj, nic nepřepisuj, do wiki nic nepiš. Opravy jsou samostatná operace, která začne až po tvém pokynu.

## Kořen druhého mozku

Složka s `_inbox`, `_wiki` a `resources`. Cestu najdi v globálních instrukcích, sekce „Druhý mozek“, řádek `KOŘEN:`.

## Kontroly

Projdi všechny `.md` soubory v `KOŘEN/_wiki/` (kromě `index.md` a `log.md` je kontroluj zvlášť).

1. **Frontmatter.** Každá stránka má blok `---` na začátku a pole `název`, `typ`, `vytvořeno`, `aktualizováno`, `tagy`. Chybějící pole je nález.
2. **Rozbité odkazy.** Každý `[[odkaz]]` musí mít stránku se stejným názvem (nebo alias). Odkaz bez cíle je nález.
3. **Osiřelé stránky.** Stránka, na kterou nikdo neodkazuje, je nález nízké závažnosti. Může být záměrná.
4. **Index.** Každá stránka v `index.md` existuje a každá existující stránka je v indexu.
5. **Zastaralost.** Stránka, jejíž `aktualizováno` je starší než 30 dnů a která má otevřené věci, je nález.
6. **Zástupné texty.** `TODO`, `TBD`, `{text}` nebo `DOPLŇ` ve stránce je nález.
7. **Rozpory.** Jen pokud je rozpor vidět přímo v textu dvou stránek. Nesnaž se hodnotit věcnou správnost.

## Výstup

- Seřazeno podle závažnosti: nejdřív rozbité odkazy a chybějící pole, pak osiřelé a zastaralé stránky.
- U každého nálezu cesta k souboru a případně řádek.
- Na konci počty: kolik stránek, kolik nálezů v jednotlivých kontrolách.
- Opravy navrhni jako seznam, ale neprováděj je. Zeptej se, které z nich chceš udělat.
