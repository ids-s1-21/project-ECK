What makes a successful Formula One team?
================
by ECK

## Summary

Formula One is the highest class of single-seater racing and one of the
most prestigious racing series around the world.

Each season constructors (also referred to as “teams”) build cars to
strict regulations and race them at more than 20 circuits across the
globe. A team fields two drivers and earns points towards two separate
championships; one each for the driver and constructor who score the
most points over a season.

With our project we wanted to investigate the factors that make a
successful F1 team. Is outright speed the only metric that matters? Or
do small gains made in pit stop times or reliability make all the
difference?

In our analysis we combined the data sets *results, races, drivers* and
*constructors* and focused only on entries in the hybrid era (2014-2020
excluding the 2021 season which was ongoing at the time of our
analysis). This resulting data set was called *f1merged_hybrid*.

In picking out a successful Formula One team from recent years there is
one obvious candidate.

![](README_files/figure-gfm/wins-bar-chart-1.png)<!-- -->

Mercedes-AMG Petronas F1 team have won the Drivers’ and Constructors’
championships 7 years running, with a near unprecedented level of
dominance. We looked at Mercedes specifically, as well as a comparison
group containing 4 other teams that competed against them during the
same era.

**Lap Times:**

Could the answer to our question simply be that Mercedes are outright
faster than their competitors? We investigated the average lap time of
each key team and found that Mercedes has only a slight advantage in
mean lap time over the likes of Ferrari and Red Bull. Is this small
advantage in race pace a significant enough difference to explain the
massive discrepancy in race victories? Looking purely at average lap
time, it wouldn’t be unreasonable to expect Ferrari and Red Bull to have
similarly successful records over the same period.

We investigated whether slightly quicker lap times could be the
determining factor by plotting average lap time against finishing
position and fitting a linear regression model. Our visualisation found
very little correlation between a driver’s average lap time during a
race and their finishing position (shown by an almost flat regression
line). Thus, Mercedes’ overwhelming number of race wins is unlikely to
be explained purely be a slight advantage in pace *during the race*.

**Qualifying:**

So where *would* we expect a small advantage in speed to make the
biggest impact? Likely during the qualifying sessions that set the
starting grid for the race. Starting race positions are decided based on
the fastest lap time each driver can set during a dedicated qualifying
session and are often separated by only fractions of a second.

As such we plotted qualifying position against finishing position and
fit a linear model to predict one from the other. We hypothesized that a
close correlation of the two would suggest a strong starting position is
vital for success in the race. Our initial model showed a strong
correlation between the two, as expected, but the plot seemed to show
particularly heavy clustering near the front of the field. To
investigate this, we split the data for drivers qualifying in the top 5
from the rest of the field and modelled each separately.

As we suspected from our plot there was a stronger relationship between
qualifying position and finishing position for the drivers qualifying in
the top 5. If a driver qualifies near the front, they are likely to stay
there. There are many possible explanations for this; better pace,
lesser likelihood of being involved in any collisions (particularly at
the race start), likely less time spent closely following another car
(something that modern F1 aerodynamics make very difficult).

Summary statistics show that Mercedes took pole position (1st place in
qualifying) more than 78% of the time in the hybrid era. Our qualifying
model would predict them to have many wins based on this alone, but what
other factors might be at play here to take a team from strong results
to near unprecedented dominance?

**Reliability**

We identified mechanical reliability as another possible predictor of
success, any race in which a driver doesn’t finish is worth 0 points
after all. We plotted and modelled retirements per season against points
per season for each of our key teams and found a strong linear
relationship between the two, if a little skewed by the teams in our
comparison group (Our intercept assumes a team with 0 retirements would
score 515 points in a season, this is plausible for the top teams but
not for teams in the middle of the field or further back). Teams with
fewer retirements in a season would be expected to score far more points
than those who frequently failed to finish.

**Pit Stops**

Similarly, we hypothesized that a team with quicker average pit stop
times would score more points over a season. The timings of when a team
chooses to pit a driver are very tight, and a slow stop can often be the
difference between gaining or losing a place on track. Again, plotting
and modelling this (and after removing data errors) we found a strong
linear relationship between median pit stop time and points scored per
season. As above our intercept doesn’t make sense in practice and our
slope seems skewed by the teams in our comparison group but it predicts
a team would score 230 fewer points in a season for each second they add
to their median stop time.

As we now had two separate models predicting total points per season, we
wanted to combine them into a single model to try and explain more of
the variation in points scored per season. Our combined model had an
adjusted R^2 value of 0.397, suggesting that around 40% of the
variability in points per season can be explained by our model using
median pit stop time and retirements per season as predictors. We tried
to improve our model further by adding median qualifying position as a
third predictor variable - this did increase the adjusted R^2, but also
introduced a pattern in the predicted vs residuals plot that suggested a
linear model was not suitable.

**Conclusion**

Our analysis allows us to go some way towards answering our question -
“What makes a successful F1 team?”

Certainly, speed is necessary, to see strong results a team needs a car
capable of qualifying consistently near the front of the grid. But for a
team to achieve the consistently impressive results that Mercedes has
had in the hybrid era they need to excel in every area. Fast and
consistent pit stops as well as the best reliability on the grid have
also played a significant part in Mercedes’ unprecedented run of
success.

**Limitations**

We were not able to separate mechanical retirements from other
retirements in our analysis, so used retirements for any reason as an
imperfect proxy.

As comparing driver skill between teams is extremely difficult and
comparing between teammates would not help to answer our question, we
have not included individual driver skill in our analysis.

------------------------------------------------------------------------

## Presentation

Our presentation can be found [here](presentation/presentation.html).

## Data

The data we have used in this project is from the Ergast Developer API,
which has collected its data from the official race classifications
released by the FIA (Formula One’s governing body).

Ergast, A 2009, *Ergast Delevoper API*, data zip file, The Ergast
Developer API, retrieved 22nd October 2021, <http://ergast.com/mrd/>

## References

Ergast, A 2009, *Ergast Delevoper API*, data zip file, The Ergast
Developer API, retrieved 22nd October 2021, <http://ergast.com/mrd/>
