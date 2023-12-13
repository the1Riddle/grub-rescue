# Error: no such pertition, grub rescue.

- Error no such partition entering rescue mode grub rescue is common after Ubuntu Linux is removed from dual boot PC or when the partition on which a linux distro was installed is tampered with. The error occurs mainly out of misconfigured bootloader or wrong active partition.

## How to fix no such pertition, entering rescue mode.. error.

If you encounter the dreaded "No Such Partition" error and find yourself stuck in rescue mode, don't worry! Follow these steps to get your system back on track:

Step 1: Identify Available Partitions
----------------------------------

Start by listing all available partitions using the ls command:

```
ls
```
This will display a list of partitions similar to the following image:

![img1](https://github.com/the1Riddle/grub-rescue/assets/125451537/18dcf04b-dd09-4e2d-af45-fec99134bd54)

Step 2: Check File Type
------------------------------------

To identify the file type within a specific partition, use the following command:

```
ls (pertitionname)
```

**Note:** If you encounter a `'Filesystem is unknown'` error, it means there's no ***operating system*** installed on that partition. Continue searching until you find a different output, as shown in the image below:

![img2](https://github.com/the1Riddle/grub-rescue/assets/125451537/e09ec3f0-d16b-4ddd-afb3-5d8fec14d60d)

Step 3: Set the Boot Partition
----------------------------------------

Once you've identified the partition you want to boot from, set it using the following commands. Adjust the partition name accordingly; use the commands:

```
set boot=(hd1,msdos5)
set prefix=(hd1,msdos5)/boot/grub
insmod normal
```
The setup should look like this:

![111](https://github.com/the1Riddle/grub-rescue/assets/125451537/70e1df2d-e004-4c19-8099-555ca8ec236c)

If you encounter an error, redo it again as you double-check the partition name and ensure you've used the correct commands.

Step 4: Restore Normal Boot
------------------------------------------

To complete the process, enter the following command:

```
normal
```
This should bring your system back to normal, and you should no longer see the "No Such Partition" error. If you still encounter issues, revisit the partition identification and setting steps.

![ma](https://github.com/the1Riddle/grub-rescue/assets/125451537/fea3d6db-df8e-4da6-9982-bb4863df6366)

Other posible challenges
--------------------------------------------

### Windows Not Showing in GRUB Menu

You will need to boot into your linux distro use `Ctrl` + `alt` + `t` to open the terminal, then check Windows Partition: Confirm where your Windows is stored using commands like ```lsblk``` or ```fdisk -l```. It might be `/dev/sda1` or anyy other.

Update GRUB for Windows: Add a special Windows option in the /etc/grub.d/40_custom file. Here's an example:

```
menuentry "Windows 10" {
    insmod ntfs
    set root=(hd0,msdos5)
    chainloader +1
}
```
**Replace (hd0,msdos5) with your Windows partition info.**

Enable os-prober: In /etc/default/grub, make sure GRUB_DISABLE_OS_PROBER is set to false for automatic detection of bootable partitions.

Update GRUB: Run ```sudo update-grub``` to refresh the GRUB configuration.

Option 2
-------------------

You may just run
```
sudo os-prober
```
if your installation is found, like you fill see tha name of the win, then do:

```
sudo update-grub
```
and you'll be done!

After these steps, you will be able to boot into your windows.

Conclusion: If Windows isn't appearing in GRUB, check its location, set up a custom GRUB entry, and enable `os-prober`. This should fix the issue and restore dual-boot.
