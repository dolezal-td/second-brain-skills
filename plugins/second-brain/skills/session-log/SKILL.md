---
name: session-log
description: Zapíše posuny právě dokončené práce do denního logu `_logs/YYYY-MM-DD.md` v druhém mozku a případně aktualizuje stránku projektu ve `_wiki/`. Použij, když řekneš „hotovo“, „končíme“, „zaloguj“, nebo zadáš /session-log.
allowed-tools: Read, Write, Edit, Bash, Glob, Grep
---

# Session log

Zapiš, co se v dnešní práci posunulo, aby to `recall` našel i za týden. Spuštění vždy zapíše aspoň jeden posun, i po čistě informační konverzaci.

Kořen druhého mozku (složka s `_inbox`, `_wiki` a `resources`) najdi v globálních instrukcích, sekce „Druhý mozek“, řádek `KOŘEN:`. Když chybí, zeptej se.

Nabídni zápis po dokončení uceleného kusu práce nebo před přechodem na jiný úkol: „Máme za sebou [souhrn]. Chceš zalogovat posun?“

## Postup

1. **Rekapitulace.** Projdi konverzaci a rozděl ji na posuny. Jeden posun = jedna konkrétní věc, která se stala (zapsáno, rozhodnuto, dokončeno, odloženo). Ke každému přidej čas, odkaz na dotčenou stránku ve wiki jako `[[wikilink]]` a krátký štítek (`#rozhodnuto`, `#zapsáno`, `#otevřeno`).
2. **Datum a čas.** Datum zjisti přes `date +"%Y-%m-%d"`, čas přes `date +"%H:%M"`. Pokud posun proběhl dřív v tomhle dni, odhadni čas a označ ho „přibližně“.
3. **Append do `KOŘEN/_logs/YYYY-MM-DD.md`.** Soubor založ, pokud neexistuje, s frontmatterem `datum: YYYY-MM-DD`. Existující obsah nech být, nové bullety přidávej na konec.
   ```markdown
   ## Posuny
   - **14:20** #rozhodnuto Zvolili jsme formát osnovy pro workshop, viz [[Osnova workshopu]]
   - **15:05** #zapsáno Vytěžená hlasovka z 22. 10., stránky [[Odolnost]] a [[Krizový plán]]
   ```
4. **Projektová stránka**, jen když se posunul stav projektu. Stránka je `KOŘEN/_wiki/projekty/<Projekt>.md`. Přepiš řádek `## Další krok` (jedna věc, co je teď na tahu) a ve frontmatteru srovnej `stav`. Dokončený projekt dostane `stav: hotovo` a prázdný Další krok. Historie na stránku nepatří, žije v logu.
5. **Ověření.** Vypiš, kam jsi zapsal (cesty k souborům) a které kroky jsi přeskočil a proč.

## Pravidla

- Log je jen pro přidání. Starý posun nemaž ani nepřepisuj, i když je špatně. Opravu zapiš jako nový řádek.
- Osobní údaje o lidech a firmách patří do wiki, ne do denního logu. Log říká, co se stalo, ne kdo je kdo.
- Obsidian syntaxi (wikilinky, callouty, frontmatter) dělej podle skillu `obsidian-markdown`.
