# Empty blocks of audio data

|Problem ID | Manufacturer | Firmware changes | Status              |
|-----------|--------------|------------------|---------------------|
|FL020         |Frontier Labs |                  |   Minor problem     |



Sometimes BARs start recording and no signal is recorded, until at some point
the signal starts being captured.

In the absence of signal we do capture some digital noise, indicating that the
sensor does think it is recording.

The simplest answer is that the microphone is either faulty or not attached.
Normally we'd see some indication of the microphones health in the log files but
in this case there's no mention of anything about the microphone. 

We've encountered two cases of this oddity, both with the same sensor:
- In the first case, the recording started capturing true
signal at 00:07:00.953 into the recording
- In the second case, the recording started capturing true
signal at 00:07:00.953 into the recording. Though in this case the first two 30
minute recordings captured no signal at all.

The fact that both recordings started capturing signal within one millisecond
leads me to believe this not simply a microphone connection issue.

![example of problem](https://github.com/ecoacoustics/known-problems/tree/main/media/BARs_weird_signal.png)

## Status
**Minor Problem** It most likely is just damaged hardware. This is mainly being
documented in case we discover the behaviour again.

## Tools to process the data
1. Acoustic Workbench (Ecosounds, A2O): **Yes**. It varies:

-   Yes (now): There was a bug with our background noise calculation in AP.exe
    which has been resolved <https://github.com/QutEcoacoustics/audio-analysis/issues/187>
-   Yes: We harvest and manipulate these files without error
-   No: we should be doing better QA for incoming audio and then rejecting or
    trimming files that have periods of silence in them.