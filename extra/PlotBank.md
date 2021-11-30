Visualisations Used in Presentation
================

## Dataset

### Wins Pie Chart

![](PlotBank_files/figure-gfm/race-wins-by-constructor-1.png)<!-- -->

### Finishing Position by Constructor Distribution

![](PlotBank_files/figure-gfm/finishing-position-by-constructor-1.png)<!-- -->

## Speed

### Constructor’s Average Speeds

![](PlotBank_files/figure-gfm/constructor-average-speeds-1.png)<!-- -->

### Average Lap Time vs Finishing Position

![](PlotBank_files/figure-gfm/lap-time-vs-finishing-position-1.png)<!-- -->

## Qualifying

### Qualifying Position vs Finishing Position

![](PlotBank_files/figure-gfm/qualifying-vs-finishing-1.png)<!-- -->

## Qualifying vs Finishing - Top 5

![](PlotBank_files/figure-gfm/qualifying-vs-finishing-top-5-1.png)<!-- -->

### Qualifying vs Finishing - Rest

``` r
f1merged_hybrid %>%
  filter(!is.na(position) & grid > 5) %>%
  ggplot(aes(x = grid, y = position, color = constructorname == "Mercedes")) +
  geom_jitter() +
  geom_smooth(method = lm,
              formula = y ~ x,
              colour = "black") +
  labs(x = "Qualifying Position",
       y = "Race Finishing Position",
       title = "Qualifying Position vs. Finishing Position (Top 5 Qualifiers)",
       subtitle = "In the hybrid era (2014-2020)") +
  theme(legend.position = "none") +
  scale_color_manual(values = c("azure4","#00d2be")) +
  annotate(geom = "label", x = 7.5, y = 21, label = "Mercedes", 
           color = "#00d2be") +
  annotate(geom = "label", x = 7.1, y = 19.4, label = "Other", 
           color = "azure4") +
  scale_x_reverse() +
  scale_y_reverse()
```

![](PlotBank_files/figure-gfm/qualifying-vs-finishing-rest-1.png)<!-- -->

### Summary Statistics

    ## # A tibble: 5 × 3
    ##   constructorname race_wins percent
    ##   <chr>               <int>   <dbl>
    ## 1 AlphaTauri              1   0.725
    ## 2 Ferrari                17  12.3  
    ## 3 Mercedes              102  73.9  
    ## 4 Racing Point            1   0.725
    ## 5 Red Bull               17  12.3

    ## # A tibble: 5 × 3
    ##   constructorname pole_positions percent
    ##   <chr>                    <int>   <dbl>
    ## 1 Ferrari                     21  15.2  
    ## 2 Mercedes                   109  79.0  
    ## 3 Racing Point                 1   0.725
    ## 4 Red Bull                     6   4.35 
    ## 5 Williams                     1   0.725

## Reliability

### Retirements vs Points

![](PlotBank_files/figure-gfm/retirements-vs-points-1.png)<!-- -->

## Pit Stops

### Pit Stop Time vs Points per Season - skewed

![](PlotBank_files/figure-gfm/pit-stop-time-vs-points-per-season-skewed-1.png)<!-- -->

### Pit Stop Time vs Points per Season - red flags removed

![](PlotBank_files/figure-gfm/pit-stop-time-vs-points-per-season-red-flags-removed-1.png)<!-- -->
