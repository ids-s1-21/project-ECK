Project proposal
================
ECK

``` r
library(tidyverse)
library(broom)
```

## 1. Introduction

We will be looking at the question **“What makes a successful Formula
One (F1) team?”**. In particular, we will look at Mercedes-AMG Petronas
F1 Team, and their success in the hybrid era (2014-2020).

The data we are using comes from the Ergast Developer API
(**<http://ergast.com/mrd/>**). It provides data for the Formula One
racing series from 1950 to present. The data is collected from official
race classifications released by the FIA, Formula One’s governing body.

Much of our analysis will focus on the *results* dataframe. Each
observation in this dataframe represents the result of one driver at one
race. The variables are:

-   Result ID  
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
the *results* frame, and separately.

These will include the *qualifying* data frame, with variables for race,
driver, constructor & and position, as well as lap time.

Similarly we will use the *pit\_stops* data frame, with variables for
race, driver, stop number, lap number, time, duration, and duration in
milliseconds.

We will also use the *drivers* and *constructors* dataframes to link
driver names to their corresponding ID number.

## 2. Data

For this project, we will be using a combination of dataframes from the
Formula One dataset. This combined dataframe will give us the variables
referenced above in the **Introduction** section.

Here is a glimpse at one of the data frames we will be using called
*results*.

    ## Rows: 25280 Columns: 18

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (8): position, positionText, time, milliseconds, fastestLap, rank, fast...
    ## dbl (10): resultId, raceId, driverId, constructorId, number, grid, positionO...

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 25,280
    ## Columns: 18
    ## $ resultId        <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16,…
    ## $ raceId          <dbl> 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18…
    ## $ driverId        <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16,…
    ## $ constructorId   <dbl> 1, 2, 3, 4, 1, 3, 5, 6, 2, 7, 8, 4, 6, 9, 7, 10, 9, 11…
    ## $ number          <dbl> 22, 3, 7, 5, 23, 8, 14, 1, 4, 12, 18, 6, 2, 9, 11, 20,…
    ## $ grid            <dbl> 1, 5, 7, 11, 3, 13, 17, 15, 2, 18, 19, 20, 4, 8, 6, 22…
    ## $ position        <chr> "1", "2", "3", "4", "5", "6", "7", "8", "\\N", "\\N", …
    ## $ positionText    <chr> "1", "2", "3", "4", "5", "6", "7", "8", "R", "R", "R",…
    ## $ positionOrder   <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16,…
    ## $ points          <dbl> 10, 8, 6, 5, 4, 3, 2, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
    ## $ laps            <dbl> 58, 58, 58, 58, 58, 57, 55, 53, 47, 43, 32, 30, 29, 25…
    ## $ time            <chr> "1:34:50.616", "+5.478", "+8.163", "+17.181", "+18.014…
    ## $ milliseconds    <chr> "5690616", "5696094", "5698779", "5707797", "5708630",…
    ## $ fastestLap      <chr> "39", "41", "41", "58", "43", "50", "22", "20", "15", …
    ## $ rank            <chr> "2", "3", "5", "7", "1", "14", "12", "4", "9", "13", "…
    ## $ fastestLapTime  <chr> "1:27.452", "1:27.739", "1:28.090", "1:28.603", "1:27.…
    ## $ fastestLapSpeed <chr> "218.300", "217.586", "216.719", "215.464", "218.385",…
    ## $ statusId        <dbl> 1, 1, 1, 1, 1, 11, 5, 5, 4, 3, 7, 8, 5, 4, 10, 9, 4, 4…

## 3. Data analysis plan

The plan for this data analysis is to explore the question  
**“What makes a successful Formula One (F1) team?”**

We will do this by wrangling and visualising our data to see if there is
a relation between a Formula 1 team’s performance and factors such as
their pit stop data or their country of birth.
