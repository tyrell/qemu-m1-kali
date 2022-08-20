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

Why x86 64-bit and not the Apple M1 installer?! Because I was not able to get the Kali Linux Applie M1 installer running using QEMU. That's why! :)

## Create a directory for your installation and initialise a QEMU virtual vard disk

  1. `mkdir qemu-m1-kalilinu`
  2. `cd qemu-m1-kalilinu`
  3. `qemu-img create -f qcow2 kali.qcow2 30G`
  4. Copy the Kali Linux 64-bit installation image to the same dorectory

# Start QEMU with the Kali installer mounted as a CD ROM

  `qemu-system-x86_64 -hda kali.qcow2 -boot d -cdrom kali-linux-2022.3-installer-amd64.iso  -m 2G -usb -machine pc`
  
This will launch a QEMU window to kickoff your Kali Linux installation. Step through the installation wizard. Depending on the installation contents you can expect this to take hours to complete. 

Once the installation completes the system will reboot. Since you still have the installation cd-rom image mounted, you will come back to the start of the installation wizard after rebooting. Please quit QEMU at this point. 

 
 # Launch your Kali Linux installation 
 
 `qemu-system-x86_64 -hda kali.qcow2 -boot d -m 2G -usb -machine q35 -cpu max -smp cores=8,threads=1,sockets=1  &`
 
Congratualtions! You are running Kali Linux on your Apple M1 Mac. 
 
This is the command I'm tweaking at the moment to improve the performance of this installation. I'm happy with the memory utilisation. The CPU performance must be improved for this to be useful as a production machine. 
 
 
 # Final thoughts
After fiddling with QEMU launch command parameters for a while I was still not happy with the performance of the Kali Linux installation. 

Kali Linux wasn't the only guest OS I was having trouble with. I also have a fiddly Windows 11 installation on QEMU that I've been using on and off for a few months. That windows instance seems to have decided to become corrupted on its own while I wasn't looking. 

If this was a long time ago, I would have spent hours and hours figuring out QEMU and getting my guest OSs working. However, today I optimise my time differently. 

So, I installed a Parallels Desktop Pro trial on my M1 Macbook Air, which came with Windows 11 and Kali Linux fully supported out of the box. Both Kali and Windows perform like native applications with Parallels. Needless to say, I went from trial to paid subscriber in under an hour. Yes, that's how fast the installation and verification process was for both guest operating systems. 

PS: This isn't a paid advertisement for Parallels, and I still encourage you to give QEMU a try folowing the steps above. Please submit a pull request, if you manage to tweak QEMU to get better performance out of a Guest OS. 


 
 
