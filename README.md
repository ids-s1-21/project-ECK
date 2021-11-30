What makes a successful Formula One team?
================
by ECK

## Summary

#### Introduction

Formula One, or F1, is the highest class of single-seater racing and one
of the most prestigious racing series around the world.

Each season, around 10 constructors (or “teams”) build a car to strict
regulations and race them at more than 20 circuits across the globe. A
constructor fields two drivers and earns points towards two separate
championships; one for the driver and one for the constructor who score
the most points over a season.

We wanted to investigate the factors that make a successful F1 team - is
speed the only metric that matters? Or do small gains made in pit stop
times or reliability make all the difference?

#### Dataset

To answer this question, we wanted to analyse how several predictor
variables from our data set impacted a team’s performance. Since our
data is actually a combination of multiple data sets, we combined the
data sets *results, races, drivers* and *constructors* and focused only
on entries in the hybrid era (2014-2020 excluding the 2021 season which
is ongoing at the time of this analysis). This resulting data set was
called *f1merged_hybrid*.

In picking out a successful Formula One team from recent years there is
one obvious candidate.

![](README_files/figure-gfm/wins-bar-chart-1.png)<!-- -->

Mercedes-AMG Petronas F1 team have won the Drivers’ and Constructors’
championships 7 years running, with a near unprecedented level of
dominance. We looked at Mercedes specifically, as well as a comparison
group containing 4 other teams that competed against them during this
same time frame.

We can see this isn’t just one good Mercedes driver - plotting the
constructors against their finishing positions, we can see that Mercedes
will almost always place in the top 5. So, what is it that makes
Mercedes such a dominant team?

#### Speed

Could the answer to our question simply be that Mercedes are outright
faster than their competitors? We investigated the average lap time of
each key team and found that Mercedes has only a slight advantage in
median lap time over the likes of Ferrari and Red Bull. If speed was the
deciding factor in races, Ferrari and Red Bull would be near the success
of Mercedes.

Does this tiny speed advantage make a significant difference in Formula
One? We investigated this by plotting average lap time against finishing
position. We found little correlation between a driver’s average speed
and their finishing position (shown by an almost flat regression line).
Thus, Mercedes’ success is unlikely to be explained by a slightly higher
speed *during the race*.

#### Qualifying

So what difference *does* a small advantage in speed make? We would
expect tiny advantages in pace to be most significant during the
qualifying sessions that set the starting grid for the race, decided
purely on the fastest lap time each driver can set in a qualifying race.

After plotting qualifying position against finishing position, our model
showed a strong correlation between the two, suggesting a good
qualifying session is necessary to perform well. However, the plot
seemed to show particularly heavy clustering near the front of the
field. To investigate this, we split the data for drivers qualifying in
the top 5 from the rest of the field, and modeled each separately.

As suspected, there was a stronger relationship between qualifying
position and finishing position for the drivers qualifying in the top 5.
In other words, if a driver qualifies near the front, they are likely to
stay there. This could be due to less opportunity for collisions
(particularly at the start) and possibly less time stuck behind another
racer.

Summary statistics show that Mercedes took pole position more than 78%
of the time in the hybrid era. Our qualifying model would predict them
to have many podiums (top 3 finish) and wins based on this alone, which
lines up with our previous findings.

#### Reliability

We identified mechanical reliability as a possible predictor of success.
We plotted and modeled retirements per season\* against points per
season for each of our key teams and found a strong linear relationship
between the two, if a little skewed by the teams in our comparison
group. Teams with fewer retirements in a season would be expected to
score far more points than those who frequently failed to finish.

\**Retirements per season used here as an imperfect proxy for mechanical
reliability, types of retirement are not easily differentiated in our
data set.*

#### Pit Stops

Similarly, we hypothesized that a team with quicker average pit stop
times would perform better - a slow stop can often be the difference
between gaining or losing a place on track. Plotting and modelling this,
we found a strong linear relationship between median pit stop time and
points scored per season. Despite our intercept not making sense in
practice and our slope being slightly skewed by our comparison group, it
predicts a team would score 230 fewer points in a season for each second
they add to their median stop time.

We combined our two models predicting total points per season - this
combined model had an adjusted R^2 value of 0.397, suggesting that
around 40% of the variability in points per season can be explained by
this model.

#### Conclusion

Our analysis allows us to go some way towards answering our question -
“What makes a successful F1 team?”

Speed is certainly important - to see strong results a team needs a car
capable of qualifying consistently near the front of the grid. However,
for a team to achieve the impressive results that Mercedes has had in
the hybrid era, they need more than just a fast car - fast and
consistent pit stops as well as the best reliability on the grid have
helped Mercedes go from a good team to one of the all time greats.

#### Limitations

We were not able to separate mechanical retirements from other
retirements in our analysis, so used retirements for any reason as a
proxy.

As comparing driver skill between teams is extremely difficult
(separating the car from the driver is almost impossible) and comparing
between teammates would not help to answer our question, we have not
included individual driver skill in our analysis. Driver skill
definitely plays some part in a team’s success, but including it would
go beyond the scope of this project.

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
