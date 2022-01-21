# Formatting SD Cards

SD cards used in the SM2 and SM2+ sensors need to be formatted with a FAT32 filesystem.
If the SD cards are formatted with another filesystem the sensor will not recognize the SD card.

## Check the filesystem of an SD card

1. Insert the SD card into a memory card reader or directly into the computer (if possible)
2. Open _Computer_ in Windows Explorer
3. Right-click on the drive that represents your SD card (e.g. _G drive_)
4. Select _Properties_
5. Look for the _File System:_ attribute and ensure it reads **`FAT32`**

## Format an SD card

Windows no longer supports formatting in the FAT32 filesystem using a GUI.
Instead we have to use a separate application.

### Using the HP USB DISK Storage Format Tool

1. Go to http://www.techspot.com/downloads/6582-hp-usb-disk-storage-format-tool.html
2. Choose _Download Now_
3. After the file has downloaded, locate in in _Windows Explorer_ - it will typically be in your _Downloads_ folder
4. Right-click the file and choose _Run as administrator_
5. In the format tool, check the correct _Device_ is set.
	1. Double check - the targeted device will have its contents erased!
6. Change _File system_ to _FAT32_
7. Ensure the other options are set as
	- _Quick Format_: ✓
	- _Enable Compression_: ✗
	- _Create a DOS startup disk_: ✗
8. Press start, wait for the format to complete
9. Optionally check the filesystem is correct (using the method in the  [Check the filesystem of an SD card](#Check the filesystem of an SD card) section)
