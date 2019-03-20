So, here's what I did after much face-palming and cursing of Apple and their absolute disregard for their users:

From the terminal:

Identify your USB by NAME and IDENTIFIER:
`diskutil list`
Output is:
```
/dev/disk3 (external, physical):  
#:                       TYPE NAME                    SIZE    IDENTIFIER  
0:               FDisk_partition_scheme              *2.0 GB     disk3
1:                 DOS_FAT_32 MIXTAPE                 2.0 GB   disk3s1
```

In this case, NAME=MIXTAPE and the IDENTIFIER=/dev/disk3s1

Now unmount the USB:
`sudo diskutil unmount /dev/$IDENTIFIER`
Example:

`sudo diskutil unmount /dev/disk3s1`
Output is:
```
Volume MIXTAPE on disk3s1 unmounted
```
Now create the Volume directory - this appears to be the key!
`sudo mkdir /Volumes/$NAME`
Example:

`sudo mkdir /Volumes/MIXTAPE`
No output.

Now mount the USB to the Volume:
sudo mount -w -t msdos /dev/disk3s1 /Volumes/$NAME
Example:

sudo mount -w -t msdos /dev/disk3s1 /Volumes/MIXTAPE
No output.

Validate that the USB is now writeable:
touch /Volumes/$NAME/tmp.txt
Example:

touch /Volumes/MIXTAPE/tmp.txt
You should now be able to see that you were able to create the tmp.txt file on your USB in the Finder app or by:
ls -al /Volumes/$NAME
Example:

ls -al /Volumes/MIXTAPE
