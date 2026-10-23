---
name: recall
description: Najde kontext z minulých konverzací k projektu, klientovi nebo tématu: nejdřív paměť Claude Code, pak druhý mozek. Zastaví se, jakmile to stačí. Použij, když řekneš „co bylo s…“, „co jsme řešili k…“, „osvěž si paměť“, nebo zadáš /recall téma.
allowed-tools: Grep, Glob, Read, Bash
---

# Recall

Najdi, co už o tématu víš, a shrň to. Hledej od nejlehčího zdroje a skonči, jakmile máš dost.

Kořen druhého mozku (složka s `_inbox`, `_wiki` a `resources`) najdi v globálních instrukcích, sekce „Druhý mozek“, řádek `KOŘEN:`.

## Kaskáda

1. **Paměť Claude Code.** `Grep` v `~/.claude/projects/` na téma (glob `*.md`). Když stačí, shrň a skonči.
2. **Wiki.** `Grep` v `KOŘEN/_wiki/` na téma. Stránky projektů a lidí mají ve frontmatteru `stav` a sekce `Další krok`. Přečti je celé, je jich málo.
3. **Historie konverzací.** `Grep` v `~/.claude/projects/` jen na konkrétní klíčová slova, když potřebuješ detail rozhodnutí. Velké soubory nečti celé: nejdřív `grep -n`, pak jen úsek.

## Výstup

- Krátké shrnutí: co o tématu víš, s odkazem na zdroj (soubor nebo datum konverzace).
- Otevřené věci a nerozhodnuté body, pokud nějaké jsou.
- Když nic nenajdeš, řekni to přímo a navrhni, co hledat jinak.
