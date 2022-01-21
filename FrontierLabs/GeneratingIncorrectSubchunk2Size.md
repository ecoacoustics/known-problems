# Generating incorrect `Subchunk2Size` header values

It appears that Frontier Labs writes an incorrect value for the `data` subchunk's
size field (known as `Subchunk2Size` or `cksize`). The value should be the size
of the data block, in bytes, and should be the equivalent of
`== NumSamples * NumChannels * BitsPerSample/8`. Essentially it is the size of
the PCM samples, which is the size of the file not including the WAV header.

Frontier Labs erroneously writes the total size of the file into the header
instead. On average this means the data size is off by 44 bytes (the standard
sized wav header) which is about 3 16-bit samples' worth.

Interestingly this problem was discovered while trying to create a validation
check for the corrupt files (see [this file](./GeneratingCorruptFiles.md)) that BARs sometimes produce.

## Status
*Minor problem*. For files with simple wav headers 3 samples worth of error is
about 0.136 seconds of error.

This problem has not been reported to FL yet.

## Tools to process the data
1. Ecosounds: **Yes**

-   Yes: While technically incorrect, all the values are small enough that they
    are omitted or ignored in our higher level code.