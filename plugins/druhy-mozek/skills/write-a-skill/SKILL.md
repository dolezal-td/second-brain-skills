---
name: write-a-skill
description: Píše a prořezává dokumenty, které čte agent: skilly, CLAUDE.md, AGENTS.md a odkazované docs. Použij při tvorbě nebo úpravě skillu, při zásahu do CLAUDE.md nebo AGENTS.md, nebo když Tomáš řekne „napiš skill“, „uprav skill“, „audit skillu“.
---

Reference pro každý dokument, který čte agent. Liší se jen obal, psaní je stejné: stejné páky vedou k tomu, že agent při každém spuštění projde stejný postup, a výstup je díky tomu předvídatelný.

Když je dokument skill, přečti [SKILL-MECHANICS.md](SKILL-MECHANICS.md): frontmatter, volba spouštění, router a Tomášovy konvence.

## Context pointer

Description skillu a řádek v CLAUDE.md jsou tentýž objekt: ukazatel, který je v kontextu pořád a jehož formulace rozhoduje, kdy agent materiál načte. Pointer říká dvě věci: co se za ním skrývá a ve kterých situacích (větvích) se má načíst. Každá větev má jeden trigger. Synonyma jsou jedna větev napsaná několikrát, sluč je do jedné. Nejdůležitější slovo dej na začátek, tam rozhoduje o spuštění. Když agent nutný materiál občas nenačte, chyba je ve formulaci pointeru. Nejdřív ji zpřesni. Materiál přesuň do hlavního souboru, až když zpřesnění nepomůže.

## Dvě zátěže

Context load je cena za text, který je v kontextu při každém tahu: description, řádek v CLAUDE.md. Cognitive load je cena, kterou platí Tomáš: musí si pamatovat, že dokument existuje a kdy po něm sáhnout. Ta druhá není chyba, je to cena za to, že rozhoduje člověk. Utrať ji tam, kde na lidském úsudku záleží.

## Informační hierarchie

Tři patra podle toho, jak rychle agent materiál potřebuje: krok v hlavním souboru (co agent dělá, v pořadí), reference v hlavním souboru (pravidla, do kterých nahlíží), reference za pointerem (jiný soubor, načtený jen když nastane daná větev). Do hlavního souboru patří, co potřebují všechny větve; za pointer patří, co potřebuje jen některá. Sprawl je dokument, který je dlouhý, i když v něm nic není dvakrát. Lék je rozdělit ho podle větví nebo podle pořadí kroků.

Reference, která patří za pointer, zasypává v hlavním souboru kroky a agent je pak plní nahodile. Uvnitř souboru drž definici pojmu, jeho pravidla a výjimky pod jedním nadpisem (co-location). Jeden význam rozsekaný po dokumentu je opak duplikátu a kontrola na duplikáty ho neodhalí.

## Kritérium hotovo

Každý krok končí podmínkou, kterou jde ověřit. „Pochop problém“ ověřit nejde; „mám jeden příkaz, který na tomhle bugu spolehlivě selže“ ano. Čím náročnější podmínka, tím víc práce agent odvede: „každý změněný model je zapsaný“ vynutí důkladnost, „vypiš změny“ ne. Náročnost platí i pro referenci: „použito každé pravidlo“ váže stejně jako „hotový každý krok“.

Vágní podmínka svádí k předčasnému ukončení kroku, protože agenta táhnou kroky, které vidí před sebou. Nejdřív zpřesni podmínku. Až když zůstane mlhavá a spěch opravdu vidíš, schovej další kroky za skutečnou hranici kontextu (subagent, handoff). Volání skillu ve stejné session nic neschová.

## Kdy dělit

Každé dělení utratí jednu ze dvou zátěží, takže dokument rozděl, jen když se to vyplatí. Podle pořadí rozděl, když další kroky svádějí ke spěchu na tom aktuálním; funguje to jen přes skutečnou hranici kontextu (viz Kritérium hotovo). Když naopak dvě sekvence spojíš, každý krok vidí kroky po něm a agent spíš ukončí krok předčasně. Dělení podle spouštění řeší [SKILL-MECHANICS.md](SKILL-MECHANICS.md).

## Leading words

Krátký pojem, který model zná z tréninku (tight loop, red, tracer bullet, seam), nese celé chování za jeden token. Hledej věty, které jdou sbalit do jednoho takového slova. Když stejné slovo žije v promptech, docs i kódu, agent podle něj dokument spolehlivěji najde. Slovo, které nepřebije výchozí chování („be thorough“), je no-op: vyměň ho za silnější („relentless“). Vlastní slovo funguje, jen když ho definuješ, a definice stojí tokeny, které slovo z tréninku dává zdarma. Zákaz škodí: „nedělej X“ přitáhne X do pozornosti. Piš, co agent má dělat. Tvrdý zákaz nech jen tam, kde pozitivní formulace nejde.

## Prořezávání

- Jeden význam, jeden zdroj pravdy. Duplikát je nejspolehlivější známka, že dokument nikdo netestoval.
- Zdrojem pravdy je i prostředí: package.json, strom složek, výstup --help. Opis prostředí je cache, vyplatí se jen tehdy, když je vyhledání drahé. Do dokumentu piš jen to, co agent nenajde v jednom souboru nebo jedním příkazem: nepsanou konvenci, důvod rozhodnutí, záludnost.
- Každou větu prožeň testem na no-op: změní chování agenta oproti tomu, co dělá i bez ní? Když ne, smaž celou větu, ne jen pár slov. Sporné věty rozhodne spuštění dokumentu, ne debata.
- Sediment jsou staré vrstvy, které v dokumentu zůstaly, protože přidávat je pohodlné a mazat se bojíme. Kratší dokument se snáz udrží aktuální.

Hotovo, když dokument funguje a už v něm nenajdeš duplikát, rozsekaný význam, sediment ani no-op.
