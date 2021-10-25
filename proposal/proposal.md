Project proposal
================
ECK

``` r
library(tidyverse)
library(broom)
```

*For instructions on what each section should include, please see the
[project page](https://idsed.digital/assessments/project/#proposal) on
the course website. Remove this text when completing your proposal*.

## 1. Introduction

The dataframes we are using are from the website **website here** and
has information on Formula 1 races. This includes variables such as the
drivers information, the races they participated in, the race results
and more.

## 2. Data

For this project, we will be using a combination of dataframes from the
Formula 1 dataset. This combined dataframe will give us the following:  
+ The drivers ID (*driverId*)  
+ The place they achieved in the race (*resultId*)  
+ **add more information here**

Here is a glimpse at the combined data frame we will be using. **(Change
the dataframe here to the combined one once goal is decided)**

    ## Rows: 853 Columns: 9

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (7): driverRef, number, code, forename, surname, nationality, url
    ## dbl  (1): driverId
    ## date (1): dob

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 853
    ## Columns: 9
    ## $ driverId    <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17,…
    ## $ driverRef   <chr> "hamilton", "heidfeld", "rosberg", "alonso", "kovalainen",…
    ## $ number      <chr> "44", "\\N", "6", "14", "\\N", "\\N", "\\N", "7", "88", "\…
    ## $ code        <chr> "HAM", "HEI", "ROS", "ALO", "KOV", "NAK", "BOU", "RAI", "K…
    ## $ forename    <chr> "Lewis", "Nick", "Nico", "Fernando", "Heikki", "Kazuki", "…
    ## $ surname     <chr> "Hamilton", "Heidfeld", "Rosberg", "Alonso", "Kovalainen",…
    ## $ dob         <date> 1985-01-07, 1977-05-10, 1985-06-27, 1981-07-29, 1981-10-1…
    ## $ nationality <chr> "British", "German", "German", "Spanish", "Finnish", "Japa…
    ## $ url         <chr> "http://en.wikipedia.org/wiki/Lewis_Hamilton", "http://en.…

## 3. Data analysis plan

The plan for this data analysis is to explore the question  
**“Question Here”**

We will do this by combining the dataframes **a, b, c…** and visualising
**x, y, z**.
