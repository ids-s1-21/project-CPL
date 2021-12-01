Olympics analysis
================
by CPL

## Summary (Write up)

The modern Olympics are leading international sporting with thousands of
athletes from more than 200 nations participating. The Olympic Games are
normally held every four years, alternating between the Summer and
Winter Olympics. So our group decided to choose a data set from
`TidyTuesday` related to the Olympic Games from previous years. The name
of the data is “The Olympics”, containing 15 different variables with
the name, age, the height of the athletes, the medals they have won, and
the year the Olympics take place.

The general research question is, “Are younger athletes more likely to
have a better performance than older athletes?”. Our hypothesised answer
is yes, so we think younger athletes are more likely to perform better
than older athletes. We are going to answer this question using a series
of related questions.

We started by plotting the number of athletes who won the medals per age
to verify our hypothesis. So we can see that there is a peak at the age
of 23, which means around 2.7 thousand athletes at the age of 23 have
won medals from 1896 to 2016.

Then, we have made a boxplot of the age range of the athletes for all 66
sports in the Olympic Games. Using a boxplot is because we can see the
median, the interquartile range, and the outliers of the age in each
sport. The Rhythmic Gymnastics stands out immediately because it has the
lowest median than the others. At the same time, it is also the only
sport with a median lower than the age of 20. To make the plot easier to
visualise, we have selected the top 12 most frequently occurring sports.
Looking at the median of these sports, it is not hard to conclude that
the median ages are all close to 25 years old. This observation has
explained why there is a peak around the age of 23.

However, these plots do not give enough information, so we plotted
another graph showing the probability of winning a medal per age. The
peak at the age of 27 on this graph is similar to the peak in the first
plot, and the likelihood of winning a medal decreases significantly
after the age of 30 in both of these plots. Up to this point, maybe we
can conclude that younger athletes are more likely to have better
performance than older athletes, but the two spikes at the age of 46 and
52 made us nervous. Therefore we need more evidence to support our
hypothesis.

We have enlarged both of the plots and only show the age range between
44 and 55, and surprisingly, there are two spikes in the number of
medals plot as well. So what causes these two spikes? To find it out, we
filtered the age for both spikes. For the age of 46, we selected a range
from 44 to 48; for the age of 52, we chose a range between 50 and 54. So
the two tibbles are the results of the filter function we used.
Equestrianism, or we can call it Horse Riding, always appear to be the
first on the ranking, followed by sailing and shooting. Is there any
similarity between these three sports? To visualise this, we have
specifically made three boxplots for these three sports. The median ages
of Sailing and Shooting are close to 30, and Equestrianism is almost 35.
Looking at the boxplot of all sports again, it is not hard to tell that
these three sports have very large interquartile ranges. Many athletes
with age over 50 were still winning medals in these three sports.
Equestrianism’s lower quartile is almost the same as the median of
Sailing and Shooting, and its upper quartile range is over the age of
40. Now we have found out why there are spikes at the age of 48 and 52,
so we can conclude our general research question.

## Presentation

Our presentation can be found [here](presentation/presentation.html).

## Data

There are 271,116 observations and 15 variables.

## References

The data fram was found at \<www.sports-reference.com> , which is from
<https://github.com/rfordatascience/tidytuesday/blob/master/data/2021/2021-07-27/readme.md>.
