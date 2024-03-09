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

## Examples of each glitch class 
#### (and their respective acronyms in the [Gravity Spy talk pages](https://www.zooniverse.org/projects/zooniverse/gravity-spy/talk/)):

- 1080 Line: ![Sample 1080 Line](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/field_guide_attached_image/25936f58-f0eb-4aff-947e-fb73b18c032a.jpeg)
- 1400 Ripple: ![Sample 1400 Ripple](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/production/project_attached_image/01f81564-9cee-49f7-b33f-c0cf059e0e44.png)
- Air Compressor: ![Sample Air Compressor](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/production/project_attached_image/21c286ea-f66b-4435-8ce9-1c759cc329a6.png)
- Blip: ![Sample Blip](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/production/project_attached_image/cd9395b9-bc24-41c1-abee-bf294ee588c0.png)
- Chirp: ![Sample Chirp](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/production/project_attached_image/69e358a1-47e0-47ce-bf48-f3b934d130c0.png)
- Extremely Loud (EL): ![Sample Extremely Loud](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/field_guide_attached_image/2d06cdc5-00f9-4df8-b01c-9a4a381827d7.jpeg)
- Helix: ![Sample Helix](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/field_guide_attached_image/3e2256a2-a58a-47b0-a0c2-21f5d026182f.jpeg)
- Koi Fish: ![Sample Koi Fish](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/field_guide_attached_image/1f6fc022-fb0a-425d-8268-1b8b594693f7.jpeg)
- Light Modulation (LM): ![Sample Light Modulation](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/field_guide_attached_image/20aa56ab-ee89-404e-aee6-caab4e1111ac.jpeg)
- Low Frequency Burst (LFB*): ![Sample LFB](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/field_guide_attached_image/c8f01659-a6dd-440c-bd87-f7b1afbda6a0.jpeg)
- Low Frequency Line (LFL): ![Sample LFL](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/production/project_attached_image/a84bb775-c7c3-467c-b35c-dfa6caef0a8b.png)
- No Glitch: ![Sample No Glitch](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/production/project_attached_image/138221a8-b8bc-4f6f-bb28-263730788240.png)
- None of the Above (NOTA): ![Sample NOTA](https://panoptes-uploads.zooniverse.org/subject_location/2a27739d-e6c7-4fd0-8520-db625b1832b1.png)

###### (or just anything that doesn't fit into the other classes)
- Paired Doves (PD): ![Sample Paired Doves](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/field_guide_attached_image/f5e80c66-c196-446c-93ee-fe7bad0255f5.jpeg)
- Power Line: ![Sample Power Line](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/production/project_attached_image/50f9b595-eeed-4360-a280-fd391ac10ab2.png)
- Repeating Blips: ![Sample Repeating Blips](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/production/project_attached_image/355b4845-0e64-46e2-ab4e-8bab49d4534f.png)
- Scattered Light (SL*): ![Sample Scattered Light](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/field_guide_attached_image/a983b07d-0a89-4cd7-a483-d5c3edd153fc.jpeg)
- Scratchy: ![Sample Scratchy](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/field_guide_attached_image/520d2eb8-5d7c-4cd5-a40c-34a6e4f8a7bc.jpeg)
- Tomte: ![Sample Tomte](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/field_guide_attached_image/5e56f0ce-7b8d-48fe-83cb-8e1f066708e2.jpeg)
- Violin Mode (aka Violin Mode Harmonics) (VM, VMH): ![Sample Violin Mode](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/field_guide_attached_image/92335ae3-fb22-4a84-ae49-c8ccdc0febd0.jpeg)
- Wandering Line ![Sample Wandering Line](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/field_guide_attached_image/4d6f9cb8-3b9a-43dd-9d5a-4420142ff14d.jpeg)
- Whistle ![Sample Whistle](https://thumbnails.zooniverse.org/500x/panoptes-uploads.zooniverse.org/field_guide_attached_image/f156a30b-2cb4-4872-8a46-457d83e744d4.jpeg)

###### *Have had extensive previous use, but used less now due to similarity with other acronyms (the LIGO detectors' "Slave Lasers" and the more recently introduced glitch class "Low Frequency Blip")
<br>

##### Examples taken from Gravity Spy classifier field guide.