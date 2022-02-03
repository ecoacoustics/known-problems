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

## Tools to process the data
1. Audacity: **Yes** 
2. Acoustics Workbench (Ecosounds, A2O): **No**

-   The workbench needs correct metadata

3. AP: **No**, but can be worked around by analyzing the first half of the file by specifying the `-s 0 -e <actual end offset>` arguments


