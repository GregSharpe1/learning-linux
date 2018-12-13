# Basic commands section

## First commands

* `$ whoami` - return the current `$USER`
* `$ cd` - change directory
* `$ ls` - list all of the files and directories within the current directory
* `$ last` - listed the last logged in users
* `$ pwd` - print working directory (aka current directory from the `/`)
* `$ man pwd` - description as well as a arguments used within this command
* `$ cat file` - concatenate the output of `file` (display the output of `file`)
* `$ history` - list all of the previous commands (commonly used in conjunction with `grep` to search the output)

## Domain and hostname setup

* `$ vi /etc/sysconfig/network` -> add line equal to: HOSTNAME=example.hostname
* `$ vi /etc/hosts`
* `$ /etc/init.d/network restart`

## Find

### definition: Command used to locate/find a file/directory within your system

* `$ find . -name "test"` - find the test FILE within the current directory (hence the ".")
* `$ find dir-location -type f -empty` - find any empty files within <dir-location>

## Archiving & Compression tools

### definition: group together a set of files/directories

* `$ tar czf myfiles.tar.gz filename[1-5]` - compress filename[1-5] using arguments c (create tar archive) z (process archive through gzip) f (file)
* $ tar cjf myfiles.tar.bz2 filename[1-5]` - compress files using b arguments (using bzip2)
* `$ tar cJf myfiles.tar.xz filename[1-5]` - compress files using b arguments (using LZMA compression)
* `$ tar tvf myfiles.tar.gz` - view what's within compressed tar.gz file

## Decompressing

* `$ gzip -d "filename".tar.gz`
* `$ bzip2 -d "filename".tar.bz2`
* `$ xz -d "filename".tar.xz`
* notes: smallest compression method is gz (czf)
* links used: https://en.wikipedia.org/wiki/Xz

## File permissions

* `$ ls -la` displays 10 character long description (mode, permissions) of the file/directory/sym-link in question. Eg, drwx------

* `$ chmod` is the command to change the permissions on a file.

 file permission meanings. Eg, chmod 744 filename:

    rwx = 4+2+1=7
    rw- = 4+2=6
    r-x = 4+0+1=5
    r-- = 4+0+0=4
    -w- = 0+2+0=2
    --x = 0+0+1=1

* First number in the sequence is owner permissions. (7)55 - Owner has complete rights

* Second number in the sequence is the group permissions. 7(5)5 - Group has read and execute permissions

* Third number in the sequence is the "rest of the world" 75(5) - "rest of the world" has read and execute permissions

## Input-output redirection

### Definition: Manipulating the output of a command

* `$ 2>` Redirection error.
* `$ >` Re-direct all output into a file
* `$ >>` Re-direct the output appending it to a file.
* `$ |` Pipe, moving the output of a command as the input to another command

## Hard and soft (symbolic) links

* Hard links can only be used within the same filesystem
  * `$ ln`
* Soft links can be used across different file systems
  * `$ ln -s`
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

## Remote desktop and file creation

* `$ ssh user@<ip/hostname>` - remote access to a server (public key has to be within the `$USER/.ssh/authorized_keys` if wish to avoid entering password (recommended))
* `$ cp file file1` - copy file one into a file name file1
* `$ rm file1` - remove file1
* `$ mv file file1` - move the contain of file into a file name file1
* `$ mkdir dir-name` - make a directory named dir-name within the current directory
* `$ rmdir dir-name` - remove a dir name (empty)
* `$ rmdir -r dir-name` - remove all files within that directory as well (`-r` recursively) as the directory

## Regular expression and grep

### *Description* Regular expressions is a way of matching patterns across a string or file

### Grep command is a powerful pattern searcher (`$ man grep`)

* `$ grep '^e' /etc/passwd` - search the `/etc/passwd` file for lines being with `e`
* `$ grep -i '^e' /etc/passwd` - search the `/etc/passwd` file for lines beginning with `e|E` `-i` will find `e` without case sensitive output (used most often)
* `$ grep 'h$' /etc/passwd` - search the `/etc/passwd` file for lines *ending* in `h`

## Using AWK

### *Description* `AWK` is a powerful processing language typically used to reformat the output of other commands [awk](https://www.gnu.org/software/gawk/manual/html_node/Very-Simple.html)

* `$ awk '//{print $1 $2 $3}' file` - extract the first three string returned from file
* `$ awk '//{print $1, $2, $3}' file` - extract the first three strings returned from file *with spaces*
* `$ awk '//{print}' /etc/hosts` - print the output of host file
* `$ awk '/localhost/{print} /etc/hosts` - extract the *lines* that contain localhost
* `$ awk '/[0-9]/{print}' /etc/hosts` - extract the *lines* containing numbers ([0-9])

## Using SED

### *Description* `sed` is a stream editor. A stream editor is used to perform basic text transformations on an input stream (a file or input from a pipeline). [sed](https://www.gnu.org/software/sed/manual/sed.html)

* `$ sed -n '5,10p` file` - read lines 5-10 in file
* `$ sed '20, 30d' file` - output everything *except* lines 20-30
* `$ sed 's/home/house/g' /etc/passwd` - _switch_ every match for home with house