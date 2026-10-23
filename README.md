# Second brain: skills a nastavení

Skills a nastavení pro Claude Code k druhému mozku, který je u Kateřiny Kryllové.

## Co tu je

- `plugins/second-brain/` je plugin se čtyřmi skills: `brain-ingest`, `extract-voicenote`, `recall`, `write-a-skill`.
- `nastaveni/` obsahuje `AGENTS.md` (instrukce pro agenta), `CLAUDE.md` (odkaz na AGENTS a cesta ke kořeni druhého mozku) a `settings.json` (oprávnění). Tyhle soubory nejsou plugin, Claude Code je neumí doručit přes plugin. Zapisují se přímo do `~/.claude/` a vždy se nejdřív zazálohují.

## Instalace

Otevřete Claude Code a vložte:

```text
Nainstaluj plugin second-brain z marketplace dolezal-td/second-brain-skills.
Spusť `claude plugin marketplace add dolezal-td/second-brain-skills` a potom
`claude plugin install second-brain@second-brain-skills`. Pak vypiš seznam skillů.
```

Nastavení (AGENTS, CLAUDE, settings) je v prompt kartě na webu portálu.

## Aktualizace

Plugin se aktualizuje sám z tohoto repa. Když se něco změní, dejte vědět Tomášovi.
