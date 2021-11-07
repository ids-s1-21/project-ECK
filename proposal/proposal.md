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
    ## chr  (14): racename, driverRef, surname, constructorRef, constructorname, co...
    ## dbl  (12): raceId, year, round, driverId, constructorId, resultId, number, g...
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
| character                                        | 14       |
| Date                                             | 1        |
| numeric                                          | 12       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |          |
| Group variables                                  | None     |

Data summary

**Variable type: character**

| skim\_variable  | n\_missing | complete\_rate | min | max | empty | n\_unique | whitespace |
|:----------------|-----------:|---------------:|----:|----:|------:|----------:|-----------:|
| racename        |          0 |              1 |  16 |  29 |     0 |        48 |          0 |
| driverRef       |          0 |              1 |   3 |  18 |     0 |       853 |          0 |
| surname         |          0 |              1 |   3 |  23 |     0 |       794 |          0 |
| constructorRef  |          0 |              1 |   2 |  20 |     0 |       210 |          0 |
| constructorname |          0 |              1 |   2 |  25 |     0 |       210 |          0 |
| constructornat  |          0 |              1 |   5 |  13 |     0 |        24 |          0 |
| position        |          0 |              1 |   1 |   2 |     0 |        34 |          0 |
| positionText    |          0 |              1 |   1 |   2 |     0 |        39 |          0 |
| time            |          0 |              1 |   2 |  11 |     0 |      6523 |          0 |
| milliseconds    |          0 |              1 |   2 |   8 |     0 |      6722 |          0 |
| fastestLap      |          0 |              1 |   1 |   2 |     0 |        80 |          0 |
| rank            |          0 |              1 |   1 |   2 |     0 |        26 |          0 |
| fastestLapTime  |          0 |              1 |   2 |   8 |     0 |      6313 |          0 |
| fastestLapSpeed |          0 |              1 |   2 |   7 |     0 |      6449 |          0 |

**Variable type: Date**

| skim\_variable | n\_missing | complete\_rate | min        | max        | median     | n\_unique |
|:---------------|-----------:|---------------:|:-----------|:-----------|:-----------|----------:|
| date           |          0 |              1 | 1950-05-13 | 2021-10-10 | 1990-07-01 |      1051 |

**Variable type: numeric**

| skim\_variable | n\_missing | complete\_rate |     mean |      sd |   p0 |     p25 |     p50 |      p75 |  p100 | hist  |
|:---------------|-----------:|---------------:|---------:|--------:|-----:|--------:|--------:|---------:|------:|:------|
| raceId         |          0 |              1 |   519.25 |  291.22 |    1 |  288.00 |   504.0 |   764.00 |  1067 | ▆▇▇▆▆ |
| year           |          0 |              1 |  1989.55 |   18.97 | 1950 | 1976.00 |  1990.0 |  2006.00 |  2021 | ▃▆▇▆▇ |
| round          |          0 |              1 |     8.28 |    4.86 |    1 |    4.00 |     8.0 |    12.00 |    21 | ▇▆▅▃▁ |
| driverId       |          0 |              1 |   251.84 |  259.27 |    1 |   56.00 |   159.0 |   347.00 |   854 | ▇▃▂▁▂ |
| constructorId  |          0 |              1 |    47.59 |   58.53 |    1 |    6.00 |    25.0 |    58.00 |   214 | ▇▂▁▁▁ |
| resultId       |          0 |              1 | 12641.24 | 7298.91 |    1 | 6320.75 | 12640.5 | 18960.25 | 25285 | ▇▇▇▇▇ |
| number         |          6 |              1 |    17.62 |   14.85 |    0 |    7.00 |    15.0 |    23.00 |   208 | ▇▁▁▁▁ |
| grid           |          0 |              1 |    11.20 |    7.27 |    0 |    5.00 |    11.0 |    17.00 |    34 | ▇▇▇▃▁ |
| positionOrder  |          0 |              1 |    12.93 |    7.74 |    1 |    6.00 |    12.0 |    19.00 |    39 | ▇▇▆▂▁ |
| points         |          0 |              1 |     1.81 |    4.05 |    0 |    0.00 |     0.0 |     2.00 |    50 | ▇▁▁▁▁ |
| laps           |          0 |              1 |    45.80 |   30.01 |    0 |   21.00 |    52.0 |    66.00 |   200 | ▅▇▁▁▁ |
| statusId       |          0 |              1 |    17.70 |   26.09 |    1 |    1.00 |    11.0 |    14.00 |   139 | ▇▁▁▁▁ |

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
