# plugin_getTimeAndF0Data (v.0.1.0)
A Praat plugin to create a table with time and F0 data extracted from a Sound object and TextGrid annotated (broadly) using [PoLaR](https://www.polarlabels.com/).

It requires [Praat version 6.x.x](http://www.fon.hum.uva.nl/praat/).

The time data includes:

* time in seconds
* time normalised to syllable count
* time normalised to Pitch Accent duration
* time centred around the centre of the lexically stressed syllable ("*") and normalised to the duration from the star to the last turning point in the PA.

The F0 data includes:

* F0 in Hertz
* F0 z-score normalised re local PA F0 mean and standard deviation
* F0 z-score normalised re global (file-wide) F0 mean and standard deviation (if requested)
* PoLaR level values

To use the plugin, select "Code" followed by "Download ZIP".
Extract the ZIP file and copy the plugin_getTimeAndF0Data folder to your Praat preferences directory. (See http://www.fon.hum.uva.nl/praat/manual/preferences_directory.html for more information.)

----------------
## About the TextGrids
The script expects four tiers:
Tier | Type | Comment
----|----|----
Points | point tier | Turning points as per PoLaR annotation.
Prosodic structure | point tier | as per PoLaR annotation, marking the centre of lexically stressed syllables with a "*" at least.
Levels | point tier | PoLaR Levels annotation tier.
Syllable | interval tier | Syllable-wise division of the utterance(s).
Pitch Accent | interval tier | Uses Interval to mark the start and end of each pitch accents, with text headed with "N-" or "PN-" for nuclear and pre-nuclear respectively.

## About the Output
The script will generate a table containing the following information for
each time point associated with a pitch accent in the sound file:

1. file name
2. index of the associated pitch accent
3. index of the point in the pitch accent
4. time (secs) of the point
5. time normalized to the number of syllables in the phrase containing the pitch accent
6. time normalized to the duration of the pitch accent
7. F0 in hertz at the time point
8. F0 as a local z-score, using the mean and SD of F0 for the current pitch accent
9. If requested, F0 as a global z-score, using the mean and SD of the whole sound file
10. F0 as a level identified by PoLaR

## About the User Interface

The option to get the time and F0 Data appears under "Polar Data Extraction" heading when a TextGrid and sound file are selected in the options menu. Most of the options are fairly self-explanatory, except for the following:

1. **Max time delta between point and level (ms)**

    This is the maximum time difference allowed between an annotation in the points tier and an associated annotation in the levels tier. It is a failsafe in case there is no appropriate matching level tier annotation. A warning will appean in the Info window.

2. **Add F0 z scores based on whole recording**

    This will add an extra row to the output table containing F0 z-scores which the mean and SD of the whole sound file.

3. **Run advanced pitch settings**

    Checking this brings up the advanced pitch settings.

4. **Check pitch contour**

    Offers the option to check the pitch contour and correct any pitch halving or doubling errors.
    
5. **Correct undefined F0**

    Offers the option to manually input the F0 value where automatic pitch detection has failed.
    NOTE: this assumes that the original point was selected because it had real F0 value.

## Notes
1. The pitch contour is interpolated to mitigate against undefined F0 values. If there are (for any reason) still undefined time points, a warning appears in the Info window.
2. A value of -1 in the F0_level column means no associated level value was found in the TextGrid.
3. This there may be some idiosyncrasies in the script as it was designed to aid a fellow PhD student's research.

## Change log
0.0.3
* PA times are now relative to the first turning point in the PA.
* Added time normalized to starred tone.
* Script ends by selecting the output table.
