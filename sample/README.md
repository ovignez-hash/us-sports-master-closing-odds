# US Sports Master — Historical Closing Odds (V2) — SAMPLE

This sample holds 20 rows per league: the first 10 rows and the last 10 rows of each file of the full dataset, so both ends of the history can be checked. Same files, same columns and same format as the full dataset; only the number of rows changes. The README of the full dataset follows.

---

## US Sports Master — Historical Closing Odds (V2)

Nine leagues, one CSV per league, updated to **2 November 2026** (games played up to that day, North American time).

Source: OddsPortal. The odds are the average closing prices shown by the source, not attributable to any single bookmaker. UFC results are completed from the official UFC fight statistics (all years) and from our UFC Multi-Market dataset (14 January 2018 – 20 June 2026). The official statistics also give the event, location and per-fighter stats of 5,602 fights (see the UFC section).

## What's new in V2

Dates below are Paris dates, as in the files.

- All nine files updated to early November 2026: 983 team-sport games added (966 dated from 1 October 2026, Paris time, plus the 12 MLB and 5 NHL games below) and 487 UFC fights added.
- MLB: 12 games missing from V1 are now included. In 2026, when the same two teams played twice on the same calendar day (Paris time) with the same final score, V1 kept a single row. Both games are now listed, each with its own kick-off time and closing odds. The kick-off time of 9 V1 rows is corrected: 8 of these games, which carried the time of the other game, and Milwaukee Brewers – Arizona Diamondbacks (13-1) on 30 April 2026.
- MLB: one game removed, Cleveland Guardians – Chicago White Sox, dated 30 September 2026 in the Wild Card round by the source. The White Sox played Houston that day. The real game (same score) is listed on 3 October 2026, in the Division Series (Stage `Play Offs`).
- NHL: the 2026/2027 season opened on 29 September 2026. The five games of 29–30 September 2026 (evening of 29 September in North America), left out of V1 as presumed preseason, are now included.
- NCAAB: Oregon – VCU Rams (21 March 2021) was never played (declared a no contest). It is now marked `Cancelled`. Two games that the source wrote twice on the same day are now listed once (the 18:00 copy, without odds, is removed): Oregon State – Washington (7 March 2010) and Miami (Ohio) – Ohio (3 March 2012).
- All other V1 team-sport rows are kept with the same values.
- UFC: every V1 fight is kept, with 13 new columns: `Status`, `Event`, `Location`, `Method_Detail`, `Finish_Time` and 8 per-fighter stats (knockdowns, significant strikes landed, takedowns landed, submission attempts). The 487 added fights (57 of them cancelled bouts) are 432 fights dated after 8 March 2026 and 55 older fights (2017–2025) that were missing from V1. 1,653 fights that the source left without a result now have their outcome (1,599 with a winner); 3 remain without one. Every win now has a detailed method (KO, TKO, KO/TKO, SUB, DEC or DQ), except 6 fights whose result was changed after the event: 678 of the source's TKO wins were submissions. Four results of the source are corrected (see the UFC section).

## Coverage

| League | Seasons | First match | Last match | Rows |
|---|---|---|---|---|
| NFL | 2008/2009 – 2026/2027 | 2008-09-05 | 2026-11-03 | 5,005 |
| NBA | 2008/2009 – 2026/2027 | 2008-10-29 | 2026-11-03 | 23,187 |
| MLB | 2006 – 2026 | 2006-05-15 | 2026-10-29 | 48,945 |
| NHL | 1998/1999 – 2026/2027 | 1998-10-09 | 2026-11-03 | 35,040 |
| NCAAF | 2008/2009 – 2026/2027 | 2008-10-17 | 2026-11-01 | 15,203 |
| NCAAB | 2008/2009 – 2026/2027 | 2008-11-20 | 2026-11-03 | 79,780 |
| MLS | 1998 – 2026 | 1998-03-21 | 2026-11-02 | 9,100 |
| WNBA | 2009 – 2026 | 2009-06-06 | 2026-11-01 | 4,225 |
| UFC | 2013 – 2026 | 2013-02-03 | 2026-11-01 | 6,596 |

227,081 rows in total. Dates are in Central European Time, so a game played on the evening of 2 November 2026 in North America shows as 3 November (see Format for the early seasons).

Not included: preseason games, All-Star games, ONE Championship fights.

