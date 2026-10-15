# King County Housing – EDA für Amy Williams

Explorative Datenanalyse (EDA) von rund 21.600 Hausverkäufen in King County (Seattle, USA) aus dem Zeitraum Mai 2014 bis Mai 2015. Ziel ist es, datenbasierte Empfehlungen für eine Kundin abzuleiten: **wann und wo sie verkaufen bzw. kaufen sollte und ob sich eine Renovierung lohnt.**

## Die Kundin

| Name | Rolle | Profil |
|---|---|---|
| **Amy Williams** | Verkäuferin | Verkauft nach und nach mehrere zentrale Häuser aus dem Top-10-%-Segment und braucht im Gegenzug durchschnittliche Häuser am Stadtrand, in denen sie nicht auffällt. |

Daraus ergeben sich drei Fragen:

1. **Verkaufen:** Wann erzielen die Top-Häuser im Zentrum den besten Preis?
2. **Renovieren:** Lohnt es sich, vor dem Verkauf zu renovieren?
3. **Kaufen:** Wo und wann findet sie günstige, unauffällige Häuser am Stadtrand?

## Hypothesen und Ergebnisse

| | Hypothese | Ergebnis |
|---|---|---|
| **H1** | Im Frühling verkaufen bringt einen höheren Preis, im Winter kaufen ist günstiger. | ⚠️ **Teilweise bestätigt.** Im Gesamtmarkt ist der Frühling ca. 8 % teurer als der Winter. Für Amys Top-Häuser im Zentrum gibt es aber keinen Frühlingsaufschlag, nur der Herbst ist ca. 7 % schwächer. Im Winter kauft sie ca. 8 % günstiger. |
| **H2** | Eine Renovierung vor dem Verkauf steigert den Gewinn. | ⚠️ **Teilweise bestätigt.** Ab Bauqualität (Grade) 7 erzielen renovierte Häuser ca. 20–67 % mehr pro m². Im Top-Segment im Zentrum gibt es keinen messbaren Unterschied. Renovierungskosten sind nicht bekannt. |
| **H3** | Je weiter vom Stadtzentrum entfernt, desto günstiger und unauffälliger. | ⚠️ **Teilweise bestätigt.** Günstiger: klar ja, am Stadtrand kostet der m² etwa die Hälfte (r ≈ −0,62). Unauffälliger: nicht generell, aber in einzelnen Orten. |

## Wichtigste Erkenntnisse

1. **Lage schlägt alles (geografisch):** Der Preis pro m² sinkt mit der Entfernung zu Downtown Seattle von ca. 3.720 $ im Zentrum auf ca. 1.860 $ am Stadtrand. Das gilt im Norden wie im Süden, der Süden ist bei gleicher Entfernung aber durchgängig günstiger.
2. **Saison wirkt je nach Segment unterschiedlich:** Im Gesamtmarkt sind die Preise im April am höchsten und im Dezember am niedrigsten. Im teuren Segment im Zentrum spielt die Jahreszeit kaum eine Rolle, nur der Herbst fällt ab.
3. **Renovierung lohnt sich vor allem bei hochwertigen Häusern:** Der Aufpreis renovierter Häuser steigt mit der Bauqualität (Grade 7: ca. +20 %, Grade 10: ca. +67 %).
4. **Unauffällig wohnen ist eine Frage des Ortes:** In Duvall und Snoqualmie sind über 40 % der Häuser Durchschnittshäuser, im Schnitt der Randlage nur ca. 19 %.
5. **Wiederverkäufe:** 176 Häuser wurden innerhalb eines Jahres zweimal verkauft. Ihr Preis stieg im Median um ca. 54 %, der Markt im selben Zeitraum nur um ca. 3 %.

## Empfehlungen für Amy Williams

1. **Herbst meiden:** Die Top-Häuser im Zentrum gestaffelt im Winter oder Frühling verkaufen. Im Herbst (September bis November) bringen sie ca. 7 % weniger pro m².
2. **Nicht renovieren:** Die zentralen Top-Häuser vor dem Verkauf nicht renovieren, denn in diesem Segment gibt es keinen messbaren Aufpreis.
3. **Im Winter kaufen:** Durchschnittshäuser am Stadtrand im Winter kaufen. Sie sind dann ca. 8 % günstiger als im Frühling (Median 366.000 $ statt 400.000 $).
4. **Snoqualmie und Duvall:** Dort ist mehr als jedes dritte Haus ein Durchschnittshaus. Die größte Auswahl gibt es in Maple Valley.

## Annahmen

