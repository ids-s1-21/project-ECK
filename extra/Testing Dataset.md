---
title: "Testing Dataset"
output: html_document
---

```{r libraries}
library(tidyverse)
library(readr)
library(dplyr)
library(skimr)
library(here)
```


```{r}
status <- read_csv(here("data/status.csv"))
results <- read_csv(here("data/results.csv"))
constructors <- read_csv(here("data/constructors.csv"))
drivers <- read_csv(here("data/drivers.csv"))
races <- read_csv(here("data/races.csv"))

res_con <- inner_join(constructors %>% select(-url), 
                     results)
colnames(res_con) [colnames(res_con) %in% c("name", "nationality") ] <- 
  c("constructorname", "constructornat")


res_con_driv <- inner_join(drivers %>% select(driverId, driverRef, surname),
                           res_con)
f1merged <- inner_join(races %>% select(raceId, year, round, name, date),
                       res_con_driv)

colnames(f1merged) [colnames(f1merged) == "name"] <- "racename"

write_csv(f1merged, "/cloud/project/data/f1merged.csv")
```

```{r hybrid_era}
hybrid_era <- (2014:2020)
```





```{r}
f1merged <- read_csv("/cloud/project/data/f1merged.csv", 
    na = "\\N")

write_csv(f1merged, "/cloud/project/data/f1merged.csv")

f1merged_hybrid <- f1merged %>%
  filter(year %in% hybrid_era)

write_csv(f1merged_hybrid, "/cloud/project/data/f1merged_hybrid.csv")
```




