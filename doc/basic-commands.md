# Basic commands section

## First commands

* ```$ whoami``` <- return the current `$USER`
* ```$ cd``` <- change directory
* ```$ ls``` <- list all of the files and directories within the current directory
* ```$ last``` <- listed the last logged in users
* ```$ pwd``` <- print working directoty (aka current directory from the `/`)

## Domain and hostname setup

* ```$ vi /etc/sysconfig/network``` -> add line equal to: HOSTNAME=example.hostname
* ```$ vi /etc/hosts```
* ```$ /etc/init.d/network restart```

## Find

### definition: Command used to locate/find a file/directory within your system.

* ```$ find . -name "test"``` <- find the test FILE within the current directory (hence the ".")
* ```$ find <dir-location> -type f -empty``` <- find any empty files within <dir-location>

## Archiving & Compression tools

### definition: group together a set of files/directories

* ```$ tar czf myfiles.tar.gz filename[1-5]``` <- compress filename[1-5] using arguements c (create tar archieve) z (process archieve through gzip) f (file)
* ```$ tar cjf myfiles.tar.bz2 filename[1-5]``` <- compress files using b arguemnts (using bzip2)
* ```$ tar cJf myfiles.tar.xz filename[1-5]``` <- compress files using b arguemnts (using LZMA compression)
* ```$ tar tvf myfiles.tar.gz``` <- view what's within compressed tar.gz file

## Decompressing

* ```$ gzip -d "filename".tar.gz```
* ```$ bzip2 -d "filename".tar.bz2```
* ```$ xz -d "filename".tar.xz```
* notes: smallest compression method is gz (czf)
* links used: https://en.wikipedia.org/wiki/Xz

## File permissions

* ```$ ls -la``` displays 10 character long description (mode, permissions) of the file/directory/sym-link in question. Eg, drwx------

* ```$ chmod``` is the command to change the permissions on a file.

 file permission meanings. Eg, chmod 744 filename:

    rwx = 4+2+1=7
    rw- = 4+2=6
    r-x = 4+0+1=5
    r-- = 4+0+0=4
    -w- = 0+2+0=2
    --x = 0+0+1=1

* First number in the sequence is owner persmissions. (7)55 <- Owner has complete rights

* Second number in the sequence is the group permissions. 7(5)5 <- Group has read and execute permissions

* Third number in the sequence is the "rest of the world" 75(5) <- "rest of the world" has read and execute permissions

## Input-output redirection

### Definition: Manipluting the output of a command

* ```$ 2>``` Redirection error.
* ```$ >``` Re-direct all output into a file
* ```$ >>``` Re-direct the output appending it to a file.
* ```$ |``` Pipe, moving the output of a command as the input to another command

## Hard and soft (symbolic) links:

* Hard links can only be used within the same filesystem
  * ```$ ln```
* Soft links can be used across different file systems
  * ```$ ln -s```
  * more visible (output of ls -l)

## Linux file system:

* `/` - root of the file system
* `/bin` - directory for binary files
* `/boot` - files required for boot
* `/dev` - physical devices are mounted
* `/etc` - configuration files are stored here
* `/lib` - libraries are stored here
* `/media` - external devices are mounted here
* `/mnt` - placeholder for devices
* `/opt` - the processes dir
* `/root` - home directory for the root user
* `/sbin` - similar to /bin folder
* `/tmp` - temporary files are stored here
* `/lost+found` - used by fsck to place files without a name
* `/var` - used to store changing files. Eg, logs
* `/usr` - contains files that are shared amongst users
* `/proc` - the process' dir