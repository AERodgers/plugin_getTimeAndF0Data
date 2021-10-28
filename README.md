# plugin_getTimeAndF0Data
A praat plugin to create a table with time and F0 data extracted from a Sound object and TextGrid annotated (broadly) using [PoLaR](https://www.polarlabels.com/).

The time data includes:

* time in seconds
* time normalised to syllable count
* time normalised to Pitch Accent duration

The F0 data includes:

* F0 in Hertz
* F0 normalised to local PA z-score
* PoLaR level values

The script expects four tiers:
Tier | Type | Comment
----|----|----
Points | point tier | Turning points as per PoLaR annotation.
Levels | point tier | PoLaR Levels annotation tier.
Syllable | interval tier | Syllable-wise division of the utterance(s).
Pitch Accent | interval tier | Uses Interval to mark the start and end of each pitch accents, with text headed with "N-" or "PN-" for nuclear and pre-nuclear respectively
 
NOTE: This there may be some idiosyncrasies in the script as it was designed to aid a fellow PhD student's research.

