---
tags:
  - "#MOC"
  - "#Module"
platform: "[[Hack The Box]]"
difficulty: Fundamental
tier: I
banner: "![[linux_fundamentals_banner.webp]]"
status: Incomplete
aliases:
  - Linux
---
>[!warning]-
>Some parts of this note are just a copy-pasted or incomplete information, because I'm already familiar with the topic. Some parts are important, so I marked them with a Important Tag

> [!danger]- Associated Certs
> - [[CREST CPSA CRT|CREST Practitioner Security Analyst]]
> - [[HTB CJCA|HTB Certified Junior Cybersecurity Associate]]
^faq

> [!faq]- Associated Paths
> - [[Operating System Fundamentals]]
> - [[CREST CPSA/CRT Preparation]]
> - [[CREST CCT APP Preparation]]
> - [[Information Security Foundations]]
> - [[CREST CCT INF Preparation]]
> - [[SOC Analyst Prerequisites]]
> - [[Junior Cybersecurity Analyst]]
^faq

> [!summary] Linux Fundamentals Summary
> Linux is an indispensable tool and system in the field of cybersecurity. Many servers run on Linux and offer a wide range of possibilities for offensive security practitioners, network defenders, and systems administrators. This module covers the essentials for starting with the Linux operating system and terminal.

> [!FLag] In this module, we will cover:
> - Linux structure
>- Using the shell
>- Navigating the Linux operating system
>- Working with files and directories
>- Linux administration
>- Service management
>- Permissions management
>

^summary
>[!tldr]- Cheat Sheet
![[Linux_Fundamentals_Module_Cheat_Sheet.pdf]]

# Sections
## 1. Linux structure
#### Philosophy
>The Linux philosophy centers on simplicity, modularity, and openness. The programs only have a single purpose: to perform one task well. These programs can be combined to accomplish complex operations.

| **Principle**                                                   | **Description**                                                                                                                                                |
| --------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Everything is a file**                                        | All configuration files for the various services running on the Linux operating system are stored in one or more text files.                                   |
| **Small, single-purpose programs**                              | Linux offers many different tools that we will work with, which can be combined to work together.                                                              |
| **Ability to chain programs together to perform complex tasks** | The integration and combination of different tools enable us to carry out many large and complex tasks, such as processing or filtering specific data results. |
| **Avoid captive user interfaces**                               | Linux is designed to work mainly with the shell (or terminal), which gives the user greater control over the operating system.                                 |
| **Configuration data stored in a text file**                    | An example of such a file is the `/etc/passwd` file, which stores all users registered on the system.                                                          |

####  Components

| **Component**     | **Description**                                                                                                                                                                                                                                                                                                                                 |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Bootloader`      | A piece of code that runs to guide the booting process to start the operating system. Parrot Linux uses the GRUB Bootloader.                                                                                                                                                                                                                    |
| `OS Kernel`       | The kernel is the main component of an operating system. It manages the resources for system's I/O devices at the hardware level.                                                                                                                                                                                                               |
| `Daemons`         | Background services are called "daemons" in Linux. Their purpose is to ensure that key functions such as scheduling, printing, and multimedia are working correctly. These small programs load after we booted or log into the computer.                                                                                                        |
| `OS Shell`        | The operating system shell or the command language interpreter (also known as the command line) is the interface between the OS and the user. This interface allows the user to tell the OS what to do. The most commonly used shells are Bash, Tcsh/Csh, Ksh, Zsh, and Fish.                                                                   |
| `Graphics server` | This provides a graphical sub-system (server) called "X" or "X-server" that allows graphical programs to run locally or remotely on the X-windowing system.                                                                                                                                                                                     |
| `Window Manager`  | Also known as a graphical user interface (GUI). There are many options, including GNOME, KDE, MATE, Unity, and Cinnamon. A desktop environment usually has several applications, including file and web browsers. These allow the user to access and manage the essential and frequently accessed features and services of an operating system. |
| `Utilities`       | Applications or utilities are programs that perform particular functions for the user or another program.                                                                                                                                                                                                                                       |

#### Linux Architecture
The Linux operating system can be broken down into layers:

| **Layer**        | **Description**                                                                                                                                                                                                                                                                                    |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Hardware`       | Peripheral devices such as the system's RAM, hard drive, CPU, and others.                                                                                                                                                                                                                          |
| `Kernel`         | The core of the Linux operating system whose function is to virtualize and control common computer hardware resources like CPU, allocated memory, accessed data, and others. The kernel gives each process its own virtual resources and prevents/mitigates conflicts between different processes. |
| `Shell`          | A command-line interface (**CLI**), also known as a shell that a user can enter commands into to execute the kernel's functions.                                                                                                                                                                   |
| `System Utility` | Makes available to the user all of the operating system's functionality.                                                                                                                                                                                                                           |
#### File System Hierarchy

