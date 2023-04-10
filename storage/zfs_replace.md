```
# zpool status -v SAS_POOL
	SAS_POOL                     ONLINE       0     0     0
	  mirror-0                   ONLINE       0     0     0
	    c0t5000CCA0806295D8d0s1  ONLINE       0     0     0
	    c0t5000CCA0806E2620d0s1  ONLINE       0     0     0
	  mirror-1                   ONLINE       0     0     0
	    c0t5000CCA0806E2754d0    ONLINE       0     0     0
	    c0t5000CCA0806ED5C8d0    ONLINE       0     0     0
	  mirror-2                   ONLINE       0     0     0
	    c0t5000CCA08064DD90d0    ONLINE       0     0     0
	    c0t5000CCA0806E28E8d0    ONLINE       0     0     0
	  mirror-3                   ONLINE       0     0     0
	    c0t5000CCA0806CD5CCd0    ONLINE       0     0     0
	    c0t5000CCA0806ED974d0    ONLINE       0     0     0
	  mirror-4                   ONLINE       0     0     0
	    c0t5000CCA0806E90F4d0    ONLINE       0     0     0
	    c0t5000C500A7EB4D73d0    ONLINE       0     0     0  (slow) ====> Mark as offline
```

```
# cfgadm -alv | grep c0t5000C500A7EB4D73d0
```

c5::w5000c500a7eb4d71,0 connected configured unknown Client Device: /dev/dsk/c0t5000C500A7EB4D73d0s0(sd0)==== Mark as unconfigure

- off-line the disk drive in slot9, using

```
  #zpool offline SAS_POOL c0t5000C500A7EB4D73d0
```

- then prepare the disk drive in slot 9 for removal using cfgadm -c unconfigure command, i.e.

```

  #cfgadm -c unconfigure c5::w5000c500a7eb4d71,0

```

- then check if OK-to-remove LED (Blue) on the drive, lit.
  Once it is lit blue, pull the drive from drive bay, and install new drive.

- check cfgamd -alv, and use command 'cfgadm -c configure <AP-ID of newly installed drive>'

- once it is available in cfgadm -alv, and seen as connected and configured, as other drives, run below command

```

# zpool replace <pool name> <old/offlined drive name> <new/to be replaced drive name>

```

```
#zpool online SAS_POOL c0t5000C500A7EB4D73d0
```

https://www.oracle.com/technical-resources/articles/it-infrastructure/admin-monitor-swap-solaris-zfs.html
