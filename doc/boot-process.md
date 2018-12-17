# Boot process of a REDHat/CentOS linux machine

## Post

### Power-On Self Test (POST) is executed by the BIOS and check the current state of all hardware.

#### The current checks that take place by the POST is as follows:

* Check that the Memory is working
* Check that the hard drive and other devices are responding
* Check that the keyboard and mouse are plugged in (commonly switched off)
* Initalise any additional BIOSes which may be installed (Eg. Raid cards, network cards..)

#### If for what ever reason the POST check, fails the system will be unable to boot and usually indicate this through a beep. Different beep codes can be set to help with the issue at hand (these are usually set by the motherboard manufacturer.)

## MBR (Master boot record)

### Once POST test is successful the process is moved to MBR which defines the partitions within a disk. The information held within a MBR is information including where partitions begin and end, so your operating system knows which sectors belong to each partition and which partition is bootable. This is why, when creating a partition you have to select either MBR or the _new_ and _improved_ GPT

## GRUB2 (GRand Unified Boot loader version 2)

### After the bootable partition is discovered and selected, the next step in a linux based machine is GRUB2 (Although GRUB2 can be used with Windows based machines). GRUB2 main function is to take over from the BIOS in booting the Kernel. This is done by moving the kernel into memory and then turn over to the execution of the kernel itself

## Kernel and initial RAMdisk

### The last but one stage in the linux boot process is loading the Kernel and initramfs. This is the process of loading the kernel so it can communicate with the various drivers and hardware of the system at the lowest possible level. RAMdisk is used to load these drivers in memory to allow the ability of communicating with the devices.

#### To edit the grub configuration (although discourage)

* `$ vi /etc/default/grub`

#### Once changes have been made to these overrides to have to re-compile the grub configuration, to do so run

* `$ grub-mkconfig -o /boot/grub2/grub.cfg`

#### To view the systems kernel architecture

* `$ lsinitrd`

## Systemd

### This is the last step described by the LFCS course in the boot process, this is the stage where all of the system process are started, networking etc.. Configuration set for these process like at `/etc/systemd/system-process`. Other linked processes from /etc/systemd/system/default.target are then loaded by the system to bring the system up to a defined state

### How to backup the MBR

#### First find out what what your root disk drive is by running the following

* `$ sudo fdisk -l`

        Device     Boot   Start      End  Sectors  Size Id Type
        /dev/sda1  *       2048   999423   997376  487M 83 Linux
        /dev/sda2       1001470 16775167 15773698  7.5G  5 Extended
        /dev/sda5       1001472 16775167 15773696  7.5G 8e Linux LVM

#### The below command will create a file called `mbr.bkup` which is a backup of the MBR on `/dev/sda`

* `root $ dd if=/dev/sda of=mbr.bkup bs=512 count=1`

#### This is best practice if you want to make changes to the MBR as you can restore the MBR with the following command if things don't go as planned

* `root $ dd if=mbr.bkup of=/dev/sda bs=512 count=1`

### Run levels within a linux system

      Level   Purpose
        0     Shutdown (or halt) the system
        1     Single-user mode, usually aliased
        2     Multiuser mode without networking
        3     Multiuser mode with networking
        4     Multiuser mode with networking
        5     Multiuser mode with networking and the X Window System
        6     Reboot the system

#### To view what run level the user you are logged in as is in (I'm running headless CentOS)

* `$ who -r`

        run-level 3  2018-11-30 16:10

* `$ runlevel`

#### If you need to change run-level, use the following command (replacing NUM with reference to the above table)

* `$ init NUM`

#### To view what is run depended on what run-level you are in run (after running the above and locating the number)

* `$ ls -la /etc/rc[0-6].d/` - where [0-6] is your run level

