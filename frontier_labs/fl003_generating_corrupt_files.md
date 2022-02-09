# Generating corrupt full-size files

|Problem ID | Manufacturer | Affected firmware|Affected hardware | Status              |
|-----------|--------------|------------------|------------------|---------------------|
|FL003         |Frontier Labs |      2.2; 2.5; 2.8 | BAR            |   Major problem     |

The BARs produce audio files that are full-size but only have partial data
written to them.

An example: There were 4 sensors, at 4 sites, and the last recording from each
site experienced this "corruption". Each of the four files appears to have two
things wrong with them:

-   The _Subchunk2Size_ field (offset at byte `40`) in the WAV header is set to
    `0x0000002c` (`44` decimal) when it should be much much larger
-   And each of the files seems to be only partially written - after some
    point only empty bytes (`NUL`s / zeroes) are present in the file

The likely cause is a sensor running out of battery life and shutting down
(confirmed by FL). Apparently, the files are pre-allocated (hence the empty
bytes at the end) and the _SubChunk2Size_ field is written only at the end of the
writing process.

The result of the malformed header means that SoX reports absolutely absurd
sample rates for recordings (e.g. `5.4 Terasamples per second` or 
`34.4 Terasamples per second`).

## Status
**Major Problem**

## Status with vendor

Have contacted Frontier Labs, but they don’t see it as a problem
– if it is always the last file in the deployment then"_that the second last
file is the last correct file_". Recommended changing the file extension of an in
progress file being written to a `.partial` extension – this would allow easy
filtering of the partially written files. Unsure if they plan to deal with it.

Additionally, these files should have recoverable WAV data in them but we don’t
yet have a tool that can repair them.

## Tools to process the data
1. Acoustics Workbench (Ecosounds, A2O): **Not really**, but it can vary:

-   Yes: SoX usually reports massive bit rates and sometimes it detect
    this as invalid and fail when processing the file
-   Kinda: When harvesting the files get rejected because they are "too short".
    This is actually a misnomer: they are too short because the sample rate is so high that their reported duration is ~0 seconds. They aren't harvested but a better error message would be ideal. Tracking issue:
    <https://github.com/QutBioacoustics/baw-workers/issues/63>
-   No: Sometimes the files pass by our initial validation. 

2. AnalysisPrograms.exe: **No**
- This leads to an OutOfMemoryException. Tracking issue:
    <https://github.com/QutBioacoustics/audio-analysis/issues/141>
-   No: our tools have no way to detect these files without trying to read them
-   No: we have no method for repairing these files – they mostly have valid
    data


