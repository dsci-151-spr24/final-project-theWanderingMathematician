Project proposal
================
Micaiah Balonek

``` r
library(tidyverse)
library(broom)
```

## 1. Introduction

## 2. Data

``` r
setwd("/cloud/project/data")
trainingset_v1d1_metadata <- read_csv("trainingset_v1d1_metadata.csv") %>%
  select(-c(8, 9, 14, 17, 18, 19, 20)) %>%
  mutate(phase = param_one_value, .keep = "unused")
```

    ## Rows: 7966 Columns: 28
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (11): ifo, search, channel, param_one_name, gravityspy_id, label, sample...
    ## dbl (17): event_time, peak_time, peak_time_ns, start_time, start_time_ns, du...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
glimpse(trainingset_v1d1_metadata)
```

    ## Rows: 7,966
    ## Columns: 21
    ## $ event_time     <dbl> 1134216193, 1129359782, 1127425469, 1132636755, 1132035…
    ## $ ifo            <chr> "L1", "L1", "L1", "L1", "L1", "H1", "L1", "L1", "L1", "…
    ## $ peak_time      <dbl> 1134216192, 1129359781, 1127425468, 1132636755, 1132035…
    ## $ peak_time_ns   <dbl> 931639909, 558593034, 976317882, 365233898, 197264909, …
    ## $ start_time     <dbl> 1134216192, 1129359781, 1127425468, 1132636754, 1132035…
    ## $ start_time_ns  <dbl> 832031011, 47851085, 960937023, 951172113, 933837890, 4…
    ## $ duration       <dbl> 0.18750, 0.94238, 0.04688, 0.82422, 2.00366, 0.38281, 0…
    ## $ event_id       <dbl> 21, 107, 218, 88, 16, 228, 78, 0, 92, 84, 10, 56, 59, 7…
    ## $ peak_frequency <dbl> 1337.6953, 654.7477, 1337.8275, 1182.9746, 1456.5114, 1…
    ## $ central_freq   <dbl> 1120.0432, 1823.0734, 2024.1775, 3981.7747, 3979.0269, …
    ## $ bandwidth      <dbl> 573.36395, 3426.57642, 3778.70190, 7492.71777, 7942.912…
    ## $ amplitude      <dbl> 1.19765e-22, 8.25585e-23, 9.76294e-22, 1.46212e-22, 4.0…
    ## $ snr            <dbl> 7.51139, 9.63013, 15.37104, 10.32116, 14.38016, 8.48089…
    ## $ gravityspy_id  <chr> "zmIdpucyOG", "zWFRqqDxwv", "zKCTakFVcf", "z14BdoiFZS",…
    ## $ label          <chr> "Whistle", "Whistle", "Whistle", "Whistle", "Whistle", …
    ## $ sample_type    <chr> "train", "test", "train", "validation", "validation", "…
    ## $ url1           <chr> "https://panoptes-uploads.zooniverse.org/production/sub…
    ## $ url2           <chr> "https://panoptes-uploads.zooniverse.org/production/sub…
    ## $ url3           <chr> "https://panoptes-uploads.zooniverse.org/production/sub…
    ## $ url4           <chr> "https://panoptes-uploads.zooniverse.org/production/sub…
    ## $ phase          <dbl> -2.72902, 1.10682, -0.83099, 0.76242, -0.31161, 1.56686…

``` r
trainingset_v1d1_metadata
```

    ## # A tibble: 7,966 × 21
    ##     event_time ifo    peak_time peak_time_ns start_time start_time_ns duration
    ##          <dbl> <chr>      <dbl>        <dbl>      <dbl>         <dbl>    <dbl>
    ##  1 1134216193. L1    1134216192    931639909 1134216192     832031011   0.188 
    ##  2 1129359782. L1    1129359781    558593034 1129359781      47851085   0.942 
    ##  3 1127425469. L1    1127425468    976317882 1127425468     960937023   0.0469
    ##  4 1132636755. L1    1132636755    365233898 1132636754     951172113   0.824 
    ##  5 1132035853. L1    1132035853    197264909 1132035852     933837890   2.00  
    ##  6 1163421592. H1    1163421591    621093034 1163421591     492187023   0.383 
    ##  7 1135086850. L1    1135086850    427246093 1135086850     310547113   0.703 
    ##  8 1136285263. L1    1136285262    929687023 1136285262        976085   1.62  
    ##  9 1132651217. L1    1132651216    955077886 1132651216             0   1.25  
    ## 10 1132637477. L1    1132637476    677733898 1132637476     342772960   0.743 
    ## # ℹ 7,956 more rows
    ## # ℹ 14 more variables: event_id <dbl>, peak_frequency <dbl>,
    ## #   central_freq <dbl>, bandwidth <dbl>, amplitude <dbl>, snr <dbl>,
    ## #   gravityspy_id <chr>, label <chr>, sample_type <chr>, url1 <chr>,
    ## #   url2 <chr>, url3 <chr>, url4 <chr>, phase <dbl>

## 3. Data analysis plan
