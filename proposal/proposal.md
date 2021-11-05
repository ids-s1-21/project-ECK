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
One (F1) team?”**. In particular, we will look at Mercedes-AMG Petronas
F1 Team, and their success in the hybrid era (2014-2020).

The data we are using comes from the Ergast Developer API
(**<http://ergast.com/mrd/>**). It provides data for the Formula One
racing series from 1950 to present. The data is collected from official
race classifications released by the FIA, Formula One’s governing body.

Much of our analysis will focus on the *f1merged* dataframe, which
combines the data we need from the results, races, drivers &
constructors data frames. Each observation in this dataframe represents
the result of one driver at one race. The variables are:

-   Result ID **(Add f1merged variables to this and expand on what they
    are)**
-   Race ID  
-   Driver ID  
-   Constructor ID  
-   Driver number  
-   Starting grid position  
-   Official classification  
-   Points gained  
-   Laps completed  
-   Finishing time or gap  
-   Finishing time in milliseconds  
-   Lap number of fastest lap  
-   Fastest lap ranking relative to other drivers  
-   Fastest lap time  
-   Fastest lap speed  
-   Status ID

We will also look at several other data frames, both in conjunction with
the *f1merged* frame, and separately.

These will include the *qualifying* data frame, with variables for race,
driver, constructor & and position, as well as lap time.

Similarly we will use the *pit\_stops* data frame, with variables for
race, driver, stop number, lap number, time, duration, and duration in
milliseconds.

## 2. Data

For this project, we will be using a combination of dataframes from the
Formula One dataset. This combined dataframe will give us the variables
referenced above in the **Introduction** section.

Here is a glimpse at one of the data frames we will be using called
*f1merged*.

    ## Rows: 25280 Columns: 27

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (14): racename, driverRef, surname, constructorRef, constructorname, co...
    ## dbl  (12): raceId, year, round, driverId, constructorId, resultId, number, g...
    ## date  (1): date

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 25,280
    ## Columns: 27
    ## $ raceId          <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ year            <dbl> 2009, 2009, 2009, 2009, 2009, 2009, 2009, 2009, 2009, …
    ## $ round           <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ racename        <chr> "Australian Grand Prix", "Australian Grand Prix", "Aus…
    ## $ date            <date> 2009-03-29, 2009-03-29, 2009-03-29, 2009-03-29, 2009-…
    ## $ driverId        <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 12, 13, 15, 16, 17, 18,…
    ## $ driverRef       <chr> "hamilton", "heidfeld", "rosberg", "alonso", "kovalain…
    ## $ surname         <chr> "Hamilton", "Heidfeld", "Rosberg", "Alonso", "Kovalain…
    ## $ constructorId   <dbl> 1, 2, 3, 4, 1, 3, 5, 6, 2, 7, 4, 6, 7, 10, 9, 23, 9, 1…
    ## $ constructorRef  <chr> "mclaren", "bmw_sauber", "williams", "renault", "mclar…
    ## $ constructorname <chr> "McLaren", "BMW Sauber", "Williams", "Renault", "McLar…
    ## $ constructornat  <chr> "British", "German", "British", "French", "British", "…
    ## $ resultId        <dbl> 7573, 7563, 7559, 7558, 7572, 7571, 7561, 7568, 7567, …
    ## $ number          <dbl> 1, 6, 16, 7, 2, 17, 11, 4, 5, 10, 8, 3, 9, 20, 14, 22,…
    ## $ grid            <dbl> 18, 9, 5, 10, 12, 11, 17, 7, 4, 19, 14, 6, 20, 16, 8, …
    ## $ position        <chr> "\\N", "10", "6", "5", "\\N", "\\N", "8", "15", "14", …
    ## $ positionText    <chr> "D", "10", "6", "5", "R", "R", "8", "15", "14", "4", "…
    ## $ positionOrder   <dbl> 20, 10, 6, 5, 19, 18, 8, 15, 14, 4, 17, 16, 3, 9, 12, …
    ## $ points          <dbl> 0.0, 0.0, 3.0, 4.0, 0.0, 0.0, 1.0, 0.0, 0.0, 5.0, 0.0,…
    ## $ laps            <dbl> 58, 58, 58, 58, 0, 17, 58, 55, 55, 58, 24, 45, 58, 58,…
    ## $ time            <chr> "\\N", "+7.085", "+5.722", "+4.879", "\\N", "\\N", "+6…
    ## $ milliseconds    <chr> "\\N", "5662869", "5661506", "5660663", "\\N", "\\N", …
    ## $ fastestLap      <chr> "39", "48", "48", "53", "\\N", "6", "50", "35", "36", …
    ## $ rank            <chr> "13", "5", "1", "9", "\\N", "18", "17", "7", "2", "6",…
    ## $ fastestLapTime  <chr> "1:29.020", "1:28.283", "1:27.706", "1:28.712", "\\N",…
    ## $ fastestLapSpeed <chr> "214.455", "216.245", "217.668", "215.199", "\\N", "21…
    ## $ statusId        <dbl> 2, 1, 1, 1, 4, 3, 1, 24, 4, 1, 20, 22, 1, 1, 11, 1, 4,…

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
