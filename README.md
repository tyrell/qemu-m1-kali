# Introduction
The aim is to get Kali Linux running on an Apple M1 Macbook Air with QEMU with a reasonable level of performance. The performance part is a work in progress. I'm currently tweaking the QEMU startup command, experimenting with different parameters.

# Steps

## Install QEMU
QEMU is a generic and open source machine emulator and virtualizer (https://qemu.readthedocs.io/en/latest/about/index.html). Since VirtualBox doesn't suport Apple M1, QEMU is increasingly becoming a go-to option for running other operating system UIs.

Let's install QEMU using Homebrew.

`brew install qemu`

## Download Kali Linux 64-bit installation image

  1. Go to https://www.kali.org/get-kali/#kali-bare-metal
  2. Pick the installer that matches your need from the 64-bit section.

Why x86 64-bit? Because I was not able to get the Applie M1 installer running using qemu-system-aarch64. That's why! :)

## Create a directory for your installation and initialise a QEMU virtual vard disk

  1. `mkdir qemu-m1-kalilinu`
  2. `cd qemu-m1-kalilinu`
  3. `qemu-img create -f qcow2 kali.qcow2 30G`
  4. Copy the Kali Linux 64-bit installation image to the same dorectory

# Start QEMU with the Kali installer mounted as a CD ROM

  `qemu-system-x86_64 -hda kali.qcow2 -boot d -cdrom kali-linux-2022.3-installer-amd64.iso  -m 2G -usb -machine pc`
  
This will launch a QEMU window to kickoff your Kali Linux installation. Step through the installation wizard. Depending on the installation contents you can expect this to take hours to complete. 

Once the installaiton ocmpletes the system will reboot. Since you still have the installation image mounted, you will come back to the start of the installation wizard after rebooting. Please quit QEMU at this point. 

 
 # Launnch your Kali Linux installation 
 
 `qemu-system-x86_64 -hda kali.qcow2 -boot d -m 2G -usb -machine pc &`
 
Congratualtions! You are running Kali Linux on your Apple M1 Mac. 
 
This is the command I'm tweaking at the moment to improve the performance of this installation. I'm happy with the memory utilisation. The CPU performance must be improved for this to be useful as a production machine. 
 
 
 
 
