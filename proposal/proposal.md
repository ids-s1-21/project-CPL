Project proposal
================
CPL

``` r
library(tidyverse)
library(broom)
olympics <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-07-27/olympics.csv')
```

*For instructions on what each section should include, please see the
[project page](https://idsed.digital/assessments/project/#proposal) on
the course website. Remove this text when completing your proposal*.

## 1. Introduction

We got this dataset from Tidytuesday, and it was collected by
JThomasmock from www.sports-reference.com.

Each case is the athletes, and the variables are id, name, sex, age,
height, weight, team, noc, games, year.

General research question: 1. What is the correlation between the height
of the athletes and the medals, if there is any?

2.  Are younger athletes more likely to have a better performance than
    older athletes?

3.  Which team tends to perform better in Winter Olympics than Summer
    Olympics?

4.  Is the percentage of females attending the Olympics increasing over
    years?

5.Does the athletes from the host country tends to behave better by
gaining more medals?

## 2. Data

``` r
glimpse(olympics)
```

    ## Rows: 271,116
    ## Columns: 15
    ## $ id     <dbl> 1, 2, 3, 4, 5, 5, 5, 5, 5, 5, 6, 6, 6, 6, 6, 6, 6, 6, 7, 7, 7, …
    ## $ name   <chr> "A Dijiang", "A Lamusi", "Gunnar Nielsen Aaby", "Edgar Lindenau…
    ## $ sex    <chr> "M", "M", "M", "M", "F", "F", "F", "F", "F", "F", "M", "M", "M"…
    ## $ age    <dbl> 24, 23, 24, 34, 21, 21, 25, 25, 27, 27, 31, 31, 31, 31, 33, 33,…
    ## $ height <dbl> 180, 170, NA, NA, 185, 185, 185, 185, 185, 185, 188, 188, 188, …
    ## $ weight <dbl> 80, 60, NA, NA, 82, 82, 82, 82, 82, 82, 75, 75, 75, 75, 75, 75,…
    ## $ team   <chr> "China", "China", "Denmark", "Denmark/Sweden", "Netherlands", "…
    ## $ noc    <chr> "CHN", "CHN", "DEN", "DEN", "NED", "NED", "NED", "NED", "NED", …
    ## $ games  <chr> "1992 Summer", "2012 Summer", "1920 Summer", "1900 Summer", "19…
    ## $ year   <dbl> 1992, 2012, 1920, 1900, 1988, 1988, 1992, 1992, 1994, 1994, 199…
    ## $ season <chr> "Summer", "Summer", "Summer", "Summer", "Winter", "Winter", "Wi…
    ## $ city   <chr> "Barcelona", "London", "Antwerpen", "Paris", "Calgary", "Calgar…
    ## $ sport  <chr> "Basketball", "Judo", "Football", "Tug-Of-War", "Speed Skating"…
    ## $ event  <chr> "Basketball Men's Basketball", "Judo Men's Extra-Lightweight", …
    ## $ medal  <chr> NA, NA, NA, "Gold", NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…

## 3. Data analysis plan

What is the correlation between the height of the athletes and the
medals, if there is any?

The outcome is the number of medals and the predictor is the height of
athletes. We will use scatter diagram and smooth line graph, then colour
it by medals to make a clear difference between gold, silver and bronze
medals. A linear line should be seen to support our hypothesized answer.

Are younger athletes more likely to have a better performance than older
athletes?

The x variable is the age and the y variable is the number of medals. A
bar plot or a line graph can be used. If the peak from the graph appears
to be at the younger age end, that means the younger athletes are more
likely to have a better performance than older athletes. So the position
of the peak is needed to support our hypothesized answer.

Which team tends to perform better in Winter Olympics than Summer
Olympics?

The x variable is the teams and the y variable is the ratio between the
medals the team received in Winter Olympics and the Summer Olympics. The
bar plot is going to be arranged from the highest ratio to the lowest
(ratio = medals in Winter Olympics/medals in Summer Olympics). So the
higher the bar means more medals that team earned in Winter Olympics
than Summer Olympics. This is needed to support our hypothesized answer.

Is the percentage of females attending the Olympics increasing over
years?

We choose the years as x variables and percentage of females as y
variable. A line graph can be plotted so if there is an ascending trend
on the plot that will support our hypothesized answer.

Does the athletes from the host country tends to behave better by
gaining more medals?

We will choose a number of years and change the host city names into
their countries name so that we can compare the data. We may use scatter
diagram to denote the number of the medals for the host countries and
other countries and then facet them to make the graph more tidy. An
anomalous point for that country in the year that country hosted on the
graph can support our hypothesized answer.
