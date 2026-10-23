# Druhý mozek: skills a nastavení

Skills a nastavení pro Claude Code k druhému mozku, který je u Kateřiny Kryllové.

## Co tu je

- `plugins/druhy-mozek/` je plugin se čtyřmi skills: `brain-ingest`, `extract-voicenote`, `recall`, `write-a-skill`.
- `nastaveni/` obsahuje `AGENTS.md` (instrukce pro agenta), `CLAUDE.md` (odkaz na AGENTS a cesta ke kořeni druhého mozku) a `settings.json` (oprávnění). Tyhle soubory nejsou plugin, Claude Code je neumí doručit přes plugin. Zapisují se přímo do `~/.claude/` a vždy se nejdřív zazálohují.

## Instalace

Otevřete Claude Code a vložte:

```text
Nainstaluj plugin druhy-mozek z marketplace dolezal-td/druhy-mozek-katerina.
Spusť `claude plugin marketplace add dolezal-td/druhy-mozek-katerina` a potom
`claude plugin install druhy-mozek@druhy-mozek-katerina`. Pak vypiš seznam skillů.
```

Nastavení (AGENTS, CLAUDE, settings) je v prompt kartě na webu portálu.

## Aktualizace

Plugin se aktualizuje sám z tohoto repa. Když se něco změní, dejte vědět Tomášovi.