Coverage follows the source, which misses some games: for example around fifty MLB games of 2018–2022, and 63 UFC fights of 2016–2026 that appear in the official UFC statistics. The UFC file has no fight in 2014, 56 in 2013 and 160 in 2015.

## Corrections to the source

In NFL 2008/2009 (from 19 October 2008) and NCAAF 2008/2009, the source's average mixed in a bookmaker with home and away reversed. Those closing odds were put back in the right order (NCAAF games priced by that bookmaker alone) or recomputed from the source's prices (games where it was one of three or four bookmakers). Where the prices could not be recovered (games averaged over two bookmakers), and for isolated games and fights whose prices cannot all be right (implied probabilities summing to less than 100%), the odds cells are left empty. They are also left empty for 5 games where the source shows only one of the two prices without telling which side it belongs to. In all, the closing odds of 597 games and 1 UFC fight differ from the source's; no row was removed for this reason. Four UFC results are corrected from the official UFC fight statistics (see the UFC section).

## Format

- CSV, UTF-8 with BOM, comma-separated, one row per match (or fight).
- `Date` is ISO 8601 (`YYYY-MM-DD`). `Date` and `Time` are in Central European Time (Europe/Paris, daylight saving included), so evening games in North America usually fall on the next calendar day.
- In the early seasons the source gives no kick-off time for most games: NHL 1998/1999–2006/2007 (9,559 of 10,251 games), MLS 1998–2007 (1,554 of 1,805) and MLB 2006–2007 (2,906 of 4,264) show a placeholder `Time` (`00:00`, or `23:55` to `23:59`), and their `Date` is the North American date.
- `Time` is empty for 28 team-sport games of September–November 2026 with no kick-off time available (MLS 15, NCAAB 6, NCAAF 5, MLB 2), and for the 487 UFC fights added in V2 (the source no longer shows it).
- Odds are American (moneyline) format. An empty odds cell means the source shows no price for that side (735 NCAAF and NCAAB games have a price for one side only), or that the source's prices were inconsistent or incomplete (see Corrections to the source).
- The first team is the home team.

## Team sports — columns (identical in the 8 files)

| Column | Description |
|---|---|
| League | NFL, NBA, MLB, NHL, NCAAF, NCAAB, MLS, WNBA |
| Season | `2025/2026` for leagues that span two years, `2026` otherwise |
| Stage | `Regular Season`, or the stage named by the source: `Play Offs`, `Wild Card`, `Bowl`, `Promotion - Play Offs` (NBA play-in), `Qualification - Play Offs`, `Placement Group`, `Commissioner's Cup` |
| Date, Time | Kick-off, Central European Time |
| Home_Team, Away_Team | Team names as written by the source |
| Home_Score, Away_Score | Final score (empty for cancelled, postponed or awarded games) |
| Winner | `Home`, `Away` or `Draw`, from the final score; empty when there is no score |
| Total_Score | Home_Score + Away_Score |
| Margin | Absolute score difference |
| Match_Ending | `Regular Time`, `Overtime`, `Shootout` (NHL), `Extra Time`, `Penalties` (MLS), `Cancelled`, `Postponed`, `Awarded` |
| Final_Result_Only | `Yes` or `No`, as flagged by the source. Filled up to early March 2026 (23 March 2026 in NCAAB); empty for later games, as the source no longer shows the flag |
| Home_Odds, Draw_Odds, Away_Odds | Closing odds. `Draw_Odds` is filled for the three-way markets only (NHL regulation time, MLS) |
| Bookmakers | Number of bookmakers in the average. Filled up to early March 2026 and empty for later games (no longer provided by the source); empty in NCAAB from the 2019/2020 season |

## UFC

Outcomes, methods, rounds and finish times are completed or detailed from two sources: the official UFC fight statistics (2013 to the event of 31 October 2026, dated 31 October – 1 November in Paris time) and our UFC Multi-Market dataset (14 January 2018 to the event of 20 June 2026, dated 20–21 June in Paris time; the "results dataset" below). Where the two give a different round or finish time, the official statistics are used. Single fights below are cited with their date in the file (Paris time).

