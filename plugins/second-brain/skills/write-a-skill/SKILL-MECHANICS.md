# Mechanika skillu

Co se mění, když je dokument skill. Zbytek psaní řídí [SKILL.md](SKILL.md).

## Spouštění

- **Model-invoked** skill má description. Agent ho najde sám a mohou ho volat jiné skilly. Cena: description je v kontextu při každém tahu.
- **User-invoked** skill má `disable-model-invocation: true`. Description je jednořádkové shrnutí pro člověka, bez triggerů. Nulová context load; spustí ho jen uživatel napsáním `/název`, žádný jiný skill ho nedosáhne. Pro Codex přidej `agents/openai.yaml` s `allow implicit invocation: false`.

Model-invoked jen když ho agent musí najít sám, nebo ho volá jiný skill. Jinak user-invoked. Sdílená reference dvou user-invoked skillů leží v obyčejném souboru mimo skill systém, protože se navzájem nedosáhnou.

Dělení podle spouštění: nový model-invoked skill odděl, když má vlastní leading word, které uživatel v promptech opravdu používá. Model-invoked skill, který obsahuje jen referenci, je místo pro referenci sdílenou víc skilly: zavolají ho a text žije na jednom místě.

## Router

Když user-invoked skillů přibude nad to, co si uživatel pamatuje, jeden user-invoked router je vyjmenuje a řekne, kdy který. Jen napovídá, nespouští.

## Frontmatter a konvence

- `name`: anglicky, malá písmena a pomlčky.
- `description` model-invoked skillu: česky, dvě věty. Co dělá; kdy ho použít. Triggery jen u skutečně různých větví, doslovně jak je uživatel říká, v uvozovkách. Popis workflow do description nepatří, agent by pak tělo přeskočil.
- Tělo: česky, rozkazovací způsob, kroky před referencí. Anglické leading words nech anglicky.
- Skill obsahuje jen to, co agent potřebuje k běhu. README, changelog a lidské docs patří jinam.

## Postup

1. Přečti cílový soubor a instrukce nad ním (CLAUDE.md projektu, router, který ho volá). Hotovo, když víš, kdo skill volá a co už řeší nadřazený dokument.
2. Rozhodni spouštění a co jde za pointer. Hotovo, když každá věta v hlavním souboru patří všem větvím.
3. Napiš nebo prořež a ukaž diff před zápisem.
4. Otestuj typickým triggerem. Hotovo, když se skill načte na trigger, na jiný ne, a nic v něm neduplikuje jiný zdroj.
