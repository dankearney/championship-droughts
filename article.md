The Statistics of Championship Droughts

The Boston Red Sox went 86 years without a World Series. The Chicago Cubs went over a century. Even today, there are teams with preposterously long championship droughts.

I got curious: what is the probability of such a drought? This question turned out to be more interesting than I expected!

A few assumptions to simplify things: let's assume that a champion is picked randomly from the set of teams playing each year. This is a wild oversimplification, but, whatever. The second assumption is that I'm just going to assume that the same X teams have been in the league for the same amount of time. This isn't true either -- leagues grow and shrink, teams change -- but it simplifies the math as well. 

Okay, so on to the statistics. 

Let's ask a simple question. In the span of 86 years, what is the probability that a specific team out of the 30 in baseball -- let's call them the Boston Braves -- doesn't win a championship in 86 years?

This one is actually pretty easy: in year 1, there are 29 other teams that can win, so there are 29 ways that the Braves don't win. In year 2, again, 29 teams can win, so there are 29*29 ways. Over 86 years, there are $29^{86}$ ways. Out of a possible of $30^{86}$ total ways the 86 years can go, that gives about a 5% probability of a given season having the Braves not win the World Series. 

But what is the probability that 86 years go by and there's still a drought in the league at all? That is, one or more teams still hasn't won the World Series.  

On the surface, this is feels like a variation on the same question: for an individual team, there is a 5% chance of not winning. So, expanding this out to any team is just 5% * 30 teams, right? Obviously this doesn't work -- it gives 150%! Why doesn't this work? Well, if the Braves don't win in 5% of the outcomes, in some of those outcomes, another team might also not win. If we simply add the probabilities, we're double-counting the cases where multiple teams don't win at the same time.

To account for this, we need to apply the inclusion-exclusion principle. That sounds complicated, but it's just a logical thing we can talk through.

An easy thing to calculate is the number of ways an individual team doesn't win, which we already covered, it's just 29^86. Across 30 possible teams to choose, we have 29^86 * 30 ways that any team doesn't win a World Series. However, this over-counts all the ways that, for example, 2 teams simultaneously don't win a World Series. So, we need to subtract out all the ways N teams can simultaneously not win.

$ N = \frac{29}{30}^{86} - N_{simultaneous}$

How many ways can at least 2 teams both not win a World Series? For any given 2 teams, there are 28 other teams that can win in Year 1, 28 that can win in year 2, etc. So there are 28^86 ways the other 28 teams can win. And how many combinations of 2 teams are there? Pick one team out of 30, then pick a second out of the remaining 29, giving us 30*29. However, order doesn't matter, because saying " Team 3 doesn't win, and also Team 4 doesn't win" is the same as "Team 4 doesn't win, and also Team 3 doesn't win." So we have to divide by 2; this is the same as counting the number of handshakes in a group of people. A shorthand for this is the "choose" operator, giving the number of combinations. 

Okay, great. But -- we have the same problem here -- we've double-counted the times that 3 or more teams simultaneously don't win! Let's just update the formula...

$N = \frac{29}{30}^{86} - (\choose{30}{2}\frac{28}{30}^{86} - N_{triple and more over counts})$

The triple counting is the same logic: there are 30 choose 3 combinations of three teams that could all not win simultaneously; and there are 27^86 ways that each combination could play out. But, again, the triple counts also leaves out the times that four teams simultaneously lose, so we'll need to compute and subtract that out, too. So,

$N = \frac{29}{30}^{86} - (30 choose 2 * \frac{28}{30}^{86} - (30 choose 2 * \frac{28}{30}^{86}) - N_{quadruple and more over counts)$

A pattern emerges - and the nested subtractions alternate:

$N = N_{one} - (N_{two} - (N_{three} - (N_{four} - (N_{five} ... ))))$

$N = \choose{30}{1} * \frac{29}{30}^{86} - \choose{30}{2} * \frac{28}{30}^{86} + \choose{30}{3} * \frac{27}{30}^{86} - + \choose{30}{4} * \frac{26}{30}^{86} ...$


