---
name: research
description: Rešerše z primárních zdrojů s citací u každého faktu: rychlá, hluboká s paralelními subagenty a ověřením, nebo z YouTube. Použij, když řekneš „udělej research“, „ověř to“, „zjisti aktuální stav“, „deep research“, „co se říká na YouTube“, nebo když návrh změny v repu stojí na faktech o knihovně, nástroji či trhu.
allowed-tools: WebSearch, WebFetch, Agent, Bash
---

Rešerše na téma z tvé zprávy.

Jen nativní nástroje: hledání na webu (v Claude Code `WebSearch`, v Codexu web search), čtení stránky s konkrétní otázkou (`WebFetch`, v Codexu `curl` přes shell), Context7 pro dokumentaci knihoven, subagenti pro paralelní úhly (`Agent`, v Codexu delegace v promptu), Bash s `yt-dlp` a `curl` tam, kam čtení stránky nedosáhne. Tréninková data jsou zastaralá: do reportu jde jen to, co je ve zdrojích, každý fakt nese `[zdroj: URL]`, rozpor mezi zdroji uveď oběma verzemi, chybějící informace jako „Nezjištěno z aktuálních zdrojů“. Názvy a verze piš přesně podle zdroje.

## Větve

- **Rychlá** (výchozí): kroky 1, 2 a 4. Hotovo do pár minut.
- **Hluboká** (uživatel řekne „deep“, „důkladně“, nebo jde o rozhodnutí s penězi či nákupem): tři subagenti po úhlech a ověření claimů podle [DEEP.md](DEEP.md).
- **YouTube** (uživatel chce, co se říká ve videích, nebo jmenuje kanál či autora): [YOUTUBE.md](YOUTUBE.md); jde kombinovat s oběma větvemi.
- **Komunita** (Reddit, HN): hledání s `site:reddit.com` nebo `site:news.ycombinator.com`, vlákno pak celé přes `curl -sA "research" "<url-vlákna>.json" | jq` (veřejné JSON, bez klíče). X jen hledání se `site:x.com`.

## Cíl výstupu

- **Repo režim**: rešerše podporuje změnu v dostupném coding repu. Primární zdroje jsou oficiální dokumentace, standardy, zdrojový kód. Ukaž osnovu, po potvrzení ulož do existující složky pro research, jinak `docs/research/<slug>.md`.
- **Personal režim**: AI téma, nástroj, trh, trend. Ulož do `KOŘEN/resources/research/<YYYY-MM-DD> <téma>.md` (KOŘEN najdi v globálních instrukcích, sekce „Druhý mozek“) s frontmatterem `typ: research`.

## Postup

1. **Discovery**: 3 až 5 hledání v jednom tahu, každý z jiného úhlu: oficiální zdroj, srovnání s hlavní alternativou, problémy a limity, komunita (`site:reddit.com`), aktuální rok v dotazu. Hotovo, když máš 5 až 8 URL a u každé víš, proč je v seznamu.
2. **Primární zdroje**: čtení 3 až 5 nejdůležitějších URL s konkrétní otázkou („ceny plánů a limity“, „co se změnilo v poslední verzi“), ne „shrň stránku“. Knihovna, framework, API, CLI: Context7 `resolve-library-id` → `query-docs`. Hotovo, když každý fakt, který půjde do reportu, má URL.
3. **Hluboká nebo YouTube větev** podle přílohy, pak zpět sem.
4. **Syntéza** do formátu níže. Hotovo, když každý fakt má URL a report jde použít jako podklad bez dalšího hledání.

## Formát reportu

```markdown
# Research: {téma}
> Datum: YYYY-MM-DD | Mód: rychlý/hluboký | Zdroje: N stránek | (hluboký: Ověřeno: M faktů)

## Executive summary
2 až 3 věty jen ze zdrojů.

## Přehled
### {Položka}
- Co to je / Cena / Klíčové funkce / Ideální pro, každé s [zdroj: URL]
(hluboký: „Ověřená data“ s [ověřeno: URL, datum] a „Z kontextu zdrojů“ s [zdroj: URL])

## Srovnávací tabulka
| Nástroj | Cena | Klíčová funkce | Zdroj |

## Trendy a závěry
(hluboký: + Verifikační log | Claim | Zdroj | Status | Poznámka |)

## Zdroje
- URL s anotací a stářím (do 7 dní, do 30 dní, starší)
```

Celý výstup česky. Rozlišuj fakta (ze zdrojů) od syntézy (tvoje propojení).
