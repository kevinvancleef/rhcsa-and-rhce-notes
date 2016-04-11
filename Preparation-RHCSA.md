## Preparation Red Hat Certified System Administrator (RHCSA)

### Installing RHEL7 on Physical Computer Using Bootable USB.

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

### Using Basic Linux Tools.

#### Accessing another Linux system via SSH (Secure Shell)
When logged in as user A and you want to login as user A on a remote machine, enter: `ssh IP-ADDRESS`.

When you logged in as user A and want to login as another user, enter either `ssh -l USERNAME IP-ADDRESS` or `ssh USERNAME@IP-ADDRESS`.

The flag `-X` can be added to run the graphical tools. E.g. `ssh -X IP-ADDRESS`.


#### Commands
Basic syntax of a command is: `command options argument`. Options are also known as `flags` or `switches`.

##### Listing files and directories
The `ls`, list, command produces a list of files and directories and displays these on the screen.

`ls -a`
Lists hidden files also. Files and directories starting with a dot are considered hidden.

`ls -l`
Displays long listing with detailed information like the file type, permissions, link count, owner, group, size, date and time of last modification and the name of the file. An alternative is using `ll` to show a long list.

`ls -lh`
Displays a long listing like the one before but now with the size in a more human readable format.

`ls -ld`
Displays a long listing, but hides its contents.

`ls -R`
List content of directory and sub directories recursively.

`ls -lt`
List all files sorted by date and time with the newest file on top.

`ls -ltr`
List all files sorted by date and time with the oldest file on top.

##### Printing working directory

The `pwd`, print working directory, shows the absolute path to the current directory on screen.

##### Changing directories
The `cd` command is used to change between directories.

To travel directly to a specific path, enter: `cd PATH`. E.g. `cd /var/log`.

To go directory to the users home directly enter either `cd` or `cd ~`. To enter a specific directory in the home directory you can use `cd ~/some-directory`.

To go to the home directory of another user, enter: `cd ~username`. E.g. `cd ~user1`. This command works only when the execution bit is set on the home directory of the user at the public level.

Usage of the ~ character is called tilde substitution.

Use `cd /` to go directly to the root directory.

Use `cd -` to switch between current en previous directory.

use `cd ..` to travel one directory up.

##### Showing the terminal file
To display the terminal name we are logged-in to to the screen with the command `tty`.

##### Listing currently logged-in users

The `who` command reads information from `/var/run/utmp` and prints information like, username, shell name, date/time and the source, `:0` for graphical and `IP-address` for remote, of the users currently logged-in to the system to the screen.

`who am i` return the same information but then only for the user executing the command.

The `w`, what, command displays similar information as the `who` command, but in more detail. It also tells the length of time the user has been idle for, along with CPU utilization and current activity. Average load is shown for the last 1, 5 and 15 minutes.

##### Inspecting systems uptime
The `uptime` command show the current system time, how long it has been up for, number of users currently logged-in, and the average load for the pas 1, 5 and 15 minutes.

##### Viewing user login name
The `whoami` command shows the name of the user executing the command.

The `logname`, login name, command shows the name of the real user who originally logged-in to the system. When using the su command, this command still shows the real username instead of `whoami`.

##### Examining user and group information
The `id` command displays a users UID, username, GID, group name, secondary groups, and SELinux context.

The `groups` command show all the groups the user is member of. The first groups is the primary group, the rest are secondary groups.

##### Viewing history of successful user login attempts
The `last` command shows the history of successful login attempts and system reboots by reading this information from `/var/log/wtmp`. This file contains information of all login and logout activities, including login time, duration and terminal name (tty).

Filtering this information can be done by e.g. `last reboot`, to show all reboot information, or `last username` to show all activity for a specific user.

##### Viewing history of failed login attempts
The `lastb` command show all information related to unsuccessful login attempts by reading the file `/va/log/btmp`.

The `lastb` command can only be executed by the `root` user.

##### Display recent user logins
The `lastlog`, last login, command shown information related to the last login attempts of users, but also when a user has never logged-in.

##### Viewing system information
The `uname` command can be used to show information about a system. Called without any options it is showing the kernel name.

