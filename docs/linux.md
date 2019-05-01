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

The `fdisk` command can be used to list all partitions on the system.

`sudo fdisk -l`

### Automatically Mount A Filesystem

If the drive is clean, it will usually mount automatically when you plug it in.
If it doesn't, you can try to access it from the GUI. If it does mount, it will
be in `/media/ubuntu/<name>`, where `<name>` is the filesystem label. If the
drive doesn't mount because of being dirty, the pop-up error message will tell
you where the partition is. Usually it's something like `/dev/sdc3`.

### Manually Mount A Filesystem

To manually mount the drive, you need an empty directory to mount it to. Create
one using `mkdir`.

`mkdir sdc3`

Then mount the drive to the empty directory.

`sudo mount -r /dev/sdc3 sdc3`

At this point you should be able to see the data in the GUI, or in the terminal
with `ls`.

`ls sdc3`

### Copy Data With `rsync`

Now that we have everything mounted, we can use `rsync` to copy the data.

`rsync -a --info=progress2 <source> <destination>`

The `-a` option tells rsync to copy all subdirectories. The `--info=progress2`
option gives us a progress bar.

`rsync` will behave differently depending on if we put a trailing `/` after the
source path. Without a trailing `/` the source directory will be copied to the
destination. With a trailing `/` the *contents* of the source directory will be
copied to the destination.

For example, lets say we have the drive we are copying from mounted at `sda3`,
and an external drive we are copying to mounted at `/media/ubuntu/external`.

Running the following command will create the `customer_name` directory on the
external drive, and create the `Users` directory inside of that. We will end up
with `/media/ubuntu/external/customer_name/Users`.

`rsync -a sda3/Users /media/ubuntu/external/customer_name/`

What if we want the *contents* of `sda3/Users` copied directly to
`/media/ubuntu/external/customer_name`? We can do that with the following
command.

`rsync -a sda3/Users/ /media/ubuntu/external/customer_name/`

Then we will end up with the *contents* of users in
`/media/ubuntu/external/customer_name/`. There will not be a `Users` directory
on the external drive, only the contents of `Users` will be copied.

If in doubt, run the command without the trailing `/`.

### Clone A Partition With gddrescue

## Secure Wipe
