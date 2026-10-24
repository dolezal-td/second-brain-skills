---
name: show-me
description: Ukáže aktuální téma nejmenším užitečným náčrtem, diagramem nebo HTML artefaktem. Použij, když řekneš „/show-me“ či „ukaž mi to názorně“, nebo když potřebuješ vysvětlit složitější pojem nebo vztah.
---

# Show me

Vycházej z [Humanlayer show-me](https://github.com/humanlayer/skills/blob/main/plugins/show-me/skills/show-me/SKILL.md) od Dexe Horthyho. Ukaž jednu myšlenku co nejmenším tvarem a krátké vysvětlení umísti hned vedle něj.

1. Urči jednu otázku, kterou má vizualizace zodpovědět, a ověř v dostupném kontextu skutečné názvy, stavy a vztahy. Hotovo, když umíš otázku napsat jednou větou a každý prvek výstupu má oporu ve zdroji.
2. Vyber tvar podle otázky: srovnání jako tabulku; pravidlo jako pseudokód; běh jako strom volání; vlastnictví UI jako strom komponent; odpovědnosti široké změny jako mělký strom souborů; vztahy či datový tok jako Mermaid; změnu známého tvaru jako krátký `diff` náčrt. Když je většina tvaru nová nebo by vynechání okolí skrylo pořadí či vlastníka, ukaž celek. Hotovo, když jediný zvolený tvar vysvětluje hlavní bod bez zbytečných detailů.
3. Když vzhled, rozložení nebo stavy nelze srozumitelně ukázat jednodušším tvarem, vytvoř jeden soustředěný HTML soubor v dočasném adresáři. Použij skutečné popisky a data, vizuální jazyk produktu a čitelný desktop i mobil; soubor otevři uživateli. Pokud chce proklikávat chování nebo vybírat UI variantu, řekni mu o tom a nabídni prototyp. Hotovo, když zobrazený výsledek osobně zkontroluješ v potřebných velikostech.
4. Vedle zobrazení napiš nejvýše několik vět, které řeknou, na co se dívat. Nech jen volání, soubory, vlastnosti, stavy a hranice potřebné k odpovědi. Hotovo, když popisky i vztahy odpovídají zdrojům a člověk pozná hlavní závěr bez čtení celého kódu.
