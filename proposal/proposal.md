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

General research question:

1.  Are younger athletes more likely to have a better performance than
    older athletes?

2.Does the athletes from the host country tends to behave better by
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

Are younger athletes more likely to have a better performance than older
athletes?

``` r
population <- olympics %>%
  count(age)

medal_by_age <- olympics %>%
  na.omit(medal) %>%
  group_by(age) %>%
  mutate(n_medal = medal %in% c("Bronze", "Silver", "Gold")) %>%
  count(n_medal) %>%
  select(age, n) 

medal_by_age_2 <- medal_by_age %>%
  left_join(population, by = "age")

medal_by_age_2 %>%
  mutate(proportion = n.x/n.y) %>%
  ggplot(aes(x = age, y = proportion)) +
  geom_line()
```

![](proposal_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

Narrative: We think that the answer for the question is yes. The peak is
at about 27\~28 years old. The likelihood is gradually increasing from
young age, have a peak at 27\~27, and decreasing over age. But, the
interesting thing is that there are 2 bumps at about 42 years old and 53
years. We want to find out why if we can. We suppose there is the peak
at 27\~28 years old even though early twenties have better physical
performance because early twenties have less experience for the
Olympics, which is a big and making nervous competition, or have spent
their time for the sports less than the older twenties. Anyway, it is
generally true that the younger athletes are more likely to have a
better performance than older athletes.

Which team tends to perform better in Winter Olympics than Summer
Olympics?

``` r
total_medal_by_team <- olympics %>%
  group_by(team) %>%
  select(team, season, medal) %>%
  na.omit(medal) %>%
  mutate(n_medal = medal %in% c("Bronze", "Silver", "Gold")) %>%
  count(n_medal) %>%
  select(team, n)

winter_medal_by_team <- olympics %>%
  group_by(team) %>%
  select(team, season, medal) %>%
  filter(season == "Winter") %>%
  na.omit(medal) %>%
  mutate(n_medal = medal %in% c("Bronze", "Silver", "Gold")) %>%
  count(n_medal) %>%
  select(team, n)
  
winter_medal_by_team %>%
  left_join(total_medal_by_team, by = "team") %>%
  mutate(proportion = n.x/n.y) %>%
  arrange(desc(proportion)) %>%
  filter(n.y >=100) %>%
  rename(winter_medal = n.x,
         all_medal = n.y) %>%
  mutate(team = case_when(
    team == "United States-1" ~ "United States",
    TRUE ~ team
  ))
```

    ## # A tibble: 36 × 4
    ## # Groups:   team [35]
    ##    team           winter_medal all_medal proportion
    ##    <chr>                 <int>     <int>      <dbl>
    ##  1 United States            69       101      0.683
    ##  2 Austria                 244       413      0.591
    ##  3 Czech Republic           73       134      0.545
    ##  4 Norway                  443       910      0.487
    ##  5 Finland                 426       876      0.486
    ##  6 Canada                  575      1243      0.463
    ##  7 Czechoslovakia          158       486      0.325
    ##  8 Switzerland             183       588      0.311
    ##  9 Sweden                  428      1434      0.298
    ## 10 Russia                  216      1110      0.195
    ## # … with 26 more rows

Narrative: We think it would be more clear if we demonstrate the answer
as a table, so we did. We calculated the proportion by dividing the
number of medal each team got on winter by all the medal they got from
both Winter Olympics and Summer Olympics. As we can see from the table,
Untied States tends to perform better on Winter Olympics because they
have got 63 medals on winter out of 101. The proportion is 68.3% high.
