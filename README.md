# 🧙‍♂️ Harry-Potter-Analysis-Power BI

<img src="img/hogwarts.jpg" width="800" />

### <img src="img/us.svg" width="24" /> English

This Power BI report analyzes character dialogues across all 8 Harry Potter films, enriched with metadata about movies, chapters, characters, houses, places, and spells.
It offers KPI overviews, drill-through to scene/movie level, and interactive slicing by movie/house/character/place/spell.

🔍 What’s inside

- Data prep (Power Query): standardized fields, fixed data types, handled nulls, derived features (e.g., dialogue length, scene counts, spell usage).
- Model (Star-Schema):
  - Facts: Dialogues, Scenes, BoxOffice
  - Dimensions: Movies, Characters, Houses, Chapters, Places, Spells, Dates
- Key DAX measures: total dialogues, dialogues by character/house/place, most-used spells, movie profitability & ROI, rolling trends.
- Report pages: KPI Overview, Character Focus, House Comparison, Spell Usage, Places & Scenes, Movie Finance, Drill-through (movie → chapter/scene).

✨ Highlights

- All movies are profitable (Series 1 stands out).
- More budget ≠ more revenue in recent entries.
- Dialogues center around Harry at Hogwarts.
- Gryffindor accumulates the most dialogue lines.
- Expelliarmus is the most used incantation in the film series.

📈 How to use

1. Open the .pbix in Power BI Desktop (latest version recommended).
2. Filter with slicers by movie/house/character/place/spell.
3. Use drill-through on movie → chapter/scene for context on dialogue distribution and spell usage.

<span id="head4"><img src="img/i_Start.png" width="25" /> Example DAX (illustrative)</span>

```bash
Total Dialogues = COUNTROWS(Dialogues)

Dialogues by Character =
CALCULATE(
    [Total Dialogues],
    ALLEXCEPT(Characters, Characters[CharacterName])
)

Most Used Spell =
VAR TopSpell =
    TOPN(1,
        SUMMARIZE(Spells, Spells[SpellName], "Uses", COUNTROWS(RELATEDTABLE(Dialogues))),
        [Uses], DESC
    )
RETURN
MAXX(TopSpell, Spells[SpellName])

Movie Profit =
SUMX(
    VALUES(Movies[MovieID]),
    SUM(BoxOffice[WorldwideGross]) - SUM(BoxOffice[Budget])
)

ROI % =
DIVIDE([Movie Profit], SUM(BoxOffice[Budget]))
```

### <img src="img/it.svg" width="24" /> Italiano

Questo report Power BI analizza i dialoghi dei personaggi nei 8 film di Harry Potter, integrando metadati su film, capitoli, personaggi, case, luoghi e incantesimi.
Offre KPI di sintesi, drill-through a livello di scena/film e slicer interattivi per film/casa/personaggio/luogo/incantesimo.

🔍 Contenuti

- Preparazione dati (Power Query): normalizzazione campi, tipizzazione corretta, gestione dei mancanti, variabili derivate (es. durata dialoghi, numero scene, uso incantesimi).
- Modello (Schema a Stella):
  - Fatti: Dialogues, Scenes, BoxOffice
  - Dimensioni: Movies, Characters, Houses, Chapters, Places, Spells, Dates
- Misure DAX chiave: dialoghi totali, dialoghi per personaggio/casa/luogo, incantesimi più usati, profittabilità & ROI dei film, trend temporali.
- Pagine report: KPI Overview, Focus Personaggio, Confronto Case, Uso Incantesimi, Luoghi & Scene, Finanza Film, Drill-through (film → capitolo/scena).

✨ Evidenze

- Tutti i film sono profittevoli (spicca la prima serie).
- Più budget non implica più incassi negli episodi recenti.
- I dialoghi si concentrano su Harry a Hogwarts.
- Grifondoro ha il maggior numero di battute.
- Expelliarmus è l’incantesimo più usato nella saga.

📈 Come usarlo

- Apri il .pbix con Power BI Desktop (versione aggiornata consigliata).
- Filtra con gli slicer per film/casa/personaggio/luogo/incantesimo.
- Usa il drill-through film → capitolo/scena per contestualizzare distribuzione dialoghi e uso degli incantesimi.

<span id="head4"><img src="img/i_Start.png" width="25" /> Esempio DAX (dimostrativo)</span>

```bash
Dialoghi Totali = COUNTROWS(Dialogues)

Dialoghi per Personaggio =
CALCULATE(
    [Dialoghi Totali],
    ALLEXCEPT(Characters, Characters[CharacterName])
)

Incantesimo più usato =
VAR TopSpell =
    TOPN(1,
        SUMMARIZE(Spells, Spells[SpellName], "Usi", COUNTROWS(RELATEDTABLE(Dialogues))),
        [Usi], DESC
    )
RETURN
MAXX(TopSpell, Spells[SpellName])

Profitto Film =
SUMX(
    VALUES(Movies[MovieID]),
    SUM(BoxOffice[WorldwideGross]) - SUM(BoxOffice[Budget])
)

ROI % =
DIVIDE([Profitto Film], SUM(BoxOffice[Budget]))

```
