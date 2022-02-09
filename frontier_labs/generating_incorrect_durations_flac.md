# Generating incorrect durations for FLAC files

|Problem ID | Manufacturer | Firmware changes | Status              |
|-----------|--------------|------------------|---------------------|
|FL04         |Frontier Labs |                  |   Major problem     |


It appears that Frontier Labs writes an incorrect value for the `duration` 
in the FLAC headers.

This affects firmwares 3.17 to 3.24.

## Status
**Major problem** 

Most audio processing tools will fail eventually when they pass the point where valid data exists.

## Example files

- [📁 FL010 files on cloudstor](https://cloudstor.aarnet.edu.au/plus/s/hrmQPSrkqV0Evvv?path=%2Ffrontier_labs%2FFL010)

## Tools to process the data
1. EMU: [EMU](https://github.com/QutEcoacoustics/emu#fix-the-fl010-metadata-duration-bug) can fix the duration of files in batch
2. Audacity: **Yes** 
3. Acoustics Workbench (Ecosounds, A2O): **No**

-   The workbench needs correct metadata

4. AP: **No**, but can be worked around by analyzing the first half of the file by specifying the `-s 0 -e <actual end offset>` arguments



