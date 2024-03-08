Project proposal
================
Micaiah Balonek

``` r
library(tidyverse)
library(broom)
```

## 1. Introduction

In this project, we are analysing data from the LIGO detectors;
specifically, we are looking at the waveforms corresponding to glitches
in these detectors, classified into categories by a machine learning
system trained on the responses of citizen scientists in the Gravity Spy
project. This dataset contains the metadata connected to each glitch,
along with the glitch class that it was classified into; each glitch can
be visualised on a spectrogram as a shape in the three-dimensional
time-amplitude-frequency space, which is what the machine learning
classifies it based on. The data includes four of these spectrograms for
each glitch, identical except for what length of time they represent, in
the format of the Gravity Spy project. The data therefore includes
variables such as the peak and central frequencies, the bandwidths,
phase, and the duration of these glitches, but also provides a few
measures of the strength of the glitch: not only the simple amplitude
value, but also the signal-to-noise ratio (SNR) of each signal and the
gravity spy ID number. Many columns were also provided which were
entirely filled with one value, which I have decided to leave out of the
descriptions, since they are of no consequence to the rest of the data.

Here we will be analysing the different classes of glitches according to
the different to attempt to see if we can find a combination of the
other parameters (bandwidth, peak and central frequencies, duration, and
snr) which can provide splits which approximate the machine learning’s
classification scheme.

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

## 3. Data analysis plan
