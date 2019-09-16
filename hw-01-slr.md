HW 01 - Simple Linear Regression
================
Hannah Wang
2019-09-16

### Load packages & Data

``` r
library(tidyverse)
library(readr)
library(broom)
library(knitr)
```

``` r
bikeshare <- read_csv("data/bikeshare.csv")
```

## Part 1: Computations & Concepts

### Question 1

``` r
winter_data <- bikeshare %>%
  filter(season == 1) %>%
  mutate(temp_c = temp *41)
winter_data
```

    ## # A tibble: 181 x 17
    ##    instant dteday     season    yr  mnth holiday weekday workingday
    ##      <dbl> <date>      <dbl> <dbl> <dbl>   <dbl>   <dbl>      <dbl>
    ##  1       1 2011-01-01      1     0     1       0       6          0
    ##  2       2 2011-01-02      1     0     1       0       0          0
    ##  3       3 2011-01-03      1     0     1       0       1          1
    ##  4       4 2011-01-04      1     0     1       0       2          1
    ##  5       5 2011-01-05      1     0     1       0       3          1
    ##  6       6 2011-01-06      1     0     1       0       4          1
    ##  7       7 2011-01-07      1     0     1       0       5          1
    ##  8       8 2011-01-08      1     0     1       0       6          0
    ##  9       9 2011-01-09      1     0     1       0       0          0
    ## 10      10 2011-01-10      1     0     1       0       1          1
    ## # … with 171 more rows, and 9 more variables: weathersit <dbl>,
    ## #   temp <dbl>, atemp <dbl>, hum <dbl>, windspeed <dbl>, casual <dbl>,
    ## #   registered <dbl>, count <dbl>, temp_c <dbl>

### Question 2

``` r
winter_model <- lm(count ~ temp_c, data = winter_data)
tidy(winter_model, conf.int = TRUE, level = 0.95) %>%
     kable(digits = 3)
```

| term        |  estimate | std.error | statistic | p.value |  conf.low | conf.high |
| :---------- | --------: | --------: | --------: | ------: | --------: | --------: |
| (Intercept) | \-111.038 |   238.312 |   \-0.466 |   0.642 | \-581.301 |   359.225 |
| temp\_c     |   222.416 |    18.459 |    12.049 |   0.000 |   185.990 |   258.841 |

count = -111.038 + 222.416 \* temp\_c

### Question 3

We are 95% confident that the true slope of the linear relationship
between number of bike rentals in the winter and temperature is between
185.990 and 248.841.

### Question 4

The width of a 90% confidence interval would be smaller than the width
of the 95% confidence interval because we are now less confident that
the CI captures the true slope, thus giving us a narrower range of
numbers.

### Question 5

Based on the 95% confidence interval, there is a statistically
significant linear relationship between temperature and number of bike
rentals in the winter because the 95% confidence interval does not
include a slope of 0 (no linear relationship).

### Question 6

The test statistic is 12.049, indicating a p-value of 0.00. This means
that assuming the null hypothesis were true, there is a 0% chance of
getting a test statistic of 12.049.

### Question 7

No, my roommate is not correct. The p-value of 0 means that assuming the
null hypothesis were true, there is a 0% chance we would have gotten the
results as extreme or more extreme than the output we got. Therefore, we
can reject the null hypothesis that there is no linear relationship
between temperature and bike rental count in the winter, in favor of the
alternative hypothesis that there is a linear relationship between
temperature and bike rental count in the winter.

### Question 8

``` r
glance(winter_model, winter_data)$r.squared
```

    ## [1] 0.4478316

The R-squared value shows that temperature explains 44.78% of the
variation in number of bikes rented in the winter.

## Part 2: Data Analysis

### Question 9

(Add code and narrative as needed.)

### Overall (Do not delete\!)

You do not need to write anything for this question. We will check the
following as part of your lab grade:

  - 5 pt: Documents neatly organized (.Rmd and .md files)
  - 3 pt: Narrative in full sentences and neatly organized
  - 2 pt: Regular and informative commit messages