| Begriff | Definition |
|---|---|
| Zentrum | Downtown Seattle (47,6062° N, 122,3321° W) |
| Zentral | die 25 % der Häuser mit der geringsten Entfernung zum Zentrum (bis ca. 9,8 km) |
| Randlage | die 25 % der Häuser mit der größten Entfernung zum Zentrum (ab ca. 25,3 km) |
| Top-Häuser | die teuersten 10 % (ab 887.000 $) |
| Durchschnittshaus („unauffällig“) | kein Wasserzugang, keine besondere Aussicht; Preis, Wohnfläche, Grade und Zustand jeweils zwischen dem 25. und 75. Perzentil |
| Renoviert | `yr_renovated` > 0 |
| Jahreszeiten | Frühling = März–Mai, Sommer = Juni–August, Herbst = September–November, Winter = Dezember–Februar |

## Methodik

- **Datenbereinigung:** fehlende Werte auffüllen (`waterfront`, `view`, `yr_renovated`, `sqft_basement`), einen Tippfehler korrigieren (33 statt 3 Schlafzimmer), Flächen von sqft in m² umrechnen
- **Neue Merkmale:** Preis pro m², Entfernung zum Zentrum (Haversine-Formel), Lage-Zonen, Jahreszeit, Durchschnittshaus
- **Analyse:** Gruppenvergleiche über Mediane, Spearman-Korrelationen, Mann-Whitney-Tests, Auswertung der Wiederverkäufe
- **Visualisierung:** Boxplots, Liniendiagramme, Korrelations-Heatmaps, interaktive Karte (Plotly)

### Einschränkungen

- Die Daten decken nur ein Jahr ab, Saisoneffekt und Markttrend lassen sich daher nicht sauber trennen.
- Korrelationen zeigen Zusammenhänge, keine Ursachen.
- Renovierungskosten und Verkaufsdauer sind nicht in den Daten enthalten.
- Das Top-Segment im Zentrum ist klein (940 Verkäufe, davon 136 im Winter).

## Inhalt des Repositorys

| Datei / Ordner | Beschreibung |
|---|---|
| [01_assignment.md](01_assignment.md) | Aufgabenstellung: Daten, Aufgaben, Abgaben und Liste der Kundinnen und Kunden |
| [02_workflow.md](02_workflow.md) | Empfohlener EDA-Workflow |
| [03_fetching_the_data_eda.ipynb](03_fetching_the_data_eda.ipynb) | Verbindung zur PostgreSQL-Datenbank, Join der beiden Tabellen und Export nach `data/eda.csv` |
| [04_eda.ipynb](04_eda.ipynb) | **Hauptnotebook:** Bereinigung, Analyse der Hypothesen, Fazit und Empfehlungen |
| [presentation/](presentation/) | Präsentation für die Kundin: [PDF](presentation/praesentation_amy_williams.pdf) und [PowerPoint](presentation/praesentation_amy_williams.pptx), 12 Folien |
| [images/](images/) | Exportierte Diagramme aus der Analyse (Ausreißer, Preis nach Entfernung, Preis nach Monat und Lage) |
| [column_names.md](column_names.md) | Beschreibung der Spalten im Datensatz |
| [data/](data/) | Ablageort für `eda.csv`; die Daten selbst werden nicht ins Repository übernommen |
| [.env.example](.env.example) | Vorlage für die Zugangsdaten zur Datenbank |
| [pyproject.toml](pyproject.toml) / [uv.lock](uv.lock) | Projektkonfiguration und festgeschriebene Abhängigkeiten |

## Setup

Voraussetzungen: [uv](https://docs.astral.sh/uv/) und Zugang zur King-County-Datenbank.

```bash
git clone <repo-url>
cd <repo-name>
uv sync                  # erstellt .venv/ und installiert alle Abhängigkeiten
cp .env.example .env     # danach die Zugangsdaten zur Datenbank eintragen
code .
```

Die Notebooks in dieser Reihenfolge ausführen und dabei die `.venv` des Projekts als Kernel wählen:

1. **[03_fetching_the_data_eda.ipynb](03_fetching_the_data_eda.ipynb)** lädt die Daten über diesen Join und speichert sie als `data/eda.csv`:
   ```sql
   SELECT s.id AS sale_id, s.date, s.price, d.*
   FROM eda.king_county_house_sales AS s
   INNER JOIN eda.king_county_house_details AS d ON s.house_id = d.id;
   ```
2. **[04_eda.ipynb](04_eda.ipynb)** führt die komplette Analyse aus (*Restart* → *Run All*).

> [!CAUTION]
> `.env` enthält Zugangsdaten und darf nicht committet werden. Die Datei steht bereits in `.gitignore`.

## Tools

Python 3.13 · pandas · NumPy · Matplotlib · seaborn · Plotly · SciPy · SQLAlchemy / psycopg2 · uv

## Datenquelle

[House Sales in King County, USA (Kaggle)](https://www.kaggle.com/datasets/harlfoxem/housesalesprediction), bereitgestellt über die Kurs-Datenbank (Schema `eda`).
