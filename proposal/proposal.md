Project proposal
================
Micaiah Balonek

## 1. Introduction

In this project, we are analysing data from the LIGO detectors;
specifically, we are looking at the waveforms corresponding to glitches
in these detectors, classified into categories by a machine learning
system trained on the responses of citizen scientists in the Gravity Spy
project.

This dataset contains the metadata connected to each glitch, along with
the glitch class that it was classified into; each glitch can be
visualised on a spectrogram as a shape in the three-dimensional
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
The URLs will also not be necessary, unless we want to look at the
spectrograms for some reason (possibly as an example of a class, or a
test of some classification schema). As an example, this is how Gravity
Spy spectrograms appear: ![Example
spectrogram](https://panoptes-uploads.zooniverse.org/production/subject_location/da7f393e-729a-46c9-8dee-160a5851c419.png)

<sub><sup> Unlike most Gravity Spy subjects, this is not a glitch, but a
“chirp”, either a real gravitational wave or one simulated by the LIGO
staff. </sup></sub>

Here we will be analysing the different classes of glitches according to
the different to attempt to see if we can find a combination of the
other parameters (`bandwidth`, `peak` and `central` frequencies,
`duration`, and `snr`) which can provide splits which approximate the
machine learning’s classification scheme.

## 2. Data

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

Our predictor variables are `bandwidth`, `peak frequency`,
`central frequency`, `duration`, and `snr`, while our outcome variable
will be the grouping system of `label`; however, realistically, the
outcome will be merely the closest approximation found to the ML’s
classification system, as it would take more complex analysis processes
to truly replicate this classification scheme.

### Data summary

To start our preliminary analysis of the data, we plot how common each
of these glitches are compared to eachother in each interferometer:
![](proposal_files/figure-gfm/glitch-frequency-1.png)<!-- --> First of
all, we can see that several glitch classes are specific to each
interferometer (although some may just have few enough examples that
they don’t show up in this graph). Another interesting thing to see is
that Hanford generally has more glitches than Livingston, and that
Blips, Koi Fish, and Low-Frequency Bursts appear to be the glitches with
the most examples. To see whether this is accurate, we will now
calculate summary statistics for each glitch class. The following
summary statistics include the number of glitches of that class detected
in each interferometer (columns `n_H1` and `n_L1`) and the means of each
of the predictor variables for each class.

    ## # A tibble: 22 × 8
    ##    label             n_H1  n_L1    snr peak_freq central_freq duration bandwidth
    ##    <chr>            <dbl> <dbl>  <dbl>     <dbl>        <dbl>    <dbl>     <dbl>
    ##  1 1080Lines          327     1   10.2      1111         2961     0.85      4730
    ##  2 1400Ripples          0    81   10.9      1527         1846     0.15      1654
    ##  3 Air_Compressor      55     3    8.7        48          320     0.41       567
    ##  4 Blip              1453   368   22.8       199          839     0.27      1595
    ##  5 Chirp               28    32   13.6       141          264     0.29       461
    ##  6 Extremely_Loud     266   181 2416.        140         2673     8.17      5311
    ##  7 Helix                3   276    8.8       134          263     0.09       326
    ##  8 Koi_Fish           517   189  139.        157         1834     1.75      3629
    ##  9 Light_Modulation   511     1   34.6       105         2000     2.34      3966
    ## 10 Low_Frequency_B…   166   455   29.9        16         2611     2.91      5208
    ## 11 Low_Frequency_L…    79   368   23.1        12         2630     3.94      5243
    ## 12 No_Glitch           91    59    9.3       183         1601     1.95      2915
    ## 13 None_of_the_Abo…    51    30   45.3       170         1744     2.72      3436
    ## 14 Paired_Doves        27     0   33.4        41         1270     0.42      2505
    ## 15 Power_Line         273   176   11.3        62          733     0.75      1367
    ## 16 Repeating_Blips    230    33   29.2       200         1650     0.31      3214
    ## 17 Scattered_Light    385    58   16.4        30         2175     2.61      4319
    ## 18 Scratchy            90   247    8.6       153         1223     1.45      2269
    ## 19 Tomte               61    42   16.2        47          833     0.73      1622
    ## 20 Violin_Mode        141   271   13.4      1673         1742     0.29      2637
    ## 21 Wandering_Line      42     0   27.8       667         2127     6.05      3929
    ## 22 Whistle              2   297    9.5      1093         2690     0.59      4788

From this summary data, we can see that the Machine Learning system has
classed several glitches into categories from the “wrong” observeratory.
This can be explained in the following way: enough glitches happen that
even if a certain glitch type isn’t present in one interferometer, a
burst of noise can appear with a random shape that the ML couldn’t
classify well into the “correct” interferometer’s categories, and which
happens to look like a glitch from another category, and would get
classified into that; alternatively, since “None of the Above” is a
category, this implies that the training data (classified by citizen
scientists) is included in this dataset, and these mistakes were human
errors, already present in the training data. We can also see that Koi
Fish, one of the most prominent types of glitches, is also the loudest
standard class (other than Extremely Loud glitches, which are the
loudest by definition), while Scratchy, Helix, and Air Compressor
glitches are the quietest, even quieter on average than the ‘No glitch’
category.

### Preliminary Analysis

To begin our analysis of the data points themselves (other than just the
averages for each glitch class) we plot out `bandwidth` by `duration`,
with the colour of the points representing the label, to see how well we
can group glitch classes by the general dimensions of the signal:
![](proposal_files/figure-gfm/bandwidth-duration-plot-1.png)<!-- -->

This image is a bit hard to read, since the labels take up so much room,
and since there are so many data points on the graph; still, one can
tell that in the lower part of the distribution the glitch population is
dominated by the blue and purple colours of Koi Fish, Low-Frequency
Bursts, and Low-Frequency Lines, with a sudden stripe of green (and
assorted other colours) at the very bottom. Zooming in on the y-axis to
glitches with durations less than 5 seconds gives us the following plot:

![](proposal_files/figure-gfm/bandwidth-duration-plot-zoomed-1.png)<!-- -->
With this zoomed-in visualisation, we can see that the data has some
artefacts, causing the values to line up on a grid; ignoring this,
however, we notice the large cluster of green “Blip”-type glitches at
the bottom, especially prominent in the bottom-left corner, as well as
two major populations of 1080-Lines: one forming linear patterns in the
lower-right-hand corner of the distribution, and the other one being
around the left-hand side of the blip distribution. We also see a
population of either violin modes or wandering lines in the center of
the lower edge of the plot, its density peaking at bandwidths between
3000 and 4000. We also now see that there are many Koi Fish glitches
spread through the background distribution, which we mixed in with the
colour of the low-frequency bursts and lines in our earlier analysis.
The last notable point that stands out in this graph is the fact that
Koi fish and Low Frequency Bursts seem to dominate for most of the
chart, with assorted scattered-light glitches among them as well.

Meanwhile, if we instead plot peak frequency by duration (using the same
limit on duration), we get the following graph:

![](proposal_files/figure-gfm/peakFreq-duration-plot-1.png)<!-- -->

Here, we can clearly see spikes of 1080-Hz lines and 1400-Hz ripples at
their respective frequencies, as well as several spikes of violin modes
at frequencies just over 1000Hz, 1500Hz, and 2000Hz, among a background
composed mostly of Whistles. Moving into lower frequencies, we see a
cloud of Blips underneath another blob, mostly composed of Koi Fish.
There are several distributions of other glitches at lower frequencies
as well, but these are harder to see clearly because of how little room
they take up on the graph; to solve this, we use the same transformation
as the Gravity Spy spectrograms do: taking the logarithm of the
frequency values.

![](proposal_files/figure-gfm/peakFreq-log-plot-1.png)<!-- -->

In this new graph, while we can still see the high-frequency spikes, we
can now also see many lower-frequency trends (as well as similar
gridline textures as in the previous diagrams). One of the most
striking, in my opinion, is the line at 20Hz that seperates the low
frequency lines and bursts from the scattered light glitches. There is a
similar line on the other side of the scattered light glitches which
seperates them from most other glitches (although there is a small area
outside this line where there are scattered lights mixed with other
glitch types, surprisingly enough still bounded by vertical lines). I
have outlined these areas in the following plot:

![](proposal_files/figure-gfm/peakFreq-log-plot-annotated-SL-1.png)<!-- -->

Moving back to the unmarked graph, we can see the 60Hz Power Line
glitches as a line of orange-coloured points around the 60Hz-line, and
the Air Compressor glitches as a similar, yellow line at around 45Hz. We
also see that in this graph, blips are mostly found in a triangle from
40Hz to 700Hz, and with durations less than 1 second, with a cluster of
Helixes in the center. The area above this triangle has a background
patterned with the dark blues of Koi Fish and Light Modulation, the cyan
colour of Scratchy glitches, and the pale blue of Tomtes. Restricting
our graph to these types of glitches to get a better look at their
distributions, we get the following graph:

![](proposal_files/figure-gfm/peakFreq-log-plot-bliplike-1.png)<!-- -->
Here, we can tell that Light Modulation has data points all across the
graph, from around (1000, 0) to around (11, 5), while Tomtes are fairly
localised between (32, 0) and (64, 1.3), with few exceptions. Helices
are indeed clustered in the center of the Blip cluster, which is in most
cases visibly seperate from the Koi Fish cluster, with Scratchy glitches
being found throughout both of these.

### Methods

To find a good predictor of the glitch class, I think a good approach
would be to start by finding a simple way to divide the space of all
glitches into two to four smaller groups, each containing different sets
of glitch classes, and then doing the same to these groups as well,
shaving off more bits of the phase space until all groups we have
(generally) represent either one glitch class or two significatly
similar classes. To do this, a good strategy would be to start by
mapping out projections from different sides of the hypersurface, and
then look for simple linear or planar areas where the data could be
divided, and move on to more complicated ways to split the data if those
don’t work. This might run into some trouble with certain glitch
classes, such as light modulation, which would be hard to create a
single classification for, since they visually look like two seperate
“glitchlets”, when they’re actually one, just with a gap in the center,
as seen in the following image: ![light
modulation](https://panoptes-uploads.zooniverse.org/production/subject_location/b82c8bd6-1932-488e-b394-b87a33f848d7.png)
As you can see, sometimes, as here, the signal detector will trigger on
the tall, thin, blip-like glitchlet, and the metadata will show a
roughly blip-like glitch, while other times, it will trigger on the
lower, wider glitchlet, which would produce metadata similar to a
low-frequency burst. Examples of these glitches are shown below:

Blip: ![Example
blip](https://panoptes-uploads.zooniverse.org/production/subject_location/b5776a8b-0462-4c33-97df-cd4c836b471c.png)

Low Frequency Burst: ![Example
LFB](https://panoptes-uploads.zooniverse.org/production/subject_location/e6404b8b-130e-4052-8205-d31c811db502.png)

In these cases, it may be impossible to characterize them, since this
dataset doesn’t contain data on the evolution of the glitches over time
(the contours of the shape of the glitch in time-frequency space). If
this is true, we may have to ignore these types of glitches in our
analysis (a similar problem may occur with repeating blips, but in that
case, we could probably just group them together with their component
blips, since they are composite glitches). On the other end of the
scale, however, the “No Glitch” and “Extremely Loud” categories should
be extremely easy to split off, with possibly only SNR being a necessary
factor for their separation.
