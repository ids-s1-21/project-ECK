What makes a successful Formula One team?
================
by ECK

## Summary

Our project is to see what can help a Formula One driver perform better?
Specifically, we are looking at the Mercedes-AMG Petronas team in the
hybrid era (2014-2020) and investigate possible reasons for their
success.

To answer the question “What makes a successful Formula One team?”, we
want to see what data we have could impact a drivers performance. Since
our data is actually a combination of multiple datasets, we combined the
datasets *results, races, drivers* and *constructors* and focused only
on entries in the hybrid era (2014-present excluding 2021 since the 2021
races are ongoing at the time of this analysis). This resulting dataset
was called *f1merged_hybrid*.

Firstly, we wanted to investigate the performance of the Mercedes team.
We looked at the total number of wins of five key teams - AlphaTauri,
Ferrari, Mercedes, Racing Point and Red Bull. Our bar chart shows
Mercedes has an impressive amount of wins when compared to the other key
teams. But why is this?

We thought it could possibly be due to Mercedes having more drivers
leading to a misleading result. However, the merged dataset we are
working with has the same amount of drivers for each key team.

Could this be due to Mercedes being faster than the other constructors?
We investigated the median speeds of each key team, and found that
although Mercedes has a slightly lower mean lap time than the other
teams, it isn’t a significant enough difference to explain their massive
amount of wins.

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
