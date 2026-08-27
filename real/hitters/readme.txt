Got the 'hitters' dataset from here:

https://gist.githubusercontent.com/keeganhines/59974f1ebef97bbaa44fb19143f90bad/raw/d9bcf657f97201394a59fffd801c44347eb7e28d/Hitters.csv

though it is available from many sources.

Changing it to tab delimited format and removing the first column (names), though these may be obtained from the above. Using * for missing salaary values.

---

hitters.rates.mixed.maximum.2.txt (with ground.truth/hitters.rates.knowledge.txt)

A re-expression of the same 322 players intended for causal search. Two problems
with the original variables motivate it. First, the career totals (CAtBat, CHits,
CHmRun, CRuns, CRBI, CWalks) are cumulative through 1986 and so contain the 1986
season statistics as components; every season -> career edge is an accounting
identity. Second, the career totals are almost perfectly collinear (each has
R^2 >= 0.92 on the other five, four of them above 0.99; smallest eigenvalue of
their correlation matrix 0.002), so any edge that names a particular career total
is arbitrary. The same holds, less severely, for the 1986 counting statistics.

Preparation:

1. Career totals replaced by prior-career totals, e.g. PAtBat = CAtBat - AtBat,
   i.e. the record before the 1986 season.
2. Each block reduced to exposure plus per-at-bat rates.
   Prior career: PAtBat, PAvg = PHits/PAtBat, PHRrate = PHmRun/PAtBat,
                 PBBrate = PWalks/PAtBat, PRBIrate = PRBI/PAtBat,
                 PRunsRate = PRuns/PAtBat.
   1986 season:  AtBat, Avg = Hits/AtBat, HRrate = HmRun/AtBat,
                 BBrate = Walks/AtBat, RBIrate = RBI/AtBat, RunsRate = Runs/AtBat.
   After this the smallest eigenvalue of the prior-career correlation matrix is
   0.14 and the largest within-block R^2 is 0.77 (PRBIrate on the others, which
   is a real relation).
3. Salary replaced by LogSalary (natural log of thousands of dollars); the 59
   missing salaries remain '*'.
4. The 22 rookies have PAtBat = 0, so their five prior rates are '*'. A further
   15 players have fewer than 50 prior at-bats and so have noisy prior rates;
   they are left in.
5. Years, League, Division, PutOuts, Assists, Errors, NewLeague are unchanged.
   League, Division, NewLeague are binary (A/N, E/W, A/N); everything else is
   continuous.

Knowledge (four temporal tiers, nothing else):

   0  Years League Division PutOuts Assists Errors
   1  PAtBat PAvg PHRrate PBBrate PRBIrate PRunsRate
   2  AtBat Avg HRrate BBrate RBIrate RunsRate
   3  LogSalary NewLeague

Fielding counts are in tier 0 as position proxies (they also scale with 1986
playing time, so tier 2 is defensible), and Years is in tier 0 as fixed before
1986. With listwise deletion the search runs on about 245 players who have both
a salary and a prior record, so the prior-rate edges describe established
players.

Questions this version can address: whether prior rates predict the
corresponding 1986 rates (persistence of contact, power, and plate discipline as
separate traits); whether RBI and runs rates are compositions of average and
power; and what 1987 salary depends on once exposure and rates are separated.
