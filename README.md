# Learn WSL2

## Install Linux on Windows with WSL

<https://learn.microsoft.com/en-us/windows/wsl/install>

### Install WSL

> wsl \--install

    Windows Subsystem for Linux is already installed.
    The following is a list of valid distributions that can be installed.
    Install using 'wsl.exe --install <Distro>'.

    NAME               FRIENDLY NAME
    Ubuntu             Ubuntu
    Debian             Debian GNU/Linux
    kali-linux         Kali Linux Rolling
    SLES-12            SUSE Linux Enterprise Server v12
    SLES-15            SUSE Linux Enterprise Server v15
    Ubuntu-18.04       Ubuntu 18.04 LTS
    Ubuntu-20.04       Ubuntu 20.04 LTS
    OracleLinux_8_5    Oracle Linux 8.5
    OracleLinux_7_9    Oracle Linux 7.9

    The above command only works if WSL is not installed at all,
    if you run wsl --install and see the WSL help text, 
    please try running wsl --list --online to see a list of available distros 
    and run wsl --install -d <DistroName> to install a distro. 
    To uninstall WSL, see Uninstall legacy version of WSL or unregister or uninstall a Linux distribution.

### Uninstall WSL

> wsl \--unregister ubuntu-20.04-indra

### List of available Linux distributions

> wsl \--list \--online \|\| wsl -l -o

    NAME               FRIENDLY NAME
    Ubuntu             Ubuntu
    Debian             Debian GNU/Linux
    kali-linux         Kali Linux Rolling
    SLES-12            SUSE Linux Enterprise Server v12
    SLES-15            SUSE Linux Enterprise Server v15
    Ubuntu-18.04       Ubuntu 18.04 LTS
    Ubuntu-20.04       Ubuntu 20.04 LTS
    OracleLinux_8_5    Oracle Linux 8.5
    OracleLinux_7_9    Oracle Linux 7.9

### List installed Linux wsl

> wsl -l -v

     NAME                   STATE           VERSION
    * docker-desktop         Running         2
      ubuntu-shared-env      Running         2
      ubuntu-20.04-gui       Running         2
      docker-desktop-data    Running         2

### Open Linux distribution specific installed

> wsl -d ubuntu-20.04-indra

### Set the default Linux distribution

> wsl -s ubuntu-20.04-indra \|\| wsl \--setdefault ubuntu-20.04-indra

### Penginstallan WSL Normal

> wsl \--install Ubuntu

    Ubuntu is already installed.
    Launching Ubuntu...

    Installing, this may take a few minutes...
    Please create a default UNIX user account. The username does not need to match your Windows username.
    For more information visit: https://aka.ms/wslusers
    Enter new UNIX username: indra
    New password: *****
    Retype new password: *****
    passwd: password updated successfully
    Installation successful!
    To run a command as administrator (user "root"), use "sudo <command>".
    See "man sudo_root" for details.

    Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.79.1-microsoft-standard-WSL2 x86_64)

     * Documentation:  https://help.ubuntu.com
     * Management:     https://landscape.canonical.com
     * Support:        https://ubuntu.com/advantage

    This message is shown once a day. To disable it please create the
    /home/indra/.hushlogin file.

### Penginstallan WSL Custom

<https://learn.microsoft.com/en-us/windows/wsl/use-custom-distro>

### Export distribution yang telah di Custom

> wsl \--export ubuntu-20.04-indra ubuntu-20.04-indra.tar

### Create new Instance from Custom distribution

> wsl \--import ubuntu-20.04-indra .\\ubuntu-20.04-indra.tar

### Open specific distro and specific username

> wsl -d ubuntu-20.04-indra -u indra

### Update admin root password

    Jika belum ada user yang dibuat ditandai dengan *root@zwetan:* pada terminal.
    Set password baru untuk admin root:

    > passwd

    New password: *****
    Retype new password: *****
    passwd: password updated successfully

    Jika lupa password admin root, maka dapat force masuk dengan command berikut

    > wsl -d ubuntu-20.04-indra -u root

    Ulangi pembuatan password dengan command passwd

### Create new User

> sudo adduser indra

    Adding user `indra' ...
    Adding new group `indra' (1000) ...
    Adding new user `indra' (1000) with group `indra' ...
    Creating home directory `/home/indra' ...
    Copying files from `/etc/skel' ...
    New password:
    Retype new password:
    passwd: password updated successfully
    Changing the user information for indra
    Enter the new value, or press ENTER for the default
            Full Name []: Indra Mahkota
            Room Number []:
            Work Phone []:
            Home Phone []:
            Other []:
    Is the information correct? [Y/n] Y

### Check groups of user

> groups indra

    indra : indra

### Add user to sudoer group

> usermod -aG sudo indra

    indra : indra sudo

### List of User

> less /etc/passwd \|\| awk -F: \'{ print \$1}\' /etc/passwd \|\| cut
> -d: -f1 /etc/passwd

    root:x:0:0:root:/root:/bin/bash
    .
    .
    .
    indra:x:1000:1000:Indra Mahkota,,,:/home/indra:/bin/bash
    indramahkota:x:1001:1002:Indra Mahkota,,,:/home/indramahkota:/bin/bash

### Deleting User

> deluser indra

> deluser \--remove-home newuser // Remove all files related to user

    Looking for files to backup/remove ...
    Removing files ...
    Removing user `indra' ...
    Warning: group `indra' has no more members.
    userdel: user indra is currently used by process 401
    /usr/sbin/deluser: `/sbin/userdel indra' returned error code 8. Exiting.

### Set default user when open the WSL

    > Single command

    tee -a /etc/wsl.conf <<EOF
    [user]
    default=indra
    EOF

    or

    > vi /etc/wsl.conf

    [user]
    default=indra

**Jangan lupa terminate distronya**

> wsl \--terminate ubuntu-20.04-indra

### Ketika WSL di open kembali

    To run a command as administrator (user "root"), use "sudo <command>".
    See "man sudo_root" for details.

    Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.79.1-microsoft-standard-WSL2 x86_64)

     * Documentation:  https://help.ubuntu.com
     * Management:     https://landscape.canonical.com
     * Support:        https://ubuntu.com/advantage


    This message is shown once a day. To disable it please create the
    /home/indra/.hushlogin file.

**Penginstallan normal akan membuat user baru otomatis yang best
practice.** 

**Penginstallan dengan import distribution
tidak akan membuat user otomatis.**

## Set up a WSL development environment

<https://learn.microsoft.com/en-us/windows/wsl/setup/environment>

## Update and Upgrade the System

> sudo apt update && sudo apt upgrade