- 1,653 fights without a result in the source now have their outcome: 1,599 wins, 15 draws and 39 no contests. The official statistics give 276 of them: the 229 fights after 20 June 2026, 30 fights before 14 January 2018, and 17 fights from the cards of 12 and 19 August 2023 (North American dates), which are missing from the results dataset.
- 3 fights remain `No result in source`: Road to UFC fights dated 4 February 2024, which neither source covers. The 16 fights cancelled after 20 June 2026 stay `Cancelled`.
- Four results of the source are corrected from the official statistics. Three fights marked as cancelled by the source took place: Rua – Nogueira (2 August 2015) and Werdum – Oleynik (9 May 2020) were won on points by Rua and Oleynik, and Miller – Alers (19 December 2015) ended in a no contest. The source's cancellation note on Werdum – Oleynik is removed; its row keeps the date, time and closing odds of the source's listing (9 May 2020, 23:00), while the other fights of that card (UFC 249) are dated 10 May. Correia – Reneau (12 March 2017) was a majority draw, not a win for Reneau.
- 15 fights whose result was changed after the event keep the result shown by the source (outcome, winner, method and round): 14 wins later changed to a no contest, and Tibau – Trujillo (8 November 2015), later changed to a disqualification win for Trujillo. Only the event, location and stats are added to them. The 6 wins still `Not specified` are among these 15 fights (the source only says "win").
- For the V1 fights, the method is detailed: "Not specified" → DEC for 1,965 fights and SUB for 1, TKO → SUB for 678, KO → TKO for 46, TKO → KO for 20, TKO → DQ for 3 and TKO → DEC for 1. The round is added for 3,225 fights and differs from V1 for 3. `DSQ` is now written `DQ` (3 fights).
- The official statistics do not separate knockouts from technical knockouts. `KO/TKO` is used for the 126 wins where only they give the method (109 of them after 20 June 2026). Elsewhere, `KO` and `TKO` come from the results dataset or the source.
- 5,602 fights have their event, location and per-fighter stats. Cancelled fights and the 3 fights without a result have none.

## UFC — columns

| Column | Description |
|---|---|
| Organization | `UFC`, `Road to UFC`, `UFC BMF Title`, `TUF Title`, `TUF 29 Title`, `TUF 30 Title` |
| Weight_Class, Gender, Year | As listed by the source (for some fights, the official statistics give an adjacent division or a catchweight) |
| Date, Time | Central European Time; `Time` is empty for the fights added in V2 |
| Event | Event name from the official statistics, e.g. `UFC 333: Volkanovski vs. Evloev`; empty for cancelled fights and the 3 fights without a result |
| Location | City, state or region, and country of the event |
| Fighter_1, Fighter_2 | Names as written by the source |
| Status | `Finished`, `Cancelled` or `No Contest`; empty for the 3 fights without a result |
| Outcome | `Win`, `Draw`, `No Contest`, `Cancelled`, or `No result in source` |
| Winner | Winning fighter, as written in Fighter_1 / Fighter_2 |
| Method | Wins only: `KO`, `TKO`, `KO/TKO`, `SUB`, `DEC`, `DQ`, or `Not specified` (6 wins, see above) |
| Method_Detail | Wins only: finishing technique given by the official statistics (`Punches`, `Rear Naked Choke`, `Kick`…), for 2,700 KO, TKO, KO/TKO and SUB wins; empty for decisions and disqualifications |
| Round | Round in which the fight ended (last round for decisions); for the 15 fights whose result was changed after the event, as shown by the source (empty for 6 of them) |
| Finish_Time | Time in that round when the fight ended (`5:00` for decisions and draws, with 8 exceptions given by the official statistics); empty for the 15 fights whose result was changed after the event |
| Fighter_1_Knockdowns, Fighter_2_Knockdowns | Knockdowns scored by each fighter |
| Fighter_1_Sig_Strikes, Fighter_2_Sig_Strikes | Significant strikes landed by each fighter |
| Fighter_1_Takedowns, Fighter_2_Takedowns | Takedowns landed by each fighter |
| Fighter_1_Sub_Attempts, Fighter_2_Sub_Attempts | Submission attempts by each fighter |
| Comment | Note shown by the source (title fight, withdrawal, no spectators…); empty for the fights added in V2. The cancellation note on Werdum – Oleynik (9 May 2020) is removed (see the UFC section) |
| Fighter_1_Odds, Fighter_2_Odds | Closing odds, American format |
| Final_Result_Only | `Yes` when the source flags the fight as final result only (all V1 fights); empty for the fights added in V2 |