#### The command output should look something like the following (running on ubuntu18.04 Jenkins server)

    lrwxrwxrwx   1 root root   13 Sep 24  2017 K01atd -> ../init.d/atd
    lrwxrwxrwx   1 root root   18 Oct  6  2017 K01ebtables -> ../init.d/ebtables
    lrwxrwxrwx   1 root root   18 Nov 10  2017 K01filebeat -> ../init.d/filebeat
    lrwxrwxrwx   1 root root   19 Oct  6  2017 K01firewalld -> ../init.d/firewalld
    lrwxrwxrwx   1 root root   20 Sep 24  2017 K01irqbalance -> ../init.d/irqbalance
    lrwxrwxrwx   1 root root   17 Sep 24  2017 K01jenkins -> ../init.d/jenkins
    lrwxrwxrwx   1 root root   22 Sep 24  2017 K01lvm2-lvmetad -> ../init.d/lvm2-lvmetad
    lrwxrwxrwx   1 root root   23 Sep 24  2017 K01lvm2-lvmpolld -> ../init.d/lvm2-lvmpolld
    lrwxrwxrwx   1 root root   15 Sep 24  2017 K01lxcfs -> ../init.d/lxcfs
    lrwxrwxrwx   1 root root   13 Sep 24  2017 K01lxd -> ../init.d/lxd
    lrwxrwxrwx   1 root root   15 Sep 24  2017 K01mdadm -> ../init.d/mdadm
    lrwxrwxrwx   1 root root   15 Oct  6  2017 K01nginx -> ../init.d/nginx
    lrwxrwxrwx   1 root root   20 Sep 24  2017 K01open-iscsi -> ../init.d/open-iscsi
    lrwxrwxrwx   1 root root   23 Sep 24  2017 K01open-vm-tools -> ../init.d/open-vm-tools
    lrwxrwxrwx   1 root root   18 Sep 24  2017 K01plymouth -> ../init.d/plymouth
    lrwxrwxrwx   1 root root   20 Sep 24  2017 K01resolvconf -> ../init.d/resolvconf
    lrwxrwxrwx   1 root root   29 Sep 24  2017 K01unattended-upgrades -> ../init.d/unattended-upgrades
    lrwxrwxrwx   1 root root   17 Sep 24  2017 K01urandom -> ../init.d/urandom
    lrwxrwxrwx   1 root root   15 Sep 24  2017 K01uuidd -> ../init.d/uuidd
    lrwxrwxrwx   1 root root   16 Sep 24  2017 K02iscsid -> ../init.d/iscsid
    lrwxrwxrwx   1 root root   18 Sep 24  2017 K03sendsigs -> ../init.d/sendsigs
    lrwxrwxrwx   1 root root   17 Sep 24  2017 K04rsyslog -> ../init.d/rsyslog
    lrwxrwxrwx   1 root root   20 Aug 15 18:51 K05hwclock.sh -> ../init.d/hwclock.sh
    lrwxrwxrwx   1 root root   22 Sep 24  2017 K05umountnfs.sh -> ../init.d/umountnfs.sh
    lrwxrwxrwx   1 root root   17 Oct  9  2017 K06rpcbind -> ../init.d/rpcbind
    lrwxrwxrwx   1 root root   20 Oct  9  2017 K07networking -> ../init.d/networking
    lrwxrwxrwx   1 root root   18 Oct  9  2017 K08umountfs -> ../init.d/umountfs
    lrwxrwxrwx   1 root root   20 Oct  9  2017 K09cryptdisks -> ../init.d/cryptdisks
    lrwxrwxrwx   1 root root   26 Oct  9  2017 K10cryptdisks-early -> ../init.d/cryptdisks-early
    lrwxrwxrwx   1 root root   20 Oct  9  2017 K11umountroot -> ../init.d/umountroot
    lrwxrwxrwx   1 root root   24 Oct  9  2017 K12mdadm-waitidle -> ../init.d/mdadm-waitidle
    lrwxrwxrwx   1 root root   16 Oct  9  2017 K13reboot -> ../init.d/reboot
    -rw-r--r--   1 root root  351 Jan 19  2016 README

#### These scripts are linked to the processes in `/etc/init.d/`

#### When shutting down a system, use the following command from the root user to shutdown specifying an amount of time and entering a message which will be printed on all other users tty session.

* `root $ shutdown -r 1 "System rebooting for minor updates"` - `-r` is reboot, if you just want to shutdown the host use `-h` for halt. `

### Systemd

#### Systemd is the first and last process loaded by the system, starting with pid 1. The first systemd related file that is loaded lives at `/etc/systemd/system/default.target`

#### To find the default system.d action, run the following

* `root $ systemctl get-default`

        multi-user.target (depending on what run-level)

### Scheduling tasks with Crontab

#### Useful for routine tasks, such as running a script to backup the system

#### Crontab is run under a service named cronie, to check you have the service installed, run rpm -q cronie

        *       *       *       *       *       command to be executed

        |       |       |       |       |
        |       |       |       |       |
        minute (0-59)   |       |       |
                |       |       |       |
            hour(0-23)  |       |       |
                        |       |       |
              day of month(1-31)|       |
                                |       |
                        month(1-12)     |
                                        |
                                day of the week
                                (0-6)

#### To create a cronjob with the above configuration, start with

* `$ crontab -u user -e` - where user is the cronjob you want to run under that user

#### List cron jobs

* `root $ crontab -l` - list all cron tasks for the current user
* `root $ crontab -l -u user` - list all cron jobs for the "user" with the `-u` flag

#### Crontab example

* `0 5,17 * * * /scripts/script.sh` - Run the script within /scripts at 5 AM and 5 PM everyday.

### Shell Scripts

* Using shell commands to 'automate' jobs
* Bash is the default shell on *most* linux distros
* "Easy" to use
* Best and common practice is to start a bash script with an interpreter `#!/bin/bash` where `/bin/bash` is the path to my bash installation
* bash script commonly end with `.sh`
* Bash scripts must be executable `chmod 755 bash_script.sh`

