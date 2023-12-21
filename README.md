# Error: no such partition, grub rescue.

- Error no such partition entering rescue mode grub rescue is common after Ubuntu Linux is removed from dual boot PC or when the partition on which a Linux distro was installed is tampered with. The error occurs mainly out of a misconfigured bootloader or wrong active partition.

## How to fix no such partition, entering rescue mode.. error.

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
ls (partition name)
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
This should bring your system back to normal, and you should no longer see the "No Such Partition" error. If you still have issues, please go ahead and revisit the partition identification and setting steps.

![ma](https://github.com/the1Riddle/grub-rescue/assets/125451537/fea3d6db-df8e-4da6-9982-bb4863df6366)

Other posible challenges
--------------------------------------------

### Windows Not Showing in GRUB Menu

You will need to boot into your Linux distro and use `Ctrl` + `alt` + `t` to open the terminal, then check Windows Partition: Confirm where your Windows is stored using commands like ```lsblk``` or ```fdisk -l```. It might be `/dev/sda1` or any other.

Update GRUB for Windows: Add a special Windows option in the /etc/grub.d/40_custom file. Here's an example:

```
menuentry "Windows 10" {
    insmod ntfs
    set root=(hd0,msdos5)
    chainloader +1
}
```
**Replace (hd0,msdos5) with your Windows partition info.**

Enable os-prober: In `/etc/default/grub`, make sure **GRUB_DISABLE_OS_PROBER** is set to `false` for automatic detection of bootable partitions.

Update GRUB: Run ```sudo update-grub``` to refresh the GRUB configuration.

Option 2
-------------------

Are you getting grub rescue every time you reboot your system? Fear not! Here's your escape plan in a few easy steps:
### bypass grub rescue

Open your Linux terminal with the command provided on option one then run the following commands:

```
sudo add-apt-repository ppa:yannubuntu/boot-repair
sudo apt-get update
sudo apt-get install -y boot-repair && boot-repair
```
a new window will open where you will be required to select your preferred repair option and then Patiently wait for the repair process to reach successful completion.
Upon successful repair, you will witness the following confirmation:

![image](https://github.com/the1Riddle/grub-rescue/assets/125451537/515cfe04-a09c-42ee-8754-a29030491328)

To finalize the process, reboot your system using the following command:
```
sudo reboot
```

and you'll be done!

After these steps, you will be able to boot into your windows.

> [!Note]: If Windows isn't appearing in GRUB, check its location, set up a custom GRUB entry, and enable `os-prober`. This should fix the issue and restore dual-boot.

## Do you have some ideas or queries?

If you have questions or suggestions on improving the information on this page, you can always write to [issues](https://github.com/the1Riddle/grub-rescue/issues).
