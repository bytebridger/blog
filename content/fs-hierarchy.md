<!--- Filesystem Hierarchy Standard v3 --->
<!--- LSB Workgroup, The Linux Foundation --->
<!--- study notes --->

+++
title = "Filesystem Hierarchy Standard - study notes"
date = 2023-02-25

[taxonomies]
categories = ["Linux"]
+++

This standard consists of a set of requirements and guidelines for file and directory placement under UNIX-like
operating systems. The guidelines are intended to support interoperability of applications, system administration tools,
development tools, and scripts as well as greater uniformity of documentation for these systems.

<!-- more -->

# Filesystem Hierarchy Standard

# Ch. 1 - Introduction

- This standard enables software and users to predict the location of installed files and directories. 

# Ch.2 - The filesystem

- We can define two independent distinctions among files:
	- shareable vs. unshareable
	- variable vs. static

- In general, files that differ in either of these respects should be located in different directories. This makes it easy to store files with different usage characteristics on different filesystems.

	- `shareable files` are files that can be stored on one host and used on others.
	`unshareable files` are those that are not shareable - example with device lock files.

	- `static files` include binaries, libraries, documentation files and other files that do not change without sys admin intervention.
	- `variable files` are files that are not static.

# Ch. 3 - The Root Filesystem
	
- The contents of the root filesystem must be adequate to boot, restore, recover and / or repair the system.
- The root filesystem contains many system-specific configuration files - possible examples include a kernel that is specific to the system.

- The following firectories or symbolic links to directories are required in `/`:

- `bin` - essential command binaries.
- `boot` - static files of the boot loader.
- `dev` - device files.
- `etc` - host-specific system configuration.
- `lib` - essential shared libraries and kernel modules.
- `media` - mount point for removable media.
- `mnt` - mount point for mounting a filesystem temporarily.
- `opt` - add-on application software packages.
- `run` - data relevant to running processes.
- `sbin` - essential system binaries.
- `srv` - data for services provided by this system.
- `tmp` - temporary files.
- `usr` - secondary hierarchy.
- `var` - variable data.

- The following directories or symbolic links to directories must be in `/` if the corresponding subsystem is installed:

- `home` - user home directories (optional).
- `lib<qual>` - alternate format essential shared libraries.
- `root` - home directory for the root user.

## `/bin` - essential user command binaries

- `/bin` contains commands that may be used by all users. The following commands are required in `/bin`:

- `cat` - Utility to concatenate files to standard output.
- `chgrp` - Utility to change file group ownership.
- `chmod` - Utility to change file access permissions.
- `chown` - Utility to change file owner and group.
- `cp` - Utility to copy files and directories.
- `date` - Utility to print or set the system data and time.
- `dd` - Utility to convert and copy a file.
- `df` - Utility to report filesystem disk space usage.
- `dmesg` - Utility to print or control the kernel message buffer.
- `echo` - Utility to display a line of text.
- `false` - Utility to do nothing, unsuccessfully.
- `hostname` - Utility to show or set the system's host name.
- `kill` - Utility to send signals to processes.
- `ln` - Utility to make links between files.
- `login` - Utility to begin a session on the system.
- `ls` - Utility to list directory contents.
- `mkdir` - Utility to make directories.
- `mknod` - Utility to make block or character special files.
- `more` - Utility to page through text.
- `mount` - Utility to mount a filesystem.
- `mv` - Utility to move/rename files.
- `ps` - Utility to report process status.
- `pwd` - Utility to print name of current working directory.
- `rm` - Utility to remove files or directories.
- `rmdir` - Utility to remove empty directories.
- `sed` - The `sed' stream editor.
- `sh` - POSIX compatible command shell.
- `stty` - Utility to change and print terminal line settings.
- `su` - Utility to change user ID.
- `sync` - Utility to flush filesystem buffers.
- `true` - Utility to do nothing, successfully.
- `umount` - Utility to unmount file systems.
- `uname` - Utility to print system information.

- The following programs or symbolic links to programs must be in `/bin` if the corresponding subsystem is installed:

- `csh` - the C shell.
- `ed` - The `ed' editor.
- `tar` - The tar archiving utility.
- `cpio` - The cpio archiving utility.
- `gzip` - The GNU compression utility.
- `gunzip` - The GNU uncompression utility.
- `zcat` - The GNU uncompression utility.
- `netstat` - The network statistics utility.
- `ping` - The ICMP network test utility.

