What makes a successful Formula One team?
================
by ECK

## Summary

Formula One, or F1, is the highest class of single-seater racing and one
of the most prestigious racing series around the world.

Each season around 10 constructors (also referred to as “teams”) build a
car to strict regulations and race them at more than 20 circuits across
the globe. A constructor fields two drivers and earns points towards two
separate championships; one each for the driver and constructor who
score the most points over a season.

With our project we wanted to investigate the factors that make a
successful F1 team. Is outright speed the only metric that matters? Or
do small gains made in pit stop times or reliability make all the
difference?

In picking out a successful Formula One team from recent years there is
one obvious candidate.

![](README_files/figure-gfm/wins-bar-chart-1.png)<!-- -->

Mercedes-AMG Petronas F1 team have won the Drivers’ and Constructors’
championships 7 years running, with a near unprecedented level of
dominance. We looked at Mercedes specifically, as well as a comparison
group containing 4 other teams: Ferrari, McLaren, Red Bull and Williams.
These comparison teams were chosen because they had all competed in F1
across the entire period we looked at, so we could easily compare them
to Mercedes directly.

To answer the question “What makes a successful Formula One team?”, we
wanted to analyse how several predictor variables from our data set
impacted a team’s performance. Since our data is actually a combination
of multiple data sets, we combined the data sets *results, races,
drivers* and *constructors* and focused only on entries in the hybrid
era (2014-2020 excluding the 2021 season which is ongoing at the time of
this analysis). This resulting data set was called *f1merged_hybrid*.

Could this be due to Mercedes being faster than the other constructors?
We investigated the average lap time of each key team and found that
Mercedes has a slightly lower median lap time than the other teams by a
few seconds. However, this isn’t a significant enough difference to
explain their massive amount of wins - if it were, Ferrari and Red Bull
would have a similar amount of wins to Mercedes due to having similar
median lap times.

Could this simply be due to Mercedes being outright faster than their
competitors? We investigated the average lap time of each key team and
found that Mercedes has only a slight advantage in median lap time over
the likes of Ferrari and Red Bull. Is this small advantage in race pace
a significant enough difference to explain the massive discrepancy in
wins and pole positions? (1st place in qualifying) Looking purely at
median lap time, it wouldn’t be unreasonable to expect Ferrari and Red
Bull to have similarly successful records over the same period.

Do tiny margins in terms of speed make a significant difference in F1?
And what factors other than outright speed might play into a winning
season?

Write-up of your project and findings go here. Think of this as the text
of your presentation. The length should be roughly 5 minutes when read
out loud. Although pacing varies, a 5-minute speech is roughly 750
words. To use the word count addin, select the text you want to count
the words of (probably this is the Summary section of this document, go
to Addins, and select the `Word count` addin). This addin counts words
using two different algorithms, but the results should be similar and as
long as you’re in the ballpark of 750 words, you’re good! The addin will
ignore code chunks and only count the words in prose.

You can also load your data here and present any analysis results /
plots, but I strongly urge you to keep that to a minimum (maybe only the
most important graphic, if you have one you can choose). And make sure
to hide your code with `echo = FALSE` unless the point you are trying to
make is about the code itself. Your results with proper output and
graphics go in your presentation, this space is for a brief summary of
your project.

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
