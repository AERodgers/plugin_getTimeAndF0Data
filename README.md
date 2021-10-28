# plugin_getTimeAndF0Data
A praat plugin to create a table with time and F0 data extracted from a Sound object and TextGrid annotated (broadly) using [PoLaR](https://www.polarlabels.com/).

It requires [Praat version 6.x.x](http://www.fon.hum.uva.nl/praat/).

The time data includes:

* time in seconds
* time normalised to syllable count
* time normalised to Pitch Accent duration

The F0 data includes:

* F0 in Hertz
* F0 normalised to local PA z-score
* PoLaR level values


To use the plugin, select "Clone or download" followed by "Download ZIP".
Extract the ZIP file and copy the plugin_getTimeAndF0Data folder to your Praat preferences directory. (See http://www.fon.hum.uva.nl/praat/manual/preferences_directory.html for more information.)

----------------
## About the TextGrids
The script expects four tiers:
Tier | Type | Comment
----|----|----
Points | point tier | Turning points as per PoLaR annotation.
Levels | point tier | PoLaR Levels annotation tier.
Syllable | interval tier | Syllable-wise division of the utterance(s).
Pitch Accent | interval tier | Uses Interval to mark the start and end of each pitch accents, with text headed with "N-" or "PN-" for nuclear and pre-nuclear respectively.

## About the Output
The script will generate a table containing the following information for
each time point associated with a pitch accent in the sound file:

1. file name
2. index of the assocated pitch accent
3. index of the point in the pitch accent
4. time (secs) of the point
5. time normalized to the number of syllables in the phrase containing the pitch accent
6. time normalized to the duration of the pitch accent
7. F0 in hertz at the time point
8. F0 as a z-score, using the mean and SD of F0 for the current pitch accent
9. F0 as a level identified by PoLaR

## About the User Interface

The option to get the time and F0 Data appears under "Polar Data Extraction" heading when a textgrid and sound file are selected in the options menu. Most of the options are fairly self-explanatory, except for the following:

1. **Max time delta betwen point and level (ms)**

    This is the maximum time difference allowed between an annotation in the points tier and an associated annotation in the levels tier. It is a failsafe in case there is no appropriate matching level tier annotation. The user is warned if one cannot be found.
2. **Run advanced pitch settings**

    Checking this brings up the advanced pitch settings.
    
3. **Check pitch contour**

    Offers the option to check the pitch contour and correct any pitch halving or doubling errors.
               
## Notes
1. The pitch contour is interpolated to mitigate against undefined F0 values.
2. A value of -1 in the F0_level column means no associated level value was found in the textgrid.
3. This there may be some idiosyncrasies in the script as it was designed to aid a fellow PhD student's research.