## `/boot` - static files of the boot loader

- The `/boot` stores data that is used before the kernel begins executing user-mode programs. This may include saved master boot sectors and sector map files.
- Programs necessary to arrange for the boot loader to be able to boot a file must be placed in `/sbin`. Configuration files for boot loaders that are not required at boot time must be placed in `/etc`.
- The operating system kernel must be located in either `/` or `/boot`.

## `/dev` - device files

- The `/dev` directory is the location of special or device files, it must contain a command named `MAKEDEV` which can create devices as needed.

## `/etc` - host-specific system configuration

- The `/etc` hierarchy contains configuration files. A configuration file is a local file used to control the operation of a program, it must be static and cannot be an executable binary. 
- It is recommended t hat files be stored in subdirectories of `/etc` rather than directly in `/etc`.

- The `/opt` directory or symbolic link to directory is required in `/etc`.

## `/etc/opt` - configuration files for `/opt`

- Host-specific config files for add-on application software packages must be installed within the directory `/etc/opt/<subdir>` where `<subdir>` is the name of the subtree in `/opt` where the static data from that package is stored.

## `/lib` - essential shared libraries and kernel modules

- The `/lib` directory contains those shared library images needed to boot the system and run the commands in the root filesystem, for example - by binaries in `/bin` and `/sbin`.

## `/media` - mount point for removable media

- The `/media` directory contains subdirectories which are used as mount points for removable media.

## `/mnt` - mount point for a temporarily mounted filesystem

- This directory is provided so that the system administrator may temporarily mount a filesystem as needed. The content of this directory is a local issue and should not affect the manner in which any program is run.

- This directory must not be used by installation programs.

## `/opt` - add-on application software packages

- `/opt` is reserved for the installation of add-on application software packages.

- A package to be installed in `/opt` must locate its static files in a separate `opt/<package>` or `opt/<provider>` directory tree, where `<package>` is a name that describes the software package and `<provider>` is the provider's LANANA registered name.

- Package files that are variable (change in normal operation) must be installed in `/var/opt`, while host-specific configuration files must be installed in `/etc/opt`.

- Generally, all data required to support a package on a system must be present within `/opt/<package>`, including files intended to be copied into `/etc/opt/<package>` and `/var/opt/<package>` as well as reserved directories in `/opt`.

## `/root` - home directory for the root user

- The root account's home directory may be determined by developer or local preference, but this is the recommended default location.

## `/run` - run-time variable data

- This directory contains system information data describing the system since it was booted.

## `/sbin` - system binaries

- Utilities used for system administration and other root-only commands are stored in `/sbin`, `/usr/sbin` and `/usr/local/sbin`. 
- `/sbin` contains binaries essential for booting, restoring, recovering, and / or reparining the system in addition to the binaries in `/bin`. 

## `/srv` - data for services provided by this system

- `/srv` contains site-specific data which is served by this system.

## `/tmp` - temporary files

- The `/tmp` directory must be made available for programs that require temporary files. 

# Ch. 4 - The `/usr` hierarchy

- `/usr` is the second major section of the filesystem, shareable, read-only data. The following directories, or symbolic links to directories are required in `/usr`:

- `bin` - most user commands
- `lib` - libraries
- `local` - local hierarchy
- `sbin` - non-vital system binaries
- `share` - architecture-independent data

## `/usr/bin` - most user commands

- `/usr/bin` - the primary directory of executable commands on the system.

## `/usr/include` - directory for standard include files.

## `/usr/lib` - libraries for programming and packages

- `/usr/lib` includes object files and libraries. On some systems, it may also include internal binaries that are not intended to be executed directly by users or shell scripts.

## `/usr/libexec` - binaries run by other programs 

- `/usr/libexec` includes internal binaries that are not intended to be executed directly by users or shell scripts. Applications may use a single subdirectory under `/usr/libexec`.

## `/usr/local` - local hierarchy

- The `/usr/local` hierarchy is for use by the system administrator when installing software locally. It needs to be safe from being overwritten when the system software is updated. It may be used for programs and data that are shareable amongst a group of hosts, but not found in `/usr`.

- Locally installed software must be placed within `/usr/local` rather than `/usr` unless it is being installed to replace or upgrade software in `/usr`. 

- The following directories or sym links to directories must be in `/usr/local`:

