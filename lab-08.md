Lab 08 - University of Edinburgh Art Collection
================
Lindsey Wilson
4/20/23

### Load packages and data

``` r
library(tidyverse) 
library(skimr)
library(robotstxt)
```

``` r
# Remove eval = FALSE or set it to TRUE once data is ready to be loaded
uoe_art <- read_csv("data/uoe-art.csv")
```

### Exercise 10

Lets go ahead and wrangle our data to separate the `title` variable into
`title` and `year`

``` r
uoe_art <- uoe_art %>%
  separate(title, into = c("title", "date"), sep = "\\(" ) %>%
  mutate(year = str_remove(date, "\\)") %>% as.numeric()) %>%
  select(title, artist, year, link)
```

    ## Warning: Expected 2 pieces. Additional pieces discarded in 39 rows [68, 211, 346, 658,
    ## 767, 782, 846, 891, 927, 979, 988, 1030, 1057, 1101, 1150, 1170, 1238, 1304,
    ## 1324, 1334, ...].

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 650 rows [2, 3, 5, 7, 13,
    ## 22, 34, 47, 49, 52, 55, 61, 66, 70, 94, 112, 119, 121, 125, 126, ...].

    ## Warning in str_remove(date, "\\)") %>% as.numeric(): NAs introduced by coercion

The reason we aren’t concerned about the error messages here is that
they all either indicate 1.) that there was extra information in the
string we aren’t concerned about capturing, or. 2.) that there were no
parentheses at all in the string so there wasn’t any date to capture.

### Exercise 12

Let’s skim our data:

``` r
skim(uoe_art)
```

|                                                  |         |
|:-------------------------------------------------|:--------|
| Name                                             | uoe_art |
| Number of rows                                   | 3017    |
| Number of columns                                | 4       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |         |
| Column type frequency:                           |         |
| character                                        | 3       |
| numeric                                          | 1       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |         |
| Group variables                                  | None    |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| title         |         1 |          1.00 |   0 |  95 |     8 |     1388 |          0 |
| artist        |       115 |          0.96 |   2 |  55 |     0 |     1116 |          0 |
| link          |         0 |          1.00 |  57 |  60 |     0 |     3017 |          0 |

**Variable type: numeric**

| skim_variable | n_missing | complete_rate |    mean |    sd |  p0 |  p25 |  p50 |  p75 | p100 | hist  |
|:--------------|----------:|--------------:|--------:|------:|----:|-----:|-----:|-----:|-----:|:------|
| year          |      1431 |          0.53 | 1964.38 | 55.47 |   2 | 1953 | 1962 | 1979 | 2020 | ▁▁▁▁▇ |

As we can see here, there are 115 pieces with artist info missing and
1431 pieces with year information missing.

### Exercise 13

``` r
ggplot(uoe_art, aes(x = year)) +
  geom_histogram(binwidth = 10)
```

    ## Warning: Removed 1431 rows containing non-finite values (`stat_bin()`).

![](lab-08_files/figure-gfm/histogram-1.png)<!-- -->

Add exercise headings as needed.
