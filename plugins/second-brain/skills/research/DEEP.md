# Hluboká větev

Navíc k rychlé rešerši. Místo jedné fronty dotazů tři paralelní subagenti (v Claude Code `Agent`, v Codexu delegace v promptu; spuštění v jednom tahu), každý jeden úhel; hlavní vlákno mezitím nic nehádá a čeká na jejich hlášení:

- **Oficiální**: dokumentace, ceník, changelog, release notes, primární výzkum.
- **Komunita**: hledání s `site:reddit.com`, `site:news.ycombinator.com`, `site:x.com`; vlákna celá přes `curl -sA "research" "<url>.json" | jq`; hledá reálné zkušenosti, problémy, limity, co dokumentace neřekne.
- **Alternativy**: 2 až 3 konkurenti, srovnání, kdy sáhnout po kterém.

Každý subagent vrátí claimy: `fact`, `source_url`, `confidence` (verified = oficiální stránka; high = důvěryhodný článek s odkazem; medium = komunita; low = jeden zdroj bez potvrzení), `date`. Claim bez URL se zahazuje.

## Ověření

Hlavní vlákno vezme 5 až 10 nejdůležitějších claimů v pořadí: ceny a plány, názvy modelů a verzí, klíčové limity, dostupnost (free tier, waitlist, regiony). Každý znovu přečti z `source_url`; cenu a verzi navíc druhým nezávislým zdrojem. Status: ✅ Confirmed, ⚠️ Differs (uveď obě verze), ❌ Not found. 403 nebo 429: jiná URL z jiného zdroje; 404: Not found; timeout: přeskoč a poznamenej.

Výsledek jde do Verifikačního logu a do rozdělení „Ověřená data“ vs. „Z kontextu zdrojů“. Hotovo, když je ověřeno aspoň 5 claimů a hlavička reportu nese jejich počet.
