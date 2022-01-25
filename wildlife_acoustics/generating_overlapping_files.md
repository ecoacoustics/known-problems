# Generating files that overlap with the next file in the sequence

|Problem ID | Manufacturer      | Firmware changes | Status              |
|-----------|-------------------|------------------|---------------------|
|WA030         |Wildlife Acoustics |                  |   Major problem     |


Recent deployments with SM4s have been generating files that overlap. For
example, if there are two files, `20171201_060000.wav` and `20171201_120000.wav`,
the first file will have a duration of `3617` seconds – that is `17` seconds 
past the start of the next file. Visual inspections of the neighbouring files
reveal that the end and start of the overlapping files DO NOT match and are not
duplicate data. In each of these cases nearly every file in a deployment
overlaps!

Our current theory is that the sensors maybe oversampling (sampling at, for
example, \~22075Hz rather than 22050Hz) and stopping once the “correct” number
of sample have been collected, earlier than the file should have stopped. This
theory explains why, despite a logical overlap, the collected data does not
overlap.

## Status

**Major Problem**. Not yet contacted WA

## Tools to process the data

1. Acoustics Workbench (Ecosounds, A2O): **No**. The website rejects files that overlap more than 12 seconds. Due to the
distributed nature of harvesting protocols some files in a harvest a
harvested and some are not – leading to a lengthy process required for deleting
the files from Ecosounds, trimming them, and re-harvesting.

## Workarounds:

Overlap report script:
<https://github.com/QutBioacoustics/Ecoacoustics/blob/master/Scripts/generate_overlap_report.ps1>

Trimming script:
<https://github.com/QutBioacoustics/Ecoacoustics/blob/master/Scripts/trimEndOffAudioFiles.sh>