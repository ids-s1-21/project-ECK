Visualisations Used in Presentation
================

``` r
library(tidyverse)
library(readr)
library(dplyr)
library(skimr)
library(here)

f1merged <- read_csv("/cloud/project/data/f1merged.csv")
f1merged_hybrid <- read_csv("/cloud/project/data/f1merged_hybrid.csv")

key_teams <- c("Ferrari", 
               "McLaren",
               "Mercedes",
               "Red Bull",
               "Williams")

key_team_colours <- c("Mercedes" = "#00d2be",
                  "Red Bull" = "#0600ef",
                  "Ferrari" = "#dc0000",
                  "Racing Point" = "#F596C8",
                  "Force India" = "#f596c8",
                  "AlphaTauri" = "#ffffff",
                  "McLaren" = "#ff8700",
                  "Renault" = "#fff500",
                  "Williams" = "#0082fa",
                  "Toro Rosso" = "#469BFF",
                  "Lotus F1" = "#000000",
                  "Alfa Romeo" = "#960000",
                  "Sauber" = "#960000",
                  "Haas F1 Team" = "#787878")

key_team_colours_wins <- c("AlphaTauri" = "grey",
                           "Ferrari" = "#dc0000",
                           "Mercedes" = "#00d2be",
                           "Racing Point" = "#F596C8",
                           "Red Bull" = "#0600ef")
```

## Dataset

### Wins Pie Chart

![](PlotBank_files/figure-gfm/race-wins-by-constructor-1.png)<!-- -->

### Finishing Position by Constructor Distribution

    ## Warning: Removed 199 rows containing non-finite values (stat_boxplot).

![](PlotBank_files/figure-gfm/finishing-position-by-constructor-1.png)<!-- -->
