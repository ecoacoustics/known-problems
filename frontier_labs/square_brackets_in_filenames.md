# Square brackets in filenames

|Problem ID | Manufacturer | Firmware changes | Status              |
|-----------|--------------|------------------|---------------------|
|FL070         |Frontier Labs |                  |   Minor problem     |

Since the BARs have GPSs in them, they encode the Latitude and Longitude in the
folder and file names of their recordings. The problem is they do it using the
following format: `20160916_Cast16-001 [-37.5397
141.3252]/20160916_154131_Cast16-001-Dsk [-37.5397 141.3252].wav`. The square
brackets in filenames are often used by shells (including Bash on Linux and
PowerShell on Windows) to denote Range Wildcards. This means many common
commands, scripts, and even our workbench fail to read the files unless the
paths are treated as literals.


## Status

**Minor Problem**. Have contacted Frontier Labs, they seemed receptive to
feedback on changing the character used to denote GPS coordinates. Unsure if
they changed the default or not.

## Tools to process the data

1. Acoustics Workbench (Ecosounds): can’t process files with wildcards in the filenames. Tracking
issue: <https://github.com/QutBioacoustics/baw-workers/issues/60>

    Slowly making our scripts more resilient to wildcard paths.

## Workarounds

Command to replace square brackets in names (using rename packaged with "SUSE
Linux Enterprise Server 12 SP2" v12.2):

```
find . -name "\*\\[\*" -type d -exec rename -v '[' \_ '{}' \\;
find . -name "\*\\]\*" -type d -exec rename -v ']' \_ '{}' \\;
find . -name "\*\\]\*" -type f -exec rename -v ']' \_ '{}' \\;
find . -name "\*\\[\*" -type f -exec rename -v '[' \_ '{}' \\;
```

Using rename packaged with Ubuntu 16.04:

```
find . -depth -name "*[*" -type d -exec rename -v 's/(\]|\[)/_/g' {} \;
```

For harvesting, it is only necessary to rename the directory. This script does this in a batch
https://github.com/QutEcoacoustics/baw-private/blob/22e70967f86e7b7f83311e7a0263fcfc40a87c9d/Scripts/removeSquareBrackets.ps1



