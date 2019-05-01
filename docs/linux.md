# Linux

## Filesystem

In linux, there is only a single root filesystem. When you mount a partition,
you must choose an empty directory to mount it to. Windows mounts each partition
under it's own drive letter, giving you many separate filesystem trees. In
linux, there is only one tree, and when mounting a partition you must place it
somewhere in that tree.

Everything in linux is a file. There are regular files, the kind you already
know about, and there are a few other types. Running `ls -l` will list files
along with some additional information, like the type of file. The first letter
of each line indicates the type.

You can find more info on the linux filesystem here:

<https://www.tldp.org/LDP/intro-linux/html/sect_03_01.html>

## Terminal

### Miscellaneous Tips

- Clear the terminal screen with `Ctl-L`
- View free space in mounted filesystems with `df -h`
- View size of a directory with `du -hs <name>`
- List files with `ls` or `ls -la`
- Delete a file with `rm <name>` or `rm -f <name>`
- Delete a directory and it's contents with `rm -r <name>` or `rm -rf <name>`
- Rename a file or directory with `mv <name> <new_name>`

## Installing and Upgrading Software

### apt

On debian based systems, use `apt` to install and upgrade software.

The first step before installing or upgrading software is to update the local
package database.

`sudo apt update`

To install new software:

`sudo apt install <name>`

Replace `<name>` with the name of the package you want to install.

To upgrade software that is already installed:

`sudo apt full-upgrade`

Also, it's usually a good idea to remove packages that are no longer needed:

`sudo apt autoremove`

### dpkg

Sometimes you may need to install a package that is not in the OS package
database. If you can download a `.deb` file, you can install it like this:

`sudo dpkg -i <file.deb>`

Replace `<file.deb>` with the actual filename.

Sometimes after installing a `.deb` file, you will see an error related to
missing dependencies. This can usually be fixed by running this command:

`sudo apt install -f`

This will install the missing dependencies if they are in the OS package
database.

## Data Recovery

When plugging in an external drive, it can be helpful to see if the drive is
even being recognized, and if so, what is the name of the device.

`dmesg -w`

The `dmesg` command will show kernel log messages. By watching the log messages,
we can see the process of the OS recognizing the drive and assigning it a name.

### Manually Mount A Filesystem

### Clone A Filesystem With gddrescue

## Secure Wipe
