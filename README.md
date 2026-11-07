# 👑 US Sports Master — Historical Closing Odds (1998–2026)

**Free sample: the first 10 and the last 10 rows of each of the 9 league files**

The full dataset holds **227,081 games and fights across 9 US leagues, from 1998 to 3 November 2026**: NFL, NBA, MLB,
NHL, NCAAF, NCAAB, MLS, WNBA and UFC, one CSV per league, with the closing odds, the final score and how each game
ended. NHL and MLS go back to 1998, MLB to 2006, NFL, NBA and the two NCAA leagues to 2008/09.

→ **[Get the full archive](https://sportsdataolivier.gumroad.com/l/ahlplc?utm_source=github&utm_medium=readme&utm_campaign=us_sports_master&utm_content=hero)** — 227,081 rows, 9 leagues · also on [Whop](https://whop.com/oliviersportsdata/us-sports-master-historical-closing-odds-1998-2026/?utm_source=github&utm_medium=readme&utm_campaign=us_sports_master&utm_content=whop_hero)

This sample is cut from the full files: the same columns, the rows copied byte for byte.

Source: OddsPortal. The odds are the average closing prices shown by the source, not attributable to any single
bookmaker. UFC results are completed from the official UFC fight statistics and from our UFC Multi-Market dataset.

---

## In this repository

| Path | Content |
|---|---|
| `sample/` | the 9 sample CSV files and their README |
| `US_Sports_Master_Verify_Before_You_Buy.ipynb` | the Verify Before You Buy notebook, run on the full files, with its results |

---

## Coverage of the full dataset

| League | Seasons | First game (Paris) | Last game (Paris) | Rows |
|---|---|---|---|---|
| NFL | 2008/09 – 2026/27 | 5 Sep 2008 | 3 Nov 2026 | 5,005 |
| NBA | 2008/09 – 2026/27 | 29 Oct 2008 | 3 Nov 2026 | 23,187 |
| MLB | 2006 – 2026 | 15 May 2006 | 29 Oct 2026 | 48,945 |
| NHL | 1998/99 – 2026/27 | 9 Oct 1998 | 3 Nov 2026 | 35,040 |
| NCAAF | 2008/09 – 2026/27 | 17 Oct 2008 | 1 Nov 2026 | 15,203 |
| NCAAB | 2008/09 – 2026/27 | 20 Nov 2008 | 3 Nov 2026 | 79,780 |
| MLS | 1998 – 2026 | 21 Mar 1998 | 2 Nov 2026 | 9,100 |
| WNBA | 2009 – 2026 | 6 Jun 2009 | 1 Nov 2026 | 4,225 |
| UFC | 2013 – 2026 | 3 Feb 2013 | 1 Nov 2026 | 6,596 |

227,081 rows in total, updated to 2 November 2026 (North American time). The UFC file counts 5,605 fights and 991
cancelled bouts.

---

## What's in this sample

| | |
|---|---|
| Rows | 180 — 20 per league: the first 10 rows and the last 10 rows of each file |
| Files | 9 CSV files, `sample/NFL_Closing_Odds_SAMPLE.csv` to `sample/UFC_Closing_Odds_SAMPLE.csv`, plus `sample/README.md`: how the sample is built, then the README of the full product |
| Columns | 18 in the 8 team-sport files, 29 in the UFC file |

The first rows show the oldest seasons as the source has them, for example placeholder kick-off times in NHL
1998/99 and MLS 1998. The last rows are the most recent games of each file, from October and early November 2026.

---

## Columns

**Team sports (8 files, the same 18 columns):**

| Column | Content |
|---|---|
| `League` | `NFL`, `NBA`, `MLB`, `NHL`, `NCAAF`, `NCAAB`, `MLS`, `WNBA` |
| `Season` | `2025/2026` for leagues that span two years, `2026` otherwise |
| `Stage` | `Regular Season`, or the stage named by the source: `Play Offs`, `Wild Card`, `Bowl`, NBA play-in… |
| `Date`, `Time` | kick-off, Central European Time (Europe/Paris) |
| `Home_Team`, `Away_Team` | team names as written by the source; the first team is the home team |
| `Home_Score`, `Away_Score` | final score |
| `Winner`, `Total_Score`, `Margin` | from the final score |
| `Match_Ending` | `Regular Time`, `Overtime`, `Shootout`, `Extra Time`, `Penalties`, `Cancelled`, `Postponed`, `Awarded` |
| `Final_Result_Only` | `Yes` or `No`, as flagged by the source, up to early March 2026 |
| `Home_Odds`, `Draw_Odds`, `Away_Odds` | closing odds; `Draw_Odds` only for the three-way markets (NHL regulation time, MLS) |
| `Bookmakers` | number of bookmakers in the source's average, up to early March 2026 |

**UFC (29 columns):** Organization, Weight_Class, Gender, Year, Date, Time, Event, Location, Fighter_1, Fighter_2,
Status, Outcome, Winner, Method, Method_Detail, Round, Finish_Time, knockdowns, significant strikes landed, takedowns
landed and submission attempts of each fighter, Comment, Fighter_1_Odds, Fighter_2_Odds, Final_Result_Only.

### How to read it

**Prices are American odds, as integers:** `-250`, and `200` for +200. **Markets:** moneyline for NFL, NBA, MLB,
NCAAF, NCAAB and WNBA; 1X2 in regulation time for NHL and MLS. **`Date` and `Time` are Central European Time**, so an
evening game in North America is usually dated the next day (the oldest seasons are the exception, see below).

```python
import pandas as pd

leagues = ["NFL", "NBA", "MLB", "NHL", "NCAAF", "NCAAB", "MLS", "WNBA", "UFC"]
data = {k: pd.read_csv(f"sample/{k}_Closing_Odds_SAMPLE.csv") for k in leagues}

def prob(us):  # American odds -> implied probability
    return -us / (-us + 100) if us < 0 else 100 / (us + 100)

nba = data["NBA"].dropna(subset=["Home_Odds", "Away_Odds"]).copy()
nba["margin"] = nba["Home_Odds"].map(prob) + nba["Away_Odds"].map(prob) - 1   # margin kept in the average price
```

---

## Said plainly

- **Closing odds only.** No opening odds, no line movement, no spreads, no totals, no bookmaker-by-bookmaker prices.
- **No preseason games, no All-Star games, no ONE Championship fights.**
- **Coverage follows the source, which misses some games.** MLB 2006 starts on 15 May 2006 and NCAAF 2008/09 on
  17 October 2008. There are no games from 4 to 14 September 2010 and from 7 to 22 May 2012 in MLB, from 4 July to
  28 August 1998 in MLS, and from 28 November to 18 December 2008 in NCAAB (Paris dates). Around fifty MLB games of
  2018–2022 and 63 UFC fights of 2016–2026 are also missing. The UFC file has no fight in 2014, 56 in 2013 and 160 in
  2015.
- **The oldest seasons have placeholder kick-off times** (`00:00`, or `23:55` to `23:59`): most games of NHL
  1998/99–2006/07, MLS 1998–2007 and MLB 2006–2007, whose `Date` is then the North American date.
- **From early March 2026, the source no longer shows the number of bookmakers or the "final result only" flag**
  (23 March 2026 in NCAAB, where `Bookmakers` is also empty from 2019/20).
- **Some games have no price for one or both sides**, mostly in college sports.
- **In NFL and NCAAF 2008/09, the source's average mixed in a bookmaker with home and away reversed.** Those odds were
  put back in the right order or recomputed from the source's prices; where that was impossible, and for a few
  isolated games with inconsistent prices, the cells are left empty: 597 games and 1 UFC fight in all.
- **UFC:** the official statistics do not separate knockouts from technical knockouts, so `KO/TKO` is used when only
  they give the method (126 wins). 3 Road to UFC fights have no result, and 15 fights whose result was changed after
  the event keep the result shown by the source.

More details in the README.

---

## Verify before you buy

The figures of the product page, the games season by season and integrity checks on every row, recomputed from the
nine full files:
[on Kaggle](https://www.kaggle.com/code/oliviersportsdata/us-sports-master-v2-verify-before-you-buy) · [in this repository](US_Sports_Master_Verify_Before_You_Buy.ipynb) (results shown).
The same sample is on [Kaggle](https://www.kaggle.com/datasets/oliviersportsdata/us-sports-master-historical-closing-odds) and [Hugging Face](https://huggingface.co/datasets/oliviersportsdata/US-Sports-Master-Historical-Closing-Odds).

---

## The full dataset

| | Sample | Full |
|---|---|---|
| Rows | 180 | 227,081 |
| Leagues | 9 | 9 |
| Seasons | first and last rows only | NHL and MLS from 1998 to 2026 |
| Files | 9 CSV + README | 9 CSV + README, in one ZIP of about 3.8 MB |

New games every month: the
[US Sports Master monthly updates](https://sportsdataolivier.gumroad.com/l/mudppx?utm_source=github&utm_medium=readme&utm_campaign=us_sports_master&utm_content=monthly) add the previous
month's games of the 9 leagues, in the same columns.

→ **[Get the full archive](https://sportsdataolivier.gumroad.com/l/ahlplc?utm_source=github&utm_medium=readme&utm_campaign=us_sports_master&utm_content=footer)** · also on [Whop](https://whop.com/oliviersportsdata/us-sports-master-historical-closing-odds-1998-2026/?utm_source=github&utm_medium=readme&utm_campaign=us_sports_master&utm_content=whop_footer)

---

## Licence

Sample: free to explore and evaluate.
Full product: single commercial user. Use the data as you wish, including the models, predictions and products you sell.
Redistribution and resale of the files, or of the raw data in another format, are not permitted.

A question before buying: contact@oliviersportsdata.com

---

*Olivier Sports Data — From Chicken Area 🐔*
