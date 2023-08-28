# The Statistics of Championship Droughts

## Summary
In this article, I explore the probability that, after 86 idealized, random baseball seasons, there are still baseball teams that haven't won the World Series.

## Background

The Boston Red Sox went 86 years without winning baseball's World Series. The Chicago Cubs went over a century. Even today, there are teams with painfully long championship droughts.

I got curious: what is the probability of such a drought? This question turned out to be more interesting than I expected!

A few ways to simplify things: let's assume that a champion is picked randomly from the set of teams playing each year. The second assumption is that I'm just going to assume that the same X teams have been in the league for the same amount of time. This isn't true either -- leagues grow and shrink, teams change -- but it simplifies the math as well. 

Okay, so on to the statistics. 

## The statistics

The question at hand asks what the probability is that 86 years go by and there is a team (or multiple) in a championship drought? 

It's simple enough to answer a more specific question, like a specific team having a drought, or exactly one team having a drought. The main challenge is that in some of the cases where one team has a drought, another team might _also_ have a drought. If we take the naive route and simply add the ways each team individually could be in a drought, we're double-counting the overlapping cases where multiple teams have droughts at the same time. So, we need to remove those overlaps.

The number of possibilities where there's at least one drought is:

$N_{droughts} = N_{1 \hspace{.25em} drought} - N_{overlaps}$

We can compute the overlapping scenarios one step at a time. First, we can compute all the ways that exactly 2 teams have droughts and add those together, and we're left with another overlap, which consists of all the times there are 3+ teams with droughts. 

$N_{droughts} = N_{1 \hspace{.25em} drought} - (N_{2 \hspace{.25em} droughts} - N_{overlaps})$

Rinse and repeat -- compute the number of ways there are three losers, then subtract the overlap..

$N_{droughts} = N_{1 \hspace{.25em} drought} - (N_{2 \hspace{.25em} droughts} - (N_{3 \hspace{.25em} droughts} - N_{overlaps}))$

This goes on until we hit bottom. There are exactly 30 ways we can have 29 teams with droughts (each team wins 86 times straight!). And there are 0 ways that all 30 teams can be in a drought (someone has to win). 

Now, what is $N_{i \hspace{.25em} droughts}$? It is the number of ways exactly $i$ have a drought. There are two parts to this. First, we need to pick our teams. There are ${30 \choose i}$ ways to combine 30 teams into $i$ groups, and once we've selected them, each combination can then have $(30-i)^{86}$ ways that all the other teams can win. As an example, if $i=2$, there ${30 \choose 2} * (28^{86})$ ways. We can write this out as a neat little summation. Note that the sign alternates due to the nested subtractions:

$N = \Sigma_{i=1}^{30} {-1}^{i+1}{30 \choose i}(30-i)^{86}$

Then converting to a probability by dividing by the total number of possible outcomes, we can compute the answer:

$P = \frac{1}{30^{86}} \Sigma_{i=1}^{30} {-1}^{i+1}{30 \choose i}(30-i)^{86} = .839775$

## Verifying with Python

This is pretty easy to verify with code! The following simulates an 86-year run of baseball teams by making a random array of "winners" which are just numbers from 0 to 29. 

```
import random

def simulateNSeasons(nTeams, nYears):
    return [random.randrange(0, nTeams) for year in range(nYears)]
    
def runNTrials(nTrials, nTeams, nYears):
    allWinCount = 0
    for i in range(nTrials):
        winners = simulateNSeasons(nTeams, nYears)
        if len(set(winners)) == nTeams:
            allWinCount += 1
        
    notAllWinPct = 100.0 * (1.0 - allWinCount / nTrials)
    print("%i teams playing for %i years\n%.2f%% of seasons didn't have every team win over %i trials"%(nTeams, nYears, notAllWinPct, nTrials)) 
    
nTeams = 30
nYears = 86
nTrials = 10000

runNTrials(nTrials, nTeams, nYears)
```

This prints

```
30 teams playing for 86 years
83.89% of seasons didn't have every team win over 10000 trials
```

Looks like the math works! 

## Future work

Some future work might be to make this a little more realistic. For example baseball had only 16 teams for a long while; every year is not independent, as good teams tend to stay good and bad teams tend to stay bad, at least with some dependence year to year. Still this was an interesting exercise. 
