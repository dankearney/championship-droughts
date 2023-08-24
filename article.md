The Statistics of Championship Droughts

The Boston Red Sox went 86 years without a World Series. The Chicago Cubs went over a century. Even today, there are teams with preposterously long championship droughts.

I got curious: what is the probability of such a drought? This question turned out to be more interesting than I expected!

A few assumptions to simplify things: let's assume that a champion is picked randomly from the set of teams playing each year. This is a wild oversimplification, but, whatever. The second assumption is that I'm just going to assume that the same X teams have been in the league for the same amount of time. This isn't true either -- leagues grow and shrink, teams change -- but it simplifies the math as well. 

Okay, so on to the statistics. 

Let's ask a simple question. In the span of 86 years, what is the probability that a specific team out of the 30 in baseball -- let's call them the Boston Braves -- doesn't win a championship in 86 years?

This one is actually pretty easy: in year 1, there are 29 other teams that can win, so the probability of the Braves not winning is 29/30. In year 2, again, 29 teams can win, so the probability of them losing twice is (29/30)*(29/30). As independent events, the probability of the Braves not winning 86 times in a row is (29/30)^86, or about 5%. 

Now it gets really interesting when you ask the broader question: what is the probability that not every team wins a World Series in 86 years? 

On the surface, this is the same question: for an individual team, there is a 5% chance of not winning. So, expanding this out to any team is just 5% * 30 teams, right? Obviously this doesn't work -- it gives 150%! Why doesn't this work? Well, if the Boston Braves don't win 5% of the time, in some of those runs, another team might also not win. If we simply add the probabilities, we're double-counting the cases where multiple teams don't win.

To account for this, we need to apply the inclusion-exclusion principle. But this is just a logical thing we can talk through.