Use `uname -a` to get more detailed information about system. Use the following flags to get specific information, the kernel [`-s`], hostname [`-n`], kernel release [`-r`], date/time of kernel built [`-v`], machine hardware name [`-m`], processor type [`-p`], hardware platform [`-i`] and operating system name [`-o`].

##### Displaying and setting hostname
Show hostname and hardware information with `hostnamectl` or only the hostname with `hostname`.

Change hostname with `hostnamectl set-hostname new-hostname.example.com`.

##### Clearing the screen
Use shortcut `Ctrl + l` or type `clear`.

##### Displaying and setting system date and time.
Show the systems date and time information with `timedatectl` or `date` to only show the date.

To change the date to August 12, 2015 use `timedatectl set-time 2015-08-12`.

To change the time to 11:00 use `timedatectl set-time 11:00`.

An alternative is `date --set "2015-08-12 11:00:00"`.

##### Listing and modifying system timezone
Show available timezones with `timedatectl list-timezones`.

To change the timezone use `timedatectl set-timezone Europe/Amsterdam`.

##### Displaying command path
The `which` command is showing the path of the command executed when run without the absolute path.

##### Counting word, lines and characters
The `wc FILE`, word count, command can be used to count words, lines and characters. Numbers shown are in order lines, words, characters (bytes).

Following options can be used to can specific counts. `-l` for counting lines, `-w` for counting words, `-c` for counting bytes and `-m` for counting characters.

##### Listing PCI, USB and CPU device information

The `lspci` command displays information about PCI buses and the devices attached to them. Options `-v`, `-vv` and `-vvv` can be used to get more verbose information. Use options `-m` to get a more legible output.

The `lsusb` command displays information about USB buses and the devices connected to them.

The `lscpu` command show information about the processor, incl, architecture, operating modus, count, vendor, family, model, speed, and the presence of virtualization support.

#### Compression tools
Compression tools are use to compress one or more files or an archive to save space. Once a compressed archive is created, it can be copied to a remote system faster than a non-compressed archive.

Example tools:
* bzip2 (bunzip2)
* gzip (gunzip)

##### Using gzip and gunzip
The gzip command is used to compress files which the following command, it created a compressed version of the file which adds the .gz extension.

```shell
gzip FILE_1 FILE_2
```

Uncompressing the files can be done with one of the commands below.

```shell
gunzip FILE_1 FILE_2
gzip -d FILE_1
```

##### Using bzip2 and bunzip2
The bzip2 command is used to compress files which the following command, it created a compressed version of the file which adds the .bz2 extension.

```shell
bzip2 FILE_1 FILE_2
```

Uncompressing the files can be done with one of the commands
below.

```shell
bunzip2 FILE_1 FILE_2
bzip2 -d FILE_1
```

#### Archiving tools
RHEL offers many tools that can be utilized to archive files for storage or distribution. For example `tar` and `star`. Both tools have the ability to preserve general file attributes, such as ownership, group membership, and timestamps.

##### Using tar
The tar, tape archive, command creates, appends, updates, lists, and extracts file to and from a single file called a tar file (or tarball).

The command structure is:

```shell
tar OPTIONS DESTINATION_FILE SOURCE_FILE_OR_DIR
```

Below a list of options available for the tar command. The dash (-) before each option flag is optional.

`-c`, create a tarball.

`-f`, specifiy the name of the tarball.

`-j`, compress the tarball with bzip2.

`-r`, appends files to an existing tarball. Does not work for compressed tarballs.

`-t`, lists the contents of a tarball.

`-u`, appends files to an existing tarball if the specified files are newer. Does not work for compressed tarballs.

`-v`, verbose output.

`-x`, extracts a tarball.

`-z`, compress the tarball with gzip.

`--selinux`, `--no-selinux`, includes or excludes SELinux file context in tarball archive.

`--xattrs`, `no-xattrs`, includes or excludes extended file attributes in tarball archive.

##### Using star
The `star`, standard tar, command is an enhanced version of `tar`. Star does have the same options as tar, but is not installed by default.

#### The vi (vim) editor



##### Modes of operation
##### Starting vi
##### Inserting text
##### Navigating within vi
##### Deleting text
##### Undoing and repeating
##### Searching and replacing text
##### Copying, moving and pasting text
##### Changing text
##### Saving and quitting vi

#### Online help

##### Using man
