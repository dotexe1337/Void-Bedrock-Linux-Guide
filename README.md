# Void/Bedrock Linux Guide
This document is licensed under the GNU Free Documentation License (FDL) v1.3. For more information, please read LICENSE.md

- This is a guide for a complete Bedrock Linux system using Void Linux as the base distribution. This guide assumes that you are using the minimal Void Linux LiveCD (with no Desktop Environments preinstalled).

- I am not responsible for your computer catching fire, you getting fired from your job because the spreadsheet you just saved got corrupted, or the beginnings of thermonuclear war. Do this at your own risk.

- Now then, withour further ado, let's get started.

# Booting the Void Installer
- Step 1: Boot the Void Installer from your preferred medium (CD, DVD, USB, etc)
- Step 2: Log in with the following credentials (username:password): root:voidlinux
- Step 3: Start the Void Linux installer: void-installer

# Installing Void
- Step 1: Select your keyboard layout (Example: us)
- Step 2: Select your network (Example: wlp12s0 for WiFi or enp9s0 for Ethernet). If using WiFi, type in your wireless SSID, encryption scheme, and password. (Example: SSID - MySSID, Encryption - WPA, Password - mypassword)
- Step 3: Select the "Local" package source
- Step 4: Type in your system's hostname This is pretty much the name of your computer. I usually use the model of the computer I'm installing to, for example, m90 for a Dell Precision M90 or optiplex-380 for a Dell Optiplex 380
- Step 5: Select your locale. If you're in the USA, this is probably en_US.UTF-8
- Step 6: Select your time zone. (Example: America/New_York)
- Step 7: Type in your root password. If you're a non-linux user, this is pretty much your administrator password.
- Step 8: Create a user account. (Example: Login name - michael, Full name - Michael LastName, Password - mypassword, Password again - mypassword)
- Step 9: Add your user to the following group: network (You can toggle checkboxes with the space key)
- Step 10: Select the drive that you will be installing the bootloader and OS to. For most people this is probably /dev/sda
- Step 11: Partition your drive. If you're using a legacy BIOS system, then you should create a single partition with the whole size of your drive, make it primary, mark it as bootable and the type should be Linux. If you're using UEFI, you should first create a 100MB partition with the type EFI System, and then create a 2nd partition with the remaining space with the type Linux. You shouldn't have to make the partition bootable on UEFI.
- Step 12: Write the partition changes to your disk.
- Step 13: Configure the filesystem types. For legacy BIOS, your single partition (probably /dev/sda1) should be formatted as ext4 and the mount point should be "/" (without quotations). For UEFI, your first (100MB) partition should be formatted as vfat and should be mounted at "/boot" (without quotations), and your 2nd partition taking up the remainder of your space should be formatted as ext4 and mounted at "/" (without quotations).
- Step 14: Hit install. If everything goes well, you should be running a minimal Void Linux system within a few minutes.
- Step 15: Once the installation is done, select "yes" to reboot the system.
- Step 16: Remove your installation media (CD/DVD/USB/etc) from the computer.

# Setting up the base Void Linux system
- Step 1: Log into Void Linux. You should use the credentials that you created earlier. (Example: username - michael, password - mypassword)
- Step 2 (Optional): Edit /etc/sudoers to remove the password prompt when using sudo. Type `sudo vi /etc/sudoers`, hit I to enter edit mode, and change the line `%wheel ALL=(ALL) ALL` to `%wheel ALL=(ALL) NOPASSWD: ALL`, then hit Esc to exit edit mode, type :w! to save and :q to edit.
- Step 3: Update the package manager: sudo xbps-install -Syu
- Step 4: Update the rest of the system: sudo xbps-install -Syu
- Step 5: Reboot the system (sudo reboot) and log back in once it reboots.
- Step 6: Install the aditional repositories: sudo xbps-install void-repo-multilib void-repo-nonfree void-repo-multilib-nonfree
- Step 7: Install packages: sudo xbps-install -S vim xorg xfce4 firefox thunderbird hexchat vlc qbittorrent qt5ct kvantum arc-theme papirus-icon-theme NetworkManager network-manager-applet pa-applet pulseaudio pavucontrol noto-fonts-ttf noto-fonts-cjk noto-fonts-emoji && sudo xbps-remove -F parole
- Step 8: Edit ~/.xinitrc:
```
Xrdb ~/.Xresources

exec xfce4-session
```
- Step 9: Configure network manager:
```
sudo ln -s /etc/sv/NetworkManager /var/service/
sudo ln -s /etc/sv/dbus /var/service/
sudo rm -rf /var/service/dhcpcd
```
- Step 10: Type "startx" to enter the graphical environment.
- Step 11: Configure XFCE4 to your liking.
- Step 12: Open the Kvantum Manager and set the theme to Arc-Dark.
- Step 13: Open qt5ct and set the theme to Kvantum-Dark Set the icon theme to Papirus-Dark.. Set the general font to Noto Sans Regular 10 and set the fixed width font to Noto Sans Mono 10.
- Step 14: Open appearance settings and set the font to Noto Sans Regular, the monospace font to Noto Sans Mono Regular, the theme to Arc-Dark, and the icon theme to Papirus-Dark.
- Step 15: Open the window manager settings and set the theme to Arc-Dark, and the title font to Noto Sans Bold
- Step 16 (Optional): Disable XFCE4's session saving. Type "xfconf-query -c xfce4-session -p /general/SaveOnExit -n -t bool -s false" (without quotations) into the terminal, then open session & startup settings, go to the session tab and hit "clear saved sessions".

# Installing Bedrock Linux
- Step 1: Download the Bedrock Linux installer for your architecture: https://raw.githubusercontent.com/bedrocklinux/bedrocklinux-userland/0.7/releases
- Step 2: Run the Bedrock Linux installer. sudo sh ./bedrock-linux-release-arch.sh --hijack
- Step 3: Wait for it to install and then reboot: sudo reboot
- Step 4 (Optional): Edit the Grub config to report Bedrock Linux in the bootloader instead of Void Linux: Edit /etc/default/grub with vim, change "Void" to "Bedrock" under "GRUB_DISTRIBUTOR", then save and quit. Run "sudo grub-mkconfig -o /boot/grub/grub.cfg" to write the changes to the config.
- Step 5: Install your desired distributions into Bedrock. You can see a list of potential distributions by typing "brl fetch --list" into terminal. You can install a distribution by typing "brl fetch <distro_name>" into terminal.

At this point, you should be done. You should have a fully functioning Bedrock Linux system running with Void Linux as the base. I hope this guide was helpful to you. Enjoy your Bedrock Linux system!
