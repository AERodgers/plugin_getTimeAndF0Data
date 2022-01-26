# plugin_getTimeAndF0Data (v.0.1.4)
A Praat plugin to create a table with time and F0 data extracted from a Sound object and TextGrid annotated (broadly) using [PoLaR](https://www.polarlabels.com/).

## 1. Installing the Script
It requires [Praat version 6.x.x](http://www.fon.hum.uva.nl/praat/).

To use the plugin, select "Code" followed by "Download ZIP".
Extract the ZIP file and copy the plugin_getTimeAndF0Data folder to your Praat preferences directory. (See http://www.fon.hum.uva.nl/praat/manual/preferences_directory.html for more information.)

## 2. Running the Script
To access the script in Praat:
* Select both the sound object and TextGrid object in the objects window. (See section 3 below for information on TextGrids.)
* Click on the "Polar Data Extraction: Get Time and F0 Data" button that appears on the left.
* Fill in the form with the appropriate information.
* Click "Process".

## 3. About the TextGrids
The script expects four tiers in your textgrid:
Tier | Type | Comment
----|----|----
Points | point tier | Turning points as per PoLaR annotation.
Prosodic structure | point tier | as per PoLaR annotation, marking the centre of lexically stressed syllables with a "\*" at least.
Levels | point tier | PoLaR Levels annotation tier.
Syllable | interval tier | Syllable-wise division of the utterance(s).
Pitch Accent | interval tier | Uses Interval to mark the start and end of each pitch accents, with text headed with "N-" or "PN-" for nuclear and pre-nuclear respectively.

## 4. About the User Interface Form
The option to get the time and F0 Data appears under "Polar Data Extraction" heading when a TextGrid and sound file are selected in the options menu. Most of the options are fairly self-explanatory, except for the following:

1. **Max time delta between point and level (ms)**

    This is the maximum time difference allowed between an annotation in the points tier and an associated annotation in the levels tier. It is a failsafe in case there is no appropriate matching level tier annotation. A warning will appean in the Info window.

2. **Add F0 z scores based on whole recording**

    This will add an extra column to the output table containing F0 z-scores which the mean and SD of the whole sound file.

3. **Include reference values**

    This will add extra columns to the output table to show the reference values (means, standad deviations, and time of centre of stressed syllable, "\*").

4. **Run advanced pitch settings**

    Checking this brings up the advanced pitch settings.

5. **Check pitch contour**

    Offers the option to check the pitch contour and correct any pitch halving or doubling errors.

6. **Correct undefined F0**

    Offers the option to manually input the F0 value where automatic pitch detection has failed.
    NOTE: this assumes that the original point was selected because it had real F0 value.

7. **Round table values**

    This gives you the option to round the values in the output table.
    All time-related parameters will be rounded to three decimal places while all F0 measurements will be rounded to integers, with their standard deviations rounded to one decimal place.
    This option is set by default. If you unset it, all decimals will have a default precision of 16 decimal places.

## 5. Output table data
The script will generate a table containing the information for each turning point (TP) associated with a pitch accent (PA) in the sound file (FILE). The table below explains each output parameter.

Parameter | Domain | Explanation | Comment
----------|--------|-------------|--------
file | FILE | Source file name | Excludes . extension names.
accent | PA-FILE | Index of PA in file. |
type | PA |  Type of pitch accent (PN = pre-nuclear, N = nuclear). |
point | TP-PA | Index of time point within PA. |
t_secs | TP-PA | Time in seconds. | 0 = time of first TP.
t_norm_syl | TP-PA | Time normalised to syllable count. | Whole number component represents syllable number (eg., 0. = first syllable), while the decimal component represents the alignment of the TP within the syllable (e.g., .75 = a time point three quarters of the way into the syllable).
t_norm_PA | TP-PA | Time normalised to Pitch Accent duration. | 0 = first time point in PA, 1 = last time point.
t_norm_star | TP-PA | Time centred around the centre of the lexically stressed syllable ("\*") and normalised to the duration from the star to the last turning point in the PA. | Time at "\*" = 0, time at last turning point = 1, any TP before "\*" will have a negative value. Note, this can exceed -1.
F0_Hz | TP-PA | F0 in Hertz. |
F0_z_score_local | TP-PA | F0 z-score calculated using mean and standard deviation of F0 of current PA. |  
F0_z_score_global | TP-FILE | F0 z-score calculated using mean and standard deviation of F0 across the whole sound file. | This parameter only appears if "Add F0 z scores based on whole recording" has been selected.
F0_level | TP-PA | F0 defined in terms of level. | This is determined by PoLaR.
star_t | PA | Time at centre of lexically stressed syllables (\*) re first TP in PA. | This parameter only appears if "Include reference values" has been selected.
F0_mean_local | PA | Mean F0 (Hz) within the current PA | This parameter only appear if "Include reference values" has been selected.
F0_SD_local | PA | Standard deviation from the mean of F0 (Hz) within the current PA. | This parameter only appears if "Include reference values" has been selected.
F0_mean_global | FILE | Mean F0 (Hz) across the whole sound file | This parameter only appears if "Include reference values" and "Add F0 z scores based on whole recording" have been selected.
F0_SD_global | FILE | Standard deviation from the mean of (Hz) across the whole sound file | This parameter only appears if "Include reference values" and "Add F0 z scores based on whole recording" have been selected.

## Notes
1. The pitch contour is interpolated to mitigate against undefined F0 values. If there are (for any reason) still undefined time points, a warning appears in the Info window.
2. A value of -1 in the F0_level column means no associated level value was found in the TextGrid.
3. This there may be some idiosyncrasies in the script as it was designed to aid a fellow PhD student's research.

## Change log
#### 0.1.4
* t_norm_star is now correctly normalised to 1 rather than 1000.
* Added UI option to round output table decimals to manageable values (or to leave them at 16 decimal point precision).
#### 0.1.3
* PA times are now relative to the first turning point in the PA.
* Added time normalized to starred tone.
* Script ends by selecting the output table.
