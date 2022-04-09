
# Grabbing the flights data

> My cousin is getting married in Kansas City in May and I need to book
> flights from Baltimore to Kansas City. I want to decide which airline
> to pick, which weekday to depart, and what time of day to leave so
> that so that the I have the least chance of my plane being delayed.
> Which airline should I pick, which day of the week should I depart on,
> and around when during the day should I depart?

I’d like to grab data on flights from Baltimore to Kansas City to help
me decide which one to book. Since this flight is in May, to try to get
historically relevant data, I’ll grab data from May in last year (2021).

First loading the packages I’ll need,

``` r
# grab flight data from any year or airport
library(anyflights)

# general tools to work with data
library(tidyverse)
```

Now, querying the data,

``` r
bwi_flights <- 
  get_flights(
    station = "BWI",
    year = 2021,
    month = 5,
    dir = "source"
  )
```

Taking a glimpse at the data,

``` r
# take a look by column
glimpse(bwi_flights)
```

    ## Rows: 6,396
    ## Columns: 19
    ## $ year           <int> 2021, 2021, 2021, 2021, 2021, 2021, 2021, 2021, 2021, 2…
    ## $ month          <int> 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5…
    ## $ day            <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ dep_time       <int> 527, 533, 557, 608, 610, 611, 624, 627, 628, 633, 634, …
    ## $ sched_dep_time <int> 530, 535, 600, 610, 606, 615, 630, 625, 625, 635, 635, …
    ## $ dep_delay      <dbl> -3, -2, -3, -2, 4, -4, -6, 2, 3, -2, -1, -3, 5, -7, -4,…
    ## $ arr_time       <int> 750, 714, 722, 701, 733, 833, 901, 822, 814, 753, 844, …
    ## $ sched_arr_time <int> 806, 726, 729, 705, 749, 850, 915, 840, 825, 805, 915, …
    ## $ arr_delay      <dbl> -16, -12, -7, -4, -16, -17, -14, -18, -11, -12, -31, -1…
    ## $ carrier        <chr> "AA", "DL", "DL", "WN", "AA", "WN", "F9", "WN", "WN", "…
    ## $ flight         <int> 213, 396, 307, 366, 452, 391, 478, 382, 761, 367, 377, …
    ## $ tailnum        <chr> "N906NN", "N806DN", "N349NB", "N752SW", "N923AN", "N868…
    ## $ origin         <chr> "BWI", "BWI", "BWI", "BWI", "BWI", "BWI", "BWI", "BWI",…
    ## $ dest           <chr> "MIA", "ATL", "DTW", "BNA", "CLT", "RSW", "MIA", "LAS",…
    ## $ air_time       <dbl> 125, 84, 68, 89, 63, 127, 129, 278, 86, 66, 118, 99, 98…
    ## $ distance       <dbl> 946, 577, 409, 587, 361, 919, 946, 2106, 577, 369, 925,…
    ## $ hour           <dbl> 5, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 7, 7, 7, 7, 7, 7…
    ## $ minute         <dbl> 30, 35, 0, 10, 6, 15, 30, 25, 25, 35, 35, 50, 45, 0, 0,…
    ## $ time_hour      <dttm> 2021-05-01 05:00:00, 2021-05-01 05:00:00, 2021-05-01 0…

``` r
# take a look by rows
head(bwi_flights)
```

    ## # A tibble: 6 × 19
    ##    year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##   <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ## 1  2021     5     1      527            530        -3      750            806
    ## 2  2021     5     1      533            535        -2      714            726
    ## 3  2021     5     1      557            600        -3      722            729
    ## 4  2021     5     1      608            610        -2      701            705
    ## 5  2021     5     1      610            606         4      733            749
    ## 6  2021     5     1      611            615        -4      833            850
    ## # … with 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
    ## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
    ## #   hour <dbl>, minute <dbl>, time_hour <dttm>

Each row is a flight that left BWI (note: we don’t have cancelled ones),
and each column is some piece of information about that flights
departure: time, date, departure delay, destination, etc.
