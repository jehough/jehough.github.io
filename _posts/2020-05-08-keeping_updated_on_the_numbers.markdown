---
layout: post
title:      "Keeping Updated on the Numbers"
date:       2020-05-09 00:31:03 +0000
permalink:  keeping_updated_on_the_numbers
---


Everyone is concerned about the COVID-19 these days, and rightfully so.  It has disrupted nearly every part of our lives and continues to haunt us after nearly 2 months of lockdowns and stay-at-home orders.  One of the things that I have noticed is that every news site has some kind of map that shows the coronavirus cases by state.  While these are interesting, as most of them are set up, they are not very helpful.

Several of the ones that I have seen have been a simple showing of positive cases in each state.  That is a good data point, but it doesn't really tell us much about how hard a state is hit by this virus.  If Florida and North Dakota have the same number of cases, that does not mean that they are hit the same.  The entire population of North Dakota is less than that of the single city of Jacksonville in Florida.  This means, in this hypothetical scenario, that North Dakota would be far more affected by the virus even though they have the same number of positive cases.

I set out to make myself a map that could help visualize this data in a more helpful way.  There are several good maps that can be used and mine is certainly not going to be the end all fix for maps.  I simply wanted something accessible that I could see the data in a form that was more helpful.  The map I created can be found [here](http://monkey-921.getforge.io/)

What I wanted in this map was to compare the number of positives and deaths to the population of each state.  Finding an API with the right information was surprisingly difficult.  It wasn't an issue of API's not being available, but rather an issue of too many API's avaiable.  I spent a good bit of time sorting through different API's till I found the data that I wanted.  I ended up going with the COVID tracking project by the Atlantic.

In order to get a good comparison, I set up graphics for raw positives, positives per 100K in population, raw number for deaths and number of deaths per 100K in population.  After I published the first version of the site, my wife (an ER Nurse) suggested I add testing data as well.  So, I added a visualization for number of tests administered per 100K in population.

Having this data shows that there are a few states that have a very serious COVID problem.  New York, Connecticut and New Jersey have all been hit very hard.  They are not the only ones, but their death rates are the highest by far.  I have heard some comments suggesting that this virus is a joke, or it's being way overblown by the media.  I would suggest we remember that not every state is the same.  In some states, it certainly feels this way as there hasn't been a great impact by the virus, and we should be thankful for that.  However, this clearly shows that some places have been hit very hard, and they need our help now, and likely will for months to come.
