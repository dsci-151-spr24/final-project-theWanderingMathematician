# data


## trainingset_v1d1_metadata
A 7,966 row by 21 column dataframe

###### (note: all times given in UTC)
- `event_time`: The time of the event
- `ifo`: The interferometer that the event was detected at; `H1` = Hanford, `L1` = Livingston
- `peak_time`: The time of the peak of the event up to the second mark
- `peak_time_ns`: The time of the peak of the event in nanoseconds
- `start_time`: The time of the start of the event
- `start_time_ns`: The time of the start of the event in nanoseconds
- `duration`: The duration of the event in seconds
- `event_id`: The ID of the event
- `peak_frequency`: The dominant frequency at the peak of the event.
- `central_freq`: The central frequency at the peak of the event
- `bandwidth`: The distance between the lowest-frequency and highest-frequency points of the event
- `amplitude`: The amplitude of the event
- `snr`: The signal-to-noise ratio of the event; a measurement of how loud the event is, defined as the strength of the signal over the strength of the background noise.
- `gravityspy_id`: The ID of the event on the Gravity Spy citizen science project, which can be used to access the metadata of the event on [the Gravity Spy tools page](https://gravityspytools.ciera.northwestern.edu/).
- `label`: The glitch class that the event was classified as.
- `sample_type`: The type of sample that the event was detected with
- `url1`: The URL of the image of the central 0.5 seconds of the event
- `url2`: The URL of the image of the central second of the event
- `url3`: The URL of the image of the central 2 seconds of the event
- `url4`: The URL of the image of the central 4 seconds of the event
- `phase`: The phase value of the waveform of the event

<br><br>

###### Data from:
###### Coughlin, S. (2018). Gravity Spy Training Set (v1.1.0) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.1486046
