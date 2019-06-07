# Void/Bedrock Linux Guide
This is a guide for a complete Bedrock Linux system using Void Linux as the base distrobution. This guide assumes that you are using the minimal Void Linux LiveCD (with no distrobutions preinstalled).

I am not responsible for your computer catching fire, you getting fired from your job because the spreadsheet you just saved got corrupted, or the beginnings of thermonuclear war. Do this at your own risk.

Now then, withour further ado, let's get started.

# Booting the Void Installer
Step 1: Boot the Void Installer from your preferred medium (CD, DVD, USB, etc)
Step 2: Log in with the following credentials (username:password): root:voidlinux
Step 3: Start the Void Linux installer: void-installer

# Installing Void
Step 1: Select your keyboard layout (Example: us)
Step 2: Select your network (Example: wlp12s0 for WiFi or enp9s0 for Ethernet). If using WiFi, type in your wireless SSID, encryption scheme, and password. (Example: SSID - MySSID, Encryption - WPA, Password - mypassword)
Step 3: Select the "Local" package source
Step 4: Type in your system's hostname This is pretty much the name of your computer. I usually use the model of the computer I'm installing to, for example, m90 for a Dell Precision M90 or optiplex-380 for a Dell Optiplex 380
Step 5: Select your locale. If you're in the USA, this is probably en_US.UTF-8
Step 6: Select your time zone. (Example: America/New_York)
Step 7: Type in your root password. If you're a non-linux user, this is pretty much your administrator password.
Step 8: Create a user account. (Example: Login name - michael, Full name - Michael LastName, Password - mypassword, Password again - mypassword)
Step 9: Add your user to the following group: network (You can toggle checkboxes with the space key)
Step 10: Select the drive that you will be installing the bootloader and OS to. For most people this is probably /dev/sda
Step 11: Partition your drive. If you're using a legacy BIOS system, then you should create a single partition with the whole size of your drive, make it primary, mark it as bootable and the type should be Linux. If you're using UEFI, you should first create a 100MB partition with the type EFI System, and then create a 2nd partition with the remaining space with the type Linux. You shouldn't have to make the partition bootable on UEFI.
Step 12: Write the partition changes to your disk.
Step 13: Configure the filesystem types. For legacy BIOS, your single partition (probably /dev/sda1) should be formatted as ext4 and the mount point should be "/" (without quotations). For UEFI, your first (100MB) partition should be formatted as vfat and should be mounted at "/boot" (without quotations), and your 2nd partition taking up the remainder of your space should be formatted as ext4 and mounted at "/" (without quotations).
Step 14: Hit install. If everything goes well, you should be running a minimal Void Linux system within a few minutes.

# Setting up the base Void Linux system
To be continued.