- `bin` - local binaries.
- `etc` - host-specific system configuration for local binaries.
- `games` - local game binaries.
- `include` - local C header files.
- `lib` - local libraries.
- `man` - local online manuals.
- `sbin` - local system binaries.
- `share` - local architecture-independent hierarchy.
- `src` - local source code.

## `/usr/bin` - non-essential standard system binaries

- This directory contains any non-essential binaries used exclusively by the system administrator. System administration programs that are required for system repair, system recovery, mounting `/usr` or other essential functions must be placed in `/sbin` instead.

## `/usr/share` - architecture-independent data

- The `/usr/share` hierarchy is for all read-only architecture independent data files. The following directories or sym links to directories must be in `/usr/share`.

- `man` - online manuals.
- `misc` - miscellaneous architecture-independent data.

## `/usr/share/man` - manual pages

- The primary `<mandir>` of the system is `/usr/share/man`. `/usr/share/man` contains manual information for commands and data under the `/` and `/usr` filesystems.

# Ch. 5 - The `/var` Hierarchy

- `/var` contains variable data files. This includes `spool` directories and files, administrative and logging data, and transient and temporary files. The following directories or symbolic links to directories are required in `/var`:

- `cache` - application cache data.
- `lib` - variable state information.
- `local` - variable data for `/usr/local`.
- `lock` - lock files. 
- `log` - log files and directories.
- `opt` - variable data for `/opt`.
- `run` - data relevant to running processes.
- `spool` - application spool data.
- `tmp` - temporary files preserved between system reboots.

- Several directories that are reserved and cannot be used by some new application:

- `/var/backups`
- `/var/cron`
- `/var/msgs`
- `/var/preserve`

## `/var/cache` - application cache data

- `/var/cache` is intended for cached data from applications. Such data is locally generated as a result of time-consuming `I/O` or calculation. The application must be able to generate or restore the data. Unlike `/var/spool` the cached files can be deleted without data loss. The data must remain valid between invocations of the application and rebooting the system.

## `/var/crash` - system crash dumps

- This directory holds system crash dumps.

## `/var/lib` - variable state information

- This hierarchy holds state information pertaining to an application or the system. 

- State information is data that programs modify while they run, and that pertains to one specific host. Users must never need to modify files in `/var/lib` to configure a package's operation, and the specific file hierarchy used to store the data must not be exposed to regular users.

- The following directory or sym link to directory is required in `/var/lib`:

	- `misc` - miscellaneous state data.

## `/var/lib/<editor>` - Editor backup files and state

- These directories contain saved files generated by any unexpected termination of an editor (e.g., elvis,jove, nvi).

## `/var/lock` - Lock files

- In this directory we can find lock files for devices and other resources shared by multiple applications, such as the serial device lock files.

## `/var/log` - Log files and directories

- This directory contains miscellaneous log files.

## `/var/spool` - Application spool data

- `/var/spool` contains data which is awaiting some kind of later processing. Data in `/var/spool` represents work to be done in the future (by a program, user, or administrator); often data is deleted after
it has been processed.

## `/var/tmp` - Temporary files preserved between system reboots

- The `/var/tmp` directory is made available for programs that require temporary files or directories that are preserved between system reboots. 

- Therefore, data stored in `/var/tmp` is more persistent than data
in `/tmp`.

# Ch. 6 - Operating System Specific Annex

## `/dev` - Devices and special files

- The following devices must exist under `/dev`:

	- `/dev/null` - All data written to this device is discarded. A read from this device will return an EOF condition.
	- `/dev/zero`
	- `/dev/tty`

## `/proc` - Kernel and process information virtual filesystem

- The `proc` filesystem is the de-facto standard Linux method for handling process and system information, rather than `/dev/kmem` and other similar methods. We strongly encourage this for the storage and retrieval of process information as well as other kernel and memory information.

## `/sbin` - Essential system binaries

- Linux systems place commands relating to filesystem maintenance and boot loader management into `/sbin`.

## `/sys` - Kernel and system information virtual filesystem

- The `sys` filesystem is the location where information about devices, drivers, and some kernel features is exposed. Its underlying structure is determined by the particular Linux kernel being used at the moment, and is otherwise unspecified.

## `/var/spool/cron` - cron and at jobs

- This directory contains the variable data for the cron and at programs.

# Ch. 7 - Appendix

###### 💾 EOF

- Husein



















