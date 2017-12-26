# ArchLinux Setup Notes

- (Official installation guide)["https://wiki.archlinux.org/index.php/Official_Arch_Linux_Install_Guide"]
- Experiment environment: Virtual Box + archlinux-2017.10.01-x86_64.iso


### Steps:

I mainly followed the offical guideline with only few tweaks different.

1. Verify the boot mode -- refer to the guideline
2. Connect to internet -- refer to the guideline
3. Update the system clock -- refer to the guideline
4. Partition the disk
	- Used fdisk instead of gdisk
		>/dev/sda1   linux filesystem    `use 'a' command to flag it as bootable`

		>/dev/sda2 	 swap				  'use 'type' command to set the type of this partition. code: 82'
		
		>/dev/sda3    linux filesystem

	- make ext4 filesystem
	```bash
		mkfs.ext4 /dev/sda1
		mkfs.ext4 /dev/sda3
	```
	- Mount the file systems 
	```bash
		mount /dev/sda1 /mnt
		mkdir /mnt/home
		mount /dev/sda3 /mnt/home
	```
5. Install the base packages -- refer to the guidline
6. Fstab -- refer to the guidline
7. Chroot -- refer to the guidline
8. Time zone -- refer to the guidline
9. Locale -- refer to the guidline
10. Hostname -- refer to the guidline
11. Root password -- refer to the guidline
12. Boot loader
	- Install the grub
	```
	grub-install --target=i386-pc /dev/sdx
	```
	- Copy locale
	```
	cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo
	```

	- Generate main configuration file
	```
	grub-mkconfig -o /boot/grub/grub.cfg
	```
13. Reboot
        - Before reboot the system, we need manually unmount all partitions with the following command.
        ```
        umount -R /mnt
        ```

        - Reboot system
        ```
        reboot
        ```
14. Add unprivileged user, "archie"
        ```
        useradd -m -G wheel -s /bin/bash archie
        ```

15. Install *sudo*
        - Install "sudo" package in root mode
        ```
        pacman -S sudo
        ```
        - Add user "archie" to configuration file /etc/sudoers by using *visudo*
        ```
        visudo
        ```
        - Add the following line under "User privilege specification"
        ```
        archie ALL=(ALL) ALL
        ```
16. Install display server
        

