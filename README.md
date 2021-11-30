What makes a successful Formula One team?
================
by ECK

## Summary

### Introduction:

Formula One, or F1, is the highest class of single-seater racing and one
of the most prestigious racing series around the world. Each season,
around 10 constructors (also referred to as “teams”) build a car to
strict regulations and race them at more than 20 circuits across the
globe. A constructor fields two drivers and earns points towards two
separate championships; one for the driver and one for the constructor
who score the most points over a season. With our project we wanted to
investigate the factors that make a successful F1 team. Is outright
speed the only metric that matters? Or do small gains made in pit stop
times or reliability make all the difference?

### Dataset:

To answer the question “What makes a successful Formula One team?”, we
wanted to analyse how several predictor variables from our data set
impacted a team’s performance. Since our data is actually a combination
of multiple data sets, we combined the data sets *results, races,
drivers* and *constructors* and focused only on entries in the hybrid
era (2014-2020 excluding the 2021 season which is ongoing at the time of
this analysis). This resulting data set was called *f1merged_hybrid*. In
picking out a successful Formula One team from recent years there is one
obvious candidate.

![](README_files/figure-gfm/wins-bar-chart-1.png)<!-- -->

Mercedes-AMG Petronas F1 team have won the Drivers’ and Constructors’
championships 7 years running, with a near unprecedented level of
dominance. We looked at Mercedes specifically, as well as a comparison
group containing 4 other teams that competed against them during this
same time frame.

### Speed:

Could the answer to our question simply be that Mercedes are outright
faster than their competitors? We investigated the average lap time of
each key team and found that Mercedes has only a slight advantage in
median lap time over the likes of Ferrari and Red Bull. Looking purely
at median lap time, we would expect Ferrari and Red Bull to have
similarly successful records to Mercedes over the same period, but we
know this isn’t true. Do tiny margins in terms of speed make a
significant difference in Formula One? We investigated whether those
fractions of a second could be the determining factor by plotting
average lap time against finishing position and plotting a line of best
fit. Our visualisation found very little correlation between a driver’s
average lap time during a race and their finishing position (shown by an
almost flat regression line). Thus, Mercedes’ overwhelming number of
race wins is unlikely to be explained by a slightly higher pace *during
the race*.

### Qualifying:

So what difference *does* a small advantage in speed make? We would
expect tiny advantages in pace to be most significant during the
qualifying sessions that set the starting grid for the race. Qualifying
positions are decided based purely on the fastest lap time each driver
can set during a given period of time, and are often separated by only
fractions of a second. As such we plotted qualifying position against
finishing position hypothesizing that a close correlation of the two
would suggest a strong qualifying session is vital for success in the
race. Further, we fit a linear regression model to predict finishing
position from starting grid position.

### Lucky Wins:

Is it possible that one particularly skilled Mercedes racer just happens
to get first place with the other Mercedes performing worse? This would
show a large number of Mercedes wins even though they would perform
worse overall as a team. We analysed this by plotting the finishing
positions of each key constructor. However, it shows that the vast
majority of Mercedes racers will finish in the top 5 with a median
finishing position of around 2. Red Bull and Ferrari both have a median
finishing position of around 4, and Williams and McLaren having a median
finishing position of around 10 (and a much wider distribution,
suggesting a less consistent finishing position).

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
