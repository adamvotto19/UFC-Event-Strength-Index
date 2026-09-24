# UFC Event Strength Index

## Which UFC events were the strongest on paper?

The UFC Event Strength Index is a data analytics project that measures
the strength of UFC events using historical fighter performance,
rankings, experience, accomplishments, main-event strength, and
pre-event search interest.

The project analyzes 8,736 UFC fights across 777 events from
1994 through 2026.

Each event receives a score from 0 to 100 using four components:

- Card Quality — 40%
- Main Event Strength — 30%
- Star Experience — 25%
- Fanfare — 5%

All historical fighter statistics are calculated using only information
available before each fight, preventing future results from influencing
earlier UFC events.

## Key Result

UFC 214: Cormier vs. Jones 2 ranks #1 in the dataset with an
Event Strength Index of 90.50.


## Methodology

The Event Strength Index is built from four components.

### 1. Card Quality — 40%

Measures the overall strength and depth of the full event.

Inputs include:

- Number of title fights
- Historical UFC rankings
- UFC experience
- UFC win percentage
- Current UFC win streak
- Historical finishing rate

### 2. Main Event Strength — 30%

Measures the strength of the event's headlining matchup.

Inputs include:

- Combined UFC experience
- UFC win percentage
- Combined win streak
- Previous title fights
- Previous UFC main events
- Previous UFC bonuses
- Historical rankings

### 3. Star Experience — 25%

Measures the accomplishments and proven UFC experience across the card.

Inputs include:

- Previous UFC title fights
- Previous UFC main events
- Previous UFC performance and fight bonuses

### 4. Fanfare — 5%

Measures pre-event search-interest acceleration using Google Trends.

Search interest during the seven days before an event is compared with
the fighters' prior baseline interest. The metric is log-transformed to
reduce the effect of extreme spikes.

Because Google Trends data is not consistently available throughout UFC
history, missing fanfare data is not treated as a score of zero.

## Preventing Future Data Leakage

Every historical fighter statistic is calculated as it existed entering
the fight.

For example, a fighter's UFC record, win streak, title-fight experience,
main-event experience, and bonus history include only UFC fights that
occurred before the event being scored.

This prevents accomplishments earned later in a fighter's career from
artificially increasing the strength of earlier events.

## Scoring

Variables are converted to zero-preserving percentile scores.

A true value of zero remains zero, while positive values are ranked
relative to the other positive observations. Metrics that did not exist
during an earlier era, such as official UFC rankings, are treated as
unavailable rather than zero.

The final Event Strength Index uses:

- 40% Card Quality
- 30% Main Event Strength
- 25% Star Experience
- 5% Fanfare

When a component is historically unavailable, its weight is redistributed
across the available components rather than treating missing data as zero.


## Top 10 Strongest UFC Events

| Rank | Event | Date | Event Strength Index |
|---:|---|---|---:|
| 1 | UFC 214: Cormier vs. Jones 2 | 2017-07-29 | 90.50 |
| 2 | UFC Freedom 250 | 2026-06-14 | 89.32 |
| 3 | UFC 217: Bisping vs. St-Pierre | 2017-11-04 | 89.12 |
| 4 | UFC 239: Jones vs. Santos | 2019-07-06 | 86.17 |
| 5 | UFC 269: Oliveira vs. Poirier | 2021-12-11 | 85.76 |
| 6 | UFC 322: Della Maddalena vs. Makhachev | 2025-11-15 | 85.54 |
| 7 | UFC 276: Adesanya vs. Cannonier | 2022-07-02 | 84.56 |
| 8 | UFC 323: Dvalishvili vs. Yan 2 | 2025-12-06 | 84.10 |
| 9 | UFC 232: Jones vs. Gustafsson 2 | 2018-12-29 | 83.59 |
| 10 | UFC 308: Topuria vs. Holloway | 2024-10-26 | 83.30 |


## Key Findings

- UFC 214: Cormier vs. Jones 2 ranks as the strongest event in the
  dataset with an Event Strength Index of 90.50.

- Among the 50 highest-rated events, Star Experience is the strongest
  component for 74% of events, while Card Quality is strongest for 24%
  and Main Event Strength for 2%.

- Numbered UFC events average a 56.74 Event Strength score compared
  with 38.16 for UFC Fight Nights. Event type itself is not included
  as an input to the model.

- Strong Fight Night cards can still score highly. The highest-rated
  Fight Night in the dataset reaches 68.70.

- Event year has only a modest relationship with Event Strength:
  Pearson correlation = 0.313 and Spearman correlation = 0.283.

- The model is highly stable across alternative component-weighting
  systems, with rank correlations of approximately 0.99 between the
  tested models.

## Limitations

- Official UFC rankings are only available beginning in 2013, so
  ranking information is treated as unavailable for earlier events.

- UFC bonus history begins later than the earliest UFC events.
  Pre-bonus-era events are not penalized for the absence of bonuses.

- The Google Trends component is available for 505 of the 777 events
  and is used as a proxy for pre-event fan interest rather than a
  direct measurement of social-media engagement.

- Google Trends data is based on U.S. search interest, which may
  underrepresent internationally popular fighters and events.

- Google Trends values are relative search-interest measurements,
  not absolute audience-size measurements.

- The component weights are modeling choices rather than objectively
  correct values. Alternative weighting systems were tested to measure
  ranking sensitivity.

- The index measures the strength of an event based primarily on the
  fighters and information available around the event. It is not a
  measurement of how entertaining the fights ultimately were.


## Visualizations

### Top 15 Strongest UFC Events

![Top 15 Strongest UFC Events](visuals/top_15_ufc_events.png)

### UFC Event Strength Over Time

![Average UFC Event Strength by Year](visuals/event_strength_by_year.png)

### Component Breakdown of the Top 10 Events

![Top 10 Component Breakdown](visuals/top_10_component_breakdown.png)

## Technologies Used

- Python
- pandas
- NumPy
- Matplotlib
- Google Colab
- Google Trends / pytrends
- Historical UFC fight, ranking, and bonus data

## Project Files

- `data/UFC_EVENT_STRENGTH_INDEX_FINAL.csv` — final event-level dataset
- `visuals/top_15_ufc_events.png` — Top 15 ranking visualization
- `visuals/event_strength_by_year.png` — historical trend visualization
- `visuals/top_10_component_breakdown.png` — component comparison visualization
- `README.md` — project methodology, results, findings, and limitations

