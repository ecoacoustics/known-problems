# Wrong UTC offset when GPS lock cannot be acquired

The Frontier Labs BAR-LT actually includes a UTC offset in its datestamps.
~~However when a GPS lock cannot be obtained it appends `+0000` as the offset - which is incorrect.~~

Example: the following two filenames are taken from two sites that are less than 100m apart
```
20201009T000000+1000_REC.flac
20200801T000000+0000_Rec.flac
```

## Status

*Not a problem*. We've cleared up the ambiguity with FL. This boils down to the UTC Offset being set incorrectly but the datestamps are still valid.


> Someone just forgot to set the UTC offset to +1000 so the GPS updated its local clock to UTC+0000 because that’s what it was set to. It’s probably just easier if I explain how the firmware works. It gets the raw UTC+0000 time from the GPS, it then adds the UTC-offset (set by the user, stored in memory and unchanging) to that time and saves that as the local time. All filenames are written using local time and the UTC offset is written to the end of the string as per ISO8601 

## Tools to process the data

1. Ecosounds: Can satisfactorily deal with the problem