### Processes

#### Process Types

* Parent Process
* Child Process

#### Child process is a process started and is running *underneath* a parent process

* Orphan Process

#### Orphan process still runs after the parent process has be terminated

* Daemon Process

#### Always created from a child process then the parent process is stopped, the daemon process runs in the background

* Zombie Process

#### Process that exists within the process table, although it has been terminated

#### Free command

* `$ free -m` - show the current usage of memory within a system

#### The above command will display current memory usage, displaying both used, total and free for both physical memory and swap memory. Swap memory is used as an overflow mechanism if the available memory starts to look a bit swamped

#### To view the swap drive is use

* `$ cat /proc/swaps` - display disk information with the swap drive.

#### The threshold for using the swap disk is set within `/proc/sys/vm/swappiness` if the number set within this file is `10`, that means the physical memory will start to use the swap disk when it reaches `90` percent. There are a number of ways to change this value, to temporarily change the value use

* `root $ sysctl -w vm.swappiness=50` - Temporarily increase the threshold of when the swap disk is used

#### To set the threshold more permanently

* `root $ vi /etc/sysctl.conf` - Make a change to the system kernel to increase or decrease the swap threshold

### VMStat

#### `vmstat` is used to display all active stats about the current state of the linux system

* `root $ vmstat`

        procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
        r  b   swpd   free  inact active   si   so    bi    bo   in   cs us sy id wa st
        0  0   8284 195752 766520 869068    0    0     1     3   12   16  0  0 100  0  0

* `root $ vmstat 2 5` - poll the vmstat command

#### Another command also used when monitoring linux systems is `top`. Top monitors and displays in *realtime* all of the system processes as well as system information such as memory and cpu usage

#### Another tool used by linux systems is `ps`. ps combined with `grep` is easy to use and quickly shows you if a process is running and the system information

#### Another notable command to use is `nice`. By using `nice` you can set the priority of the command/script in question

### Using the `nice` command

#### **Description** The Nice/Renice command is a command which allows the use of prioritising processes running within the linux system

* `root $ nice -n number process` - increase the priority of process by number
* `root $ renice -n number process` - decrease the priority of the running process by number

### Using the `kill` command

#### Using the kill command, enables the shutting down of a process this can be complete both with force (not recommended) and with "safe" shutdown of a process

* `root $ kill -1 process ID` - "gracefully" shut down process ID
* `root S kill -9 process ID` - "force" a shutdown of process ID

#### Another related command to kill is `pkill` this is a __safer__ way to kill a service that is running

* `root & pkill -9 serviceName' - force the killing of the service name

#### I tool I prefer to use when managing and monitoring processes is `pgrep`. Pgrep looks through the currently running processes and list process ID

### Package Managers

#### A package manager or package management system is a collection of software tools that automates the process of installing, upgrading, configuring, and removing computer programs for a computer's operating system in a consistent manner. Redhat's default package manager is RPM (RedHat package manager) although more commonly used is YUM (yellowdog updater modified) as it includes more repository based packages

* `$ rpm -qa` - List all of the installed packages on a RedHat based system
* `$ yum list installed` - List all pf the installed packages using yum
* `$ yum remove package-name` - Remove package-name

#### A commonly used extended package manager tool is `yum-utils`

* `$ repoquery -a --installed` - list all installed packages using yum-utils package

#### APT - is the frontend package management system for `dkpg` and debian based system

* `root $ apt-get install package-name` - installing a package on debian based systems
* `root $ apt-get remove package-name` - This will remove the package but leave the existing configuration files
* `root $ apt-get purge package-name` - Remove the package and the configuration files associated with it
* `root $ apt-cache search package-name` - search for the package-name package list the description of the package

### Changing the kernel run-time parameters

#### Through use of the `sysctl` command the kernel run-time system can be modified

* `root $ sysctl -a | wc -l` - return the number of current kernel run time parameters
* `root $ systctl dev.cdrom.auto_close` - will display the current value set on dev.cdrom.auto_close
* `root $ echo "0" > /proc/sys/dev/cdrom/autoclose` - set the state of auto close to false at runtime
* `root $ vi /etc/sysctl.conf` - append the configuration you want to overwrite on boot. For example, `dev.cdrom.autoclose=0` will set the autoclose to false

### Identifying files that a package belongs too

#### Redhat

* `root $ rpm -qf file-name` - list what package file-name belongs too
* `root $ rpm -ql package-name.version-number` - list what files are associated with package-name.version-name
* `root $ yum, whatprovides package-path` - list all related files associated with this package-name

#### Debian

* `root $ dpkg -S package-path` - display where the file is located
* `root $ dpkg -L package-name` - display all the files associated with package-name

### Locate and analyse system log files

#### Default location of log files are at `/var/log/`

* `root $ tailf logfile-path` - follow the logfile-path log