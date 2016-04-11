## Installing RHEL7 on Physical Computer Using Bootable USB.

How to create a bootable usb from iso image:
* Get CentOS7 iso image from [www.centos.org](https://www.centos.org/download/).
* Connect USB drive to the computer and unmount partition with command `diskutil unmountDisk /dev/disk2`, replace disk2 with the correct usb drive.
* Navigate to the iso image and run command `sudo dd if=CENTOS_IMAGE.iso of=/dev/disk2 bs=1m`. This command reads the iso disk and writes it to the usb drive with a block size of 1 mb. This can take a while and looks like if the process hangs, you do not get any progress updates. Also here replace disk2 with the correct usb drive.

When copying is done you will get something like the output below. The usb drive is now ready to use as installation source.

```shell
694272+0 records in
694272+0 records out
355467264 bytes transferred in 249.100402 secs (1427004 bytes/sec)
```
