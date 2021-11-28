Merging Data Frames
================

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.5     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   2.0.0     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(readr)
library(dplyr)
library(skimr)
library(here)
```

    ## here() starts at /cloud/project

``` r
status <- read_csv(here("data/status.csv"))
results <- read_csv(here("data/results.csv"))
constructors <- read_csv(here("data/constructors.csv"))
drivers <- read_csv(here("data/drivers.csv"))
races <- read_csv(here("data/races.csv"))
```

``` r
res_con <- inner_join(constructors %>% select(-url), 
                     results)
```

    ## Joining, by = "constructorId"

``` r
colnames(res_con) [colnames(res_con) %in% c("name", "nationality") ] <- 
  c("constructorname", "constructornat")


res_con_driv <- inner_join(drivers %>% select(driverId, driverRef, surname),
                           res_con)
```

    ## Joining, by = "driverId"

``` r
f1merged <- inner_join(races %>% select(raceId, year, round, name, date),
                       res_con_driv)
```

    ## Joining, by = "raceId"

``` r
colnames(f1merged) [colnames(f1merged) == "name"] <- "racename"

write_csv(f1merged, "/cloud/project/data/f1merged.csv")
```

``` r
f1merged <- read_csv("/cloud/project/data/f1merged.csv", 
    na = "\\N")
```

    ## Rows: 25280 Columns: 27

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr   (9): racename, driverRef, surname, constructorRef, constructorname, co...
    ## dbl  (17): raceId, year, round, driverId, constructorId, resultId, number, g...
    ## date  (1): date

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
write_csv(f1merged, "/cloud/project/data/f1merged.csv")

f1merged_hybrid <- f1merged %>%
  filter(year %in% 2014:2020)

write_csv(f1merged_hybrid, "/cloud/project/data/f1merged_hybrid.csv")
```

``` r
stops <- read_csv(here("data/pit_stops.csv")) 

stops_drivers <- inner_join(drivers %>% select(driverId, driverRef, surname),
                           stops)
stops_merged <- inner_join(f1merged %>% select(-time, -milliseconds),
                           stops_drivers) %>%
  filter(year %in% 2014:2020)

write_csv(stops_merged, "/cloud/project/data/stops_merged.csv")
```