The Linux operating system is structured in a tree-like hierarchy and is documented in the [Filesystem Hierarchy](http://www.pathname.com/fhs/) Standard (FHS). Linux is structured with the following standard top-level directories:

![Diagram of Linux file system hierarchy with root directory branching to folders: /bin, /boot, /dev, /etc, /lib, /media, /mnt, /opt, /home, /run, /root, /proc, /sys, /tmp, /usr, /var.](https://academy.hackthebox.com/storage/modules/18/NEW_filesystem.png)

| **Path** | **Description**                                                                                                                                                                                                                                                                                                                    |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/`      | The top-level directory is the root filesystem and contains all of the files required to boot the operating system before other filesystems are mounted, as well as the files required to boot the other filesystems. After boot, all of the other filesystems are mounted at standard mount points as subdirectories of the root. |
| `/bin`   | Contains essential command binaries.                                                                                                                                                                                                                                                                                               |
| `/boot`  | Consists of the static bootloader, kernel executable, and files required to boot the Linux OS.                                                                                                                                                                                                                                     |
| `/dev`   | Contains device files to facilitate access to every hardware device attached to the system.                                                                                                                                                                                                                                        |
| `/etc`   | Local system configuration files. Configuration files for installed applications may be saved here as well.                                                                                                                                                                                                                        |
| `/home`  | Each user on the system has a subdirectory here for storage.                                                                                                                                                                                                                                                                       |
| `/lib`   | Shared library files that are required for system boot.                                                                                                                                                                                                                                                                            |
| `/media` | External removable media devices such as USB drives are mounted here.                                                                                                                                                                                                                                                              |
| `/mnt`   | Temporary mount point for regular filesystems.                                                                                                                                                                                                                                                                                     |
| `/opt`   | Optional files such as third-party tools can be saved here.                                                                                                                                                                                                                                                                        |
| `/root`  | The home directory for the root user.                                                                                                                                                                                                                                                                                              |
| `/sbin`  | This directory contains executables used for system administration (binary system files).                                                                                                                                                                                                                                          |
| `/tmp`   | The operating system and many programs use this directory to store temporary files. This directory is generally cleared upon system boot and may be deleted at other times without any warning.                                                                                                                                    |
| `/usr`   | Contains executables, libraries, man files, etc.                                                                                                                                                                                                                                                                                   |
| `/var`   | This directory contains variable data files such as log files, email in-boxes, web application related files, cron files, and more.                                                                                                                                                                                                |
## 2. Linux Distributions
> [!info] 
> Linux distributions - or distros - are operating systems based on the Linux kernel. They are used for various purposes, from servers and embedded devices to desktop computers and mobile phones. Linux distributions are like different branches or franchises of the same company, each tailored to serve specific markets or customer preferences. While they all share the same dedicated employees (components), organizational structure (architecture), and corporate culture (philosophy), each distribution offers its own unique products and services (software packages and configurations), customizing the experience to meet diverse needs—all while operating under the unified brand and values of Linux. Each Linux distribution is different, with its own set of features, packages, and tools. 

Some popular examples include:
- [Ubuntu](https://ubuntu.com/)
- [Fedora](https://getfedora.org/)
- [CentOS](https://www.centos.org/)
- [Debian](https://www.debian.org/)
- [Red Hat Enterprise Linux](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux)

## 3. Introduction to Shell

It is crucial to learn how to use the Linux shell, as there are many servers based on Linux. These are often used because Linux is less error-prone as opposed to Windows servers. For example, web servers are often based on Linux. Knowing how to use the operating system to control it effectively requires understanding and mastering Linux’s essential part, the `Shell`. When we first switched from Windows to Linux, does it look something like this:

![Parrot Terminal showing command prompt with user 'user6@htb-wpjudq32ze' and command 'okay google' entered.](https://academy.hackthebox.com/storage/modules/18/first_linux2.png)

## 4. Prompt Description

The bash prompt is simple to understand. By default, it shows information like your username (who you are), your computer's name (hostname), and the folder/directory you're currently working in. It's a line of text that appears on the screen to let you know the system is ready for you. The prompt appears on a new line, and the cursor (the blinking line or box) is placed right after it, waiting for you to type a command.

It can be customized to provide useful information to the user. The format can look something like this:

  Prompt Description

```shell-session
<username>@<hostname><current working directory>$
```

The home directory for a user is marked with a tilde <`~`> and is the default folder when we log in.

  Prompt Description

```shell-session
<username>@<hostname>[~]$
```

The dollar sign, in this case, stands for a user. As soon as we log in as `root`, the character changes to a `hash` <`#`> and looks like this:

  Prompt Description

```shell-session
root@htb[/htb]#
```



## 5. Getting Help
Having established a solid foundation in Linux's structure, its various distributions, and the purpose of the shell, we're now prepared to put this knowledge into action. It's time to dive in, using commands directly in the terminal, as well as learning how to seek help when we encounter unfamiliar ones.

We will always stumble across tools whose optional parameters we do not know from memory or tools we have never seen before. Therefore it is vital to know how we can help ourselves to get familiar with those tools. The first two ways are the man pages and the help functions. It is always a good idea to familiarize ourselves with the tool we want to try first. We will also learn some possible tricks with some of the tools that we thought were not possible. In the man pages, we will find the detailed manuals with detailed explanations.


## 6. System Information
>[!warning] Important!
^important

Now, let’s dive into some hands-on practice to get comfortable with using the terminal and the shell. Keep in mind that you can always use the `-h`, `--help`, or man commands to access help if needed.

Since we’ll be working with various Linux systems, it's important to understand their structure, including system details, processes, network configurations, users/user settings, and directories, along with their related parameters. Below is a list of essential tools to help gather this information. Most of these tools come pre-installed. However, this knowledge is not only crucial for routine Linux tasks, but also plays a key role when assessing security configurations, identifying vulnerabilities, or preventing potential security risks in Linux operating systems.

| **Command** | **Description**                                                                                                                    |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `whoami`    | Displays current username.                                                                                                         |
| `id`        | Returns users identity                                                                                                             |
| `hostname`  | Sets or prints the name of current host system.                                                                                    |
| `uname`     | Prints basic information about the operating system name and system hardware.                                                      |
| `pwd`       | Returns working directory name.                                                                                                    |
| `ifconfig`  | The ifconfig utility is used to assign or to view an address to a network interface and/or configure network interface parameters. |
| `ip`        | Ip is a utility to show or manipulate routing, network devices, interfaces and tunnels.                                            |
| `netstat`   | Shows network status.                                                                                                              |
| `ss`        | Another utility to investigate sockets.                                                                                            |
| `ps`        | Shows process status.                                                                                                              |
| `who`       | Displays who is logged in.                                                                                                         |
| `env`       | Prints environment or sets and executes command.                                                                                   |
| `lsblk`     | Lists block devices.                                                                                                               |
| `lsusb`     | Lists USB devices                                                                                                                  |
| `lsof`      | Lists opened files.                                                                                                                |
| `lspci`     | Lists PCI devices.                                                                                                                 |

Let us scroll to the bottom of the page, spawn the target machine, then connect to it using SSH. Then, try to follow along and reproduce as many of the example shown in the section.

#### Logging In via SSH
`Secure Shell` (`SSH`) refers to a protocol that allows remote access through a CLI. It doesn't require a graphical interface, which makes it highly effective for server management.

We can connect to a SSH server using the next command:
```sh ln:false
skkippie@x0rs3us$ ssh htb-student@<IP address> 
```

##### Hostname
The `{sh icon}hostname` command only prints the name of the computer which we logged into.

```sh ln:false
htb-student@<IP>$ hostname
nixfund
```

##### Whoami
The `{sh icon} whoami` command prints the username of the current user.

```sh ln:false
htb-student@<IP>$ whoami
htb-student
```

##### Id
The `{sh icon}id` command is similar to `{sh icon}whoami` but it provides more detailed info like group mermbership and IDs. This information are important for [[Penetration Tester|Penetration Testers]]  because they would see what access a user may have, and sysadmins looking to audit account permissions and group memberships.  

```sh ln:false
htb-student@<IP>$ id
uid=1000(cry0l1t3) gid=1000(cry0l1t3) groups=1000(cry0l1t3),1337(hackthebox),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),116(lpadmin),126(sambashare)
```

##### Uname
>[!tldr] `{sh icon}tldr` command
>I prefer `{sh icon}tldr` because it provides descriptions of the flags used with a command
>For example:
>```sh ln:false
>skkippie@x0rs3us $ tldr uname
>  - Print kernel name:
>    uname
 > - Print all available system information:
 >   uname --all
>
 > - Print system architecture and processor information:
>   uname --machine --processsor
>
 > - Print kernel name, kernel release and kernel version:
>    uname --kernel-name --kernel-release --kernel-version
>
 > - Print system hostname:
 >   uname --nodename
>
 > - Print the current operating system name:
 >   uname --operating-system
>
 > - Print the current network node host name:
>   uname --nodename
>
 > - Display help:
 >   uname --help
>```

Let's dig into the `{sh icon}uname` command a bit more. If we type `{sh icon}man uname` in our terminal, we will bring up the man page for the command, which will show the possible options we can run with the command and the results.

> Practical part, I already do it. 

# Workflow
## 7. Navigation
Navigation is essential, like working with the mouse as a standard Windows user. With it, we move across the system and work in directories and with files, we need and want. Therefore, we use different commands and tools to print out information about a directory or a file and can use advanced options to optimize the output to our needs.

One of the best ways to learn something new is to experiment with it. Here we cover the sections on navigating through Linux, creating, moving, editing, and deleting files and folders, finding them on the operating system, different types of redirects, and what file descriptors are. We will also find shortcuts to make our work with the shell much easier and more comfortable. We recommend experimenting on our locally hosted VM. Ensure we have created a snapshot for our VM in case our system gets unexpectedly damaged.

Let us start with the navigation. Before we move through the system, we have to find out in which directory we are. We can find out where we are with the command `pwd`.

#### Lab
^important
>[!tip] Questions
>1. What is the name of the hidden "history" file in the htb-user's home directory?
>	The command `{sh icon} ls -a` return all files included hidden files.
>```sh ln:false
>htb-student@nixfund:~$ ls -a
.  ..  .bash_history  .bash_logout  .bashrc  .cache  .gnupg  .profile
>```
>There is .bash_history.
>2. What is the index number of the "sudoers" file in the "/etc" directory?
>```sh ln:false
>htb-student@nixfund:/$ ls -i /etc/sudoers
147627 /etc/sudoers
>```
>The index number is 147627

## 8. Working with Files and Directories
Some utilities like `{sh icon}cp` `{sh icon}mv` `{sh icon}touch` but the lab need  `{sh icon}ls -lti` to solve.

## 9. Editing Files
After learning how to create files and directories, let’s move on to working with these files. There are several ways to edit a file in Linux, with some of the most common text editors being `Vi` and `Vim`. However, we will start with the `Nano` editor, which is less commonly used but easier to understand.

To create and edit a file using Nano, you can specify the file name directly as the first parameter when launching the editor. For example, to create and open a new file named `notes.txt`, you would use the following command:
```shell-session ln:false
Skkippie@htb[/htb]$ nano notes.txt
```
## 10. Find Files and Directories
It's crucial to be able to find files and directories we need.
#### Which
This command shows the path of a binary
```shell-session ln:false
Skkippie@htb[/htb]$ which python
/usr/bin/python
```
#### Find
This command searches through all the system files and folders.
```shell-session ln:false
Skkippie@htb[/htb]$ find <location> <options>
```

For example:
```shell-session ln:false
Skkippie@htb[/htb]$ find / -type f -name *.conf -user root -size +20k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null

-rw-r--r-- 1 root root 136392 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/auto.conf
-rw-r--r-- 1 root root 82290 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/tristate.conf
-rw-r--r-- 1 root root 95813 May  7 14:33 /usr/share/metasploit-framework/data/jtr/repeats32.conf
-rw-r--r-- 1 root root 60346 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dynamic.conf
-rw-r--r-- 1 root root 96249 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dumb32.conf
-rw-r--r-- 1 root root 54755 May  7 14:33 /usr/share/metasploit-framework/data/jtr/repeats16.conf
-rw-r--r-- 1 root root 22635 May  7 14:33 /usr/share/metasploit-framework/data/jtr/korelogic.conf
-rwxr-xr-x 1 root root 108534 May  7 14:33 /usr/share/metasploit-framework/data/jtr/john.conf
-rw-r--r-- 1 root root 55285 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dumb16.conf
-rw-r--r-- 1 root root 21254 May  2 11:59 /usr/share/doc/sqlmap/examples/sqlmap.conf
-rw-r--r-- 1 root root 25086 Mar  4 22:04 /etc/dnsmasq.conf
-rw-r--r-- 1 root root 21254 May  2 11:59 /etc/sqlmap/sqlmap.conf
```

| **Option**            | **Description**                                                                                                                                                                                                                                                                |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `-type f`             | Hereby, we define the type of the searched object. In this case, '`f`' stands for '`file`'.                                                                                                                                                                                    |
| `-name *.conf`        | With '`-name`', we indicate the name of the file we are looking for. The asterisk (`*`) stands for 'all' files with the '`.conf`' extension.                                                                                                                                   |
| `-user root`          | This option filters all files whose owner is the root user.                                                                                                                                                                                                                    |
| `-size +20k`          | We can then filter all the located files and specify that we only want to see the files that are larger than 20 KiB.                                                                                                                                                           |
| `-newermt 2020-03-03` | With this option, we set the date. Only files newer than the specified date will be presented.                                                                                                                                                                                 |
| `-exec ls -al {} \;`  | This option executes the specified command, using the curly brackets as placeholders for each result. The backslash escapes the next character from being interpreted by the shell because otherwise, the semicolon would terminate the command and not reach the redirection. |
| `2>/dev/null`         | This is a `STDERR` redirection to the '`null device`', which we will come back to in the next section. This redirection ensures that no errors are displayed in the terminal. This redirection must `not` be an option of the 'find' command.                                  |
#### Locate
In contrast to the `{sh icon}find` command, this one searches a local database that contains all information about existing files and folders.
To update this database, we can execute this command.
```shell-session ln:false
sudo updatedb
```

If were now search for all files with the `*.conf` extension, you will find that this search produces results much faster than using `{sh icon}find`.

## 11.  File Descriptors and Redirections
#### File Descriptors
File descriptors are system's way of keeping track of active I/O connections, such as reading from or writing to a file.
On Linux, the first three file descriptors are:
- STDIN - 0
- STDOUT - 1
- STDERR - 2
STDIN is the standard Input
STDOUT is the standard output
STDERR is the standard error management

#### Redirections
The operator `>` redirects the STD to anything, for example if we want to redirect errors to the null device, we use `{sh icon}2>/dev/null`, or if we want to redirect the standard output we can use `{sh icon}> output.txt`. Also we can use `1` like the STDERR: 
`{sh icon}find / -type f -name 'shadow' 2>/dev/null 1> output.txt`
And, for STDIN we use `<` operator. for example
`{sh icon}cat < stdin.txt`

>[!warning]
> When we use `>` operator, a new file is created, if already exists, it will overwrite the file without asking for confirmation.
>To append the STDOUT to the file, we use `>>` 

#### Streams
We can use the `<<` operator to provide our standard input through a stream, we can use a special word, for example EOF which is a convention for End-Of-File, and then can write lines until we write the delimiter EOF.
```sh-session ln:false
  │ skkippie@x0rs3us │  ~  cat << ASD                                                 
skkippie@x0rs3us ~ heredoc> asd
skkippie@x0rs3us ~ heredoc> asd
skkippie@x0rs3us ~ heredoc> asd
skkippie@x0rs3us ~ heredoc> asd
skkippie@x0rs3us ~ heredoc> ASD             
   1   │ asd
   2   │ asd
   3   │ asd
   4   │ asd            
```

We can also combine operators, for example: 
```sh-session ln:false
  │ skkippie@x0rs3us │  ~  cat << ASD > output.txt                                    
skkippie@x0rs3us ~ heredoc> asd
skkippie@x0rs3us ~ heredoc> asd
skkippie@x0rs3us ~ heredoc> asd
skkippie@x0rs3us ~ heredoc> asd
skkippie@x0rs3us ~ heredoc> ASD             
   1   │ asd
   2   │ asd
   3   │ asd
   4   │ asd     
  │ skkippie@x0rs3us │  ~  cat output.txt
   1   │ asd
   2   │ asd
   3   │ asd
   4   │ asd  
```

>[!important] 
>Modern Bash uses the `&` operator to refer STDOUT and STDERR(only in FD operations), so we can redirect both to anything, for example:
>`{sh icon} sudo openvpn academic.ovpn &>/dev/null &`
>The `&` operator also mean *move to background* in no FD operations.
>Don't confuse `&` and `&&` operators, the second means execute other command only if first success, for example:
>`{sh icon}mkdir folder && cd folder`
 
#### Pipes
A pipe `|` is a way to pass the STDOUT of one command to another, for example
`{sh icon}strings image.jpg | grep -i flag`.

## 12. Filter Contents
We going to talk about how to open files in the cli without needing a text editor
#### More
```shell-session ln:false
Skkippie@htb[/htb]$ cat /etc/passwd | more
```

After we read the content using `cat` and redirected it to `more`, the already mentioned `pager` opens, and we will automatically start at the beginning of the file.

#### Less
If we now take a look at the tool `less`, we will notice on the man page that it contains many more features than `more`.

```shell-session ln:false
Skkippie@htb[/htb]$ less /etc/passwd
```

The presentation is almost the same as with `more`.

#### Head
Sometimes we will only be interested in specific issues either at the beginning of the file or the end. If we only want to get the `first` lines of the file, we can use the tool `head`. By default, `head` prints the first ten lines of the given file or input, if not specified otherwise.

```shell-session ln:false
Skkippie@htb[/htb]$ head /etc/passwd

root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
```

#### Tail
If we only want to see the last parts of a file or results, we can use the counterpart of `head` called `tail`, which returns the `last` ten lines.

```shell-session ln:false
Skkippie@htb[/htb]$ tail /etc/passwd

miredo:x:115:65534::/var/run/miredo:/usr/sbin/nologin
usbmux:x:116:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
rtkit:x:117:119:RealtimeKit,,,:/proc:/usr/sbin/nologin
nm-openvpn:x:118:120:NetworkManager OpenVPN,,,:/var/lib/openvpn/chroot:/usr/sbin/nologin
nm-openconnect:x:119:121:NetworkManager OpenConnect plugin,,,:/var/lib/NetworkManager:/usr/sbin/nologin
pulse:x:120:122:PulseAudio daemon,,,:/var/run/pulse:/usr/sbin/nologin
beef-xss:x:121:124::/var/lib/beef-xss:/usr/sbin/nologin
lightdm:x:122:125:Light Display Manager:/var/lib/lightdm:/bin/false
do-agent:x:998:998::/home/do-agent:/bin/false
user6:x:1000:1000:,,,:/home/user6:/bin/bash
```

#### Sort
Depending on which results and files are dealt with, they are rarely sorted. Often it is necessary to sort the desired results alphabetically or numerically to get a better overview. For this, we can use a tool called `sort`.

```shell-session ln:false
Skkippie@htb[/htb]$ cat /etc/passwd | sort

_apt:x:104:65534::/nonexistent:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
cry0l1t3:x:1001:1001::/home/cry0l1t3:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
dnsmasq:x:107:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
dovecot:x:114:117:Dovecot mail server,,,:/usr/lib/dovecot:/usr/sbin/nologin
dovenull:x:115:118:Dovecot login user,,,:/nonexistent:/usr/sbin/nologin
ftp:x:113:65534::/srv/ftp:/usr/sbin/nologin
games:x:5:60:games:/usr/games:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
htb-student:x:1002:1002::/home/htb-student:/bin/bash
<SNIP>
```

As we can see now, the output no longer starts with root but is now sorted alphabetically.

#### Grep

In many cases, we will need to search for specific results that match patterns we define. One of the most commonly used tools for this purpose is grep, which provides a wide range of powerful features for pattern searching. For instance, we can use grep to search for users who have their default shell set to `/bin/bash`.

```shell-session ln:false
Skkippie@htb[/htb]$ cat /etc/passwd | grep "/bin/bash"

root:x:0:0:root:/root:/bin/bash
mrb3n:x:1000:1000:mrb3n:/home/mrb3n:/bin/bash
cry0l1t3:x:1001:1001::/home/cry0l1t3:/bin/bash
htb-student:x:1002:1002::/home/htb-student:/bin/bash
```

This is just one example of how grep can be applied to efficiently filter data based on predefined patterns. Another possibility is to exclude specific results. For this, the option "`-v`" is used with `grep`. In the next example, we exclude all users who have disabled the standard shell with the name "`/bin/false`" or "`/usr/bin/nologin`".

  Filter Contents

```shell-session ln:false
Skkippie@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin"

root:x:0:0:root:/root:/bin/bash
sync:x:4:65534:sync:/bin:/bin/sync
postgres:x:111:117:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
user6:x:1000:1000:,,,:/home/user6:/bin/bash
```

#### Cut
Cut is used for putting a delimiter in the STDOUT with the `-d` flag, and with the `-f<n>` flag choose a field.
```shell-session ln:False
Skkippie@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | cut -d":" -f1

root
sync
postgres
mrb3n
cry0l1t3
htb-student
```
#### Tr
This tool replace a string with another string.
```shell-session ln:false
Skkippie@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " "

root x 0 0 root /root /bin/bash
sync x 4 65534 sync /bin /bin/sync
postgres x 111 117 PostgreSQL administrator,,, /var/lib/postgresql /bin/bash
mrb3n x 1000 1000 mrb3n /home/mrb3n /bin/bash
cry0l1t3 x 1001 1001  /home/cry0l1t3 /bin/bash
htb-student x 1002 1002  /home/htb-student /bin/bash
```

#### Column
If the output seems weird, we can use column with the flag `-t` to tabulate the output.
```shell-session ln:false
Skkippie@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | column -t

root         x  0     0      root               /root        		 /bin/bash
sync         x  4     65534  sync               /bin         		 /bin/sync
postgres     x  111   117    PostgreSQL         administrator,,,    /var/lib/postgresql		/bin/bash
mrb3n        x  1000  1000   mrb3n              /home/mrb3n  	     /bin/bash
cry0l1t3     x  1001  1001   /home/cry0l1t3     /bin/bash
htb-student  x  1002  1002   /home/htb-student  /bin/bash
```

#### Awk
`awk` command is used for transforming and filtering data from a column, the syntax is `awk 'pattern { action }' file`
`NF` refers to last column.
```shell-session ln:false
Skkippie@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}'

root /bin/bash
sync /bin/sync
postgres /bin/bash
mrb3n /bin/bash
cry0l1t3 /bin/bash
htb-student /bin/bash
```

#### Sed
Sed can change some parts of the filtered data. The "`s`" flag at the beginning stands for the substitute command. Then we specify the pattern we want to replace. After the slash (`/`), we enter the pattern we want to use as a replacement in the third position. Finally, we use the "`g`" flag, which stands for replacing all matches.

```shell-session ln:false
Skkippie@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | sed 's/bin/HTB/g'

root /HTB/bash
sync /HTB/sync
postgres /HTB/bash
mrb3n /HTB/bash
cry0l1t3 /HTB/bash
htb-student /HTB/bash
```

#### Wc
Last but not least, it will often be useful to know how many successful matches we have. To avoid counting the lines or characters manually, we can use the tool `wc`. With the "`-l`" option, we specify that only the lines are counted.

```shell-session ln:false
Skkippie@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | wc -l

6
```

## 13. Regular Expressions
RegEx is available in many programming languages and tools, such as grep or sed, making it a versatile and powerful tool in a our toolkit.
#### Grouping
Among other things, regex offers us the possibility to group the desired search patterns. Basically, regex follows three different concepts, which are distinguished by the three different brackets:

##### Grouping Operators

|     | **Operators** | **Description**                                                                                                                                                             |
| --- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | `(a)`         | The round brackets are used to group parts of a regex. Within the brackets, you can define further patterns which should be processed together.                             |
| 2   | `[a-z]`       | The square brackets are used to define character classes. Inside the brackets, you can specify a list of characters to search for.                                          |
| 3   | `{1,10}`      | The curly brackets are used to define quantifiers. Inside the brackets, you can specify a number or a range that indicates how often a previous pattern should be repeated. |
| 4   | `\|`          | Also called the OR operator and shows results when one of the two expressions matches                                                                                       |
| 5   | `.*`          | Operates similarly to an AND operator by displaying results only when both expressions are present and match in the specified order                                         |

#### OR operator
`|`

```shell-session ln:false
cry0l1t3@htb:~$ grep -E "(my|false)" /etc/passwd

lxd:x:105:65534::/var/lib/lxd/:/bin/false
pollinate:x:109:1::/var/cache/pollinate:/bin/false
mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```

#### AND operator
`.*`
```shell-session
cry0l1t3@htb:~$ grep -E "(my.*false)" /etc/passwd

mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```

//TODO learn more RegEx

## 14. Permission Management
In Linux, the permissions are like keys that control the access to files and directories. These permissions are assigned to users and groups.

Each file have an owner and is associated with a group.

To moving through a directory, the user must have `execute` permission.

`execute` permission in DIRECTORIES only allows to move through the directory, the user can't modify, create or delete anything.

To execute some file within the directory, the user needs `execute` permission on the file. To modify create and delete files within the directory, the user needs `write` permission on the directory.

The whole permission system on Linux systems is based on the octal number system, and basically, there are three different types of permissions a file or directory can be assigned:

- (`r`) - Read
- (`w`) - Write
- (`x`) - Execute

The permissions can be set for the `owner`, `group`, and `others` like presented in the next example with their corresponding permissions.

```shell-session ln:false
cry0l1t3@htb[/htb]$ ls -l /etc/passwd

- rwx rw- r--   1 root root 1641 May  4 23:42 /etc/passwd
- --- --- ---   |  |    |    |   |__________|
|  |   |   |    |  |    |    |        |_ Date
|  |   |   |    |  |    |    |__________ File Size
|  |   |   |    |  |    |_______________ Group
|  |   |   |    |  |____________________ User
|  |   |   |    |_______________________ Number of hard links
|  |   |   |_ Permission of others (read)
|  |   |_____ Permissions of the group (read, write)
|  |_________ Permissions of the owner (read, write, execute)
|____________ File type (- = File, d = Directory, l = Link, ... )
```

#### Change Permissions
We can modify permissions using `chmod` command, permission group references (`u` - owner, `g` - Group, `o` - others, `a` - All users), and either a [+] or a [-] to add remove the designated permissions

We can then apply `read` permissions for all users and see the result.

```shell-session ln:false
cry0l1t3@htb[/htb]$ chmod a+r shell && ls -l shell

-rwxr-xr-x   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

We can also set the permissions for all other users to `read` only using the octal value assignment.

```shell-session ln:false
cry0l1t3@htb[/htb]$ chmod 754 shell && ls -l shell

-rwxr-xr--   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

Let us look at all the representations associated with it to understand better how the permission assignment is calculated.

```shell-session ln:false
Binary Notation:                4 2 1  |  4 2 1  |  4 2 1
----------------------------------------------------------
Binary Representation:          1 1 1  |  1 0 1  |  1 0 0
----------------------------------------------------------
Octal Value:                      7    |    5    |    4
----------------------------------------------------------
Permission Representation:      r w x  |  r - x  |  r - -
```

#### Change Owner
To change the owner and/or the group, we use `chown` command 

```shell-session ln:false
cry0l1t3@htb[/htb]$ chown <user>:<group> <file/directory>
```

In this example, "shell" can be replaced with any arbitrary file or folder.

```shell-session ln:false
cry0l1t3@htb[/htb]$ chown root:root shell && ls -l shell

-rwxr-xr--   1 root root 0 May  4 22:12 shell
```

#### SUID & SGID / Sticky Bit
Linux provides special permissions beyond the usual user and group settings: SUID, SGID, and the Sticky Bit.

- SUID/SGID: When set on a file, they make a program run with the permissions of the file’s owner or group instead of the user running it. This is useful for specific system tasks but risky if misused, as it can allow unintended privilege escalation.
    
- Sticky Bit: Applied to a directory, it ensures only the file’s owner, the directory owner, or root can delete or rename files, protecting shared folders. Lowercase `t` means others have execute permission; uppercase `T` means they don’t.


# System Management
## 15. 

# References
- [[Hack The Box]]
- [[HTB Module]]
