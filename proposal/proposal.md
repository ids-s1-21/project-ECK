Project proposal
================
ECK

``` r
library(tidyverse)
library(broom)
library(here)
library(skimr)
```

## 1. Introduction

We will be looking at the question **“What makes a successful Formula
One team?”**. In particular, we will look at Mercedes-AMG Petronas F1
Team, and their success in the hybrid era (2014-2020\*).

The data we are using comes from the Ergast Developer API
(**<http://ergast.com/mrd/>**). It provides data for the Formula One
(F1) racing series from 1950 to present. The data is collected from
official race classifications released by the FIA, Formula One’s
governing body.

Much of our analysis will focus on the *f1merged* dataframe, which
combines relevant data from the results, races, drivers & constructors
data frames. Each observation in this dataframe represents the result of
one driver at one race.

Variables in this data frame include:

-   Unique ID numbers and identifiers for each result, race, driver and
    constructor.
-   The year/season, round number, date and name of each race.
-   Driver names and numbers. Constructor names and nationalities.
-   Starting and finishing positions for each driver.
-   Laps completed, points gained, finishing time.
-   Fastest lap time, fastest lap speed and fastest lap ranking.
-   Status ID, which links to a data frame with detailed finishing
    statuses.

We will also look at the *qualifying* data frame, with variables for
race, driver, constructor and qualifying position, as well as fastest
lap times from each qualifying session.

Similarly we will use the *pit\_stops* data frame, with variables for
race, driver, stop number, lap number, time of the pit stop and duration
of the pit stop.

\**The 2021 season is excluded from our analysis because it is still
ongoing at the time of writing*.

## 2. Data

For this project, we will be using a combination of data frames from the
Formula One data set. The combined data frame *f1merged* will give us
the variables referenced above in the **Introduction** section.

Here is a skim of the *f1merged* data frame.

    ## Rows: 25280 Columns: 27

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr   (9): racename, driverRef, surname, constructorRef, constructorname, co...
    ## dbl  (17): raceId, year, round, driverId, constructorId, resultId, number, g...
    ## date  (1): date

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

|                                                  |          |
|:-------------------------------------------------|:---------|
| Name                                             | f1merged |
| Number of rows                                   | 25280    |
| Number of columns                                | 27       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |          |
| Column type frequency:                           |          |
| character                                        | 9        |
| Date                                             | 1        |
| numeric                                          | 17       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |          |
| Group variables                                  | None     |

Data summary

**Variable type: character**

| skim\_variable  | n\_missing | complete\_rate | min | max | empty | n\_unique | whitespace |
|:----------------|-----------:|---------------:|----:|----:|------:|----------:|-----------:|
| racename        |          0 |           1.00 |  16 |  29 |     0 |        48 |          0 |
| driverRef       |          0 |           1.00 |   3 |  18 |     0 |       853 |          0 |
| surname         |          0 |           1.00 |   3 |  23 |     0 |       794 |          0 |
| constructorRef  |          0 |           1.00 |   2 |  20 |     0 |       210 |          0 |
| constructorname |          0 |           1.00 |   2 |  25 |     0 |       210 |          0 |
| constructornat  |          0 |           1.00 |   5 |  13 |     0 |        24 |          0 |
| positionText    |          0 |           1.00 |   1 |   2 |     0 |        39 |          0 |
| time            |      18521 |           0.27 |   4 |  11 |     0 |      6522 |          0 |
| fastestLapTime  |      18444 |           0.27 |   7 |   8 |     0 |      6312 |          0 |

**Variable type: Date**

| skim\_variable | n\_missing | complete\_rate | min        | max        | median     | n\_unique |
|:---------------|-----------:|---------------:|:-----------|:-----------|:-----------|----------:|
| date           |          0 |              1 | 1950-05-13 | 2021-10-10 | 1990-07-01 |      1051 |

**Variable type: numeric**

| skim\_variable  | n\_missing | complete\_rate |       mean |         sd |        p0 |        p25 |        p50 |        p75 |        p100 | hist  |
|:----------------|-----------:|---------------:|-----------:|-----------:|----------:|-----------:|-----------:|-----------:|------------:|:------|
| raceId          |          0 |           1.00 |     519.25 |     291.22 |      1.00 |     288.00 |     504.00 |     764.00 |     1067.00 | ▆▇▇▆▆ |
| year            |          0 |           1.00 |    1989.55 |      18.97 |   1950.00 |    1976.00 |    1990.00 |    2006.00 |     2021.00 | ▃▆▇▆▇ |
| round           |          0 |           1.00 |       8.28 |       4.86 |      1.00 |       4.00 |       8.00 |      12.00 |       21.00 | ▇▆▅▃▁ |
| driverId        |          0 |           1.00 |     251.84 |     259.27 |      1.00 |      56.00 |     159.00 |     347.00 |      854.00 | ▇▃▂▁▂ |
| constructorId   |          0 |           1.00 |      47.59 |      58.53 |      1.00 |       6.00 |      25.00 |      58.00 |      214.00 | ▇▂▁▁▁ |
| resultId        |          0 |           1.00 |   12641.24 |    7298.91 |      1.00 |    6320.75 |   12640.50 |   18960.25 |    25285.00 | ▇▇▇▇▇ |
| number          |          6 |           1.00 |      17.62 |      14.85 |      0.00 |       7.00 |      15.00 |      23.00 |      208.00 | ▇▁▁▁▁ |
| grid            |          0 |           1.00 |      11.20 |       7.27 |      0.00 |       5.00 |      11.00 |      17.00 |       34.00 | ▇▇▇▃▁ |
| position        |      10768 |           0.57 |       7.91 |       4.79 |      1.00 |       4.00 |       7.00 |      11.00 |       33.00 | ▇▆▂▁▁ |
| positionOrder   |          0 |           1.00 |      12.93 |       7.74 |      1.00 |       6.00 |      12.00 |      19.00 |       39.00 | ▇▇▆▂▁ |
| points          |          0 |           1.00 |       1.81 |       4.05 |      0.00 |       0.00 |       0.00 |       2.00 |       50.00 | ▇▁▁▁▁ |
| laps            |          0 |           1.00 |      45.80 |      30.01 |      0.00 |      21.00 |      52.00 |      66.00 |      200.00 | ▅▇▁▁▁ |
| milliseconds    |      18522 |           0.27 | 6232734.40 | 1691425.64 | 207071.00 | 5410837.50 | 5812935.50 | 6432545.00 | 15090540.00 | ▁▇▃▁▁ |
| fastestLap      |      18444 |           0.27 |      42.28 |      16.95 |      2.00 |      32.00 |      45.00 |      54.00 |       85.00 | ▂▃▇▆▁ |
| rank            |      18249 |           0.28 |      10.45 |       6.19 |      0.00 |       5.00 |      10.00 |      16.00 |       24.00 | ▇▇▇▇▂ |
| fastestLapSpeed |      18444 |           0.27 |     202.74 |      21.35 |     89.54 |     192.53 |     204.13 |     215.75 |      257.32 | ▁▁▂▇▂ |
| statusId        |          0 |           1.00 |      17.70 |      26.09 |      1.00 |       1.00 |      11.00 |      14.00 |      139.00 | ▇▁▁▁▁ |

It’s perhaps worth noting that the large number of NA values in this
data frame do not signify errors in the data.

An NA value in the *position* column represents a driver that did not
finish that race, and data on individual lap times and speeds was not
available for much of F1’s history.

## 3. Data analysis plan

The plan for this data analysis is to explore the question  
**“What makes a successful Formula One (F1) team?”**

To investigate this, we will look at the predictor variables(‘position’
from the qualifying dataframe, ‘duration’, ‘stop’ from the pit\_stops
dataframe and ‘fastestLapTime’, ‘fastestLapSpeed’, ‘rank’, ‘points’, and
‘positionText’ from the results dataframe) and the outcome variable
(‘wins’ from the constructor\_standings dataframe) for Mercedes-AMG
Petronas F1 Team during the hybrid era.

To do this we will compare the duration of a pit stop for the team
throughout a season, and look at the efficiency and reliability of the
pit crew. We will also compare the fastest lap time to other teams to
explore the possible effect that updated engineering has had on the
sport.
