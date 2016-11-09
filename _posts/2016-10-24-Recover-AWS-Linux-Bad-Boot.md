---
layout: post
title: Recover from bad boot in Linux on AWS
---

I updated some of my Ubuntu 14.04 LTS instances to 16.04. It turns out in the process the _nobootwait_ option has been removed for use in /etc/fstab.
This stopped my VM from booting with an error. I used the _nobootwait_ option to not have the VM hang around on boot waiting for the EBS I use to become available.  

After going through some man files I found the closest thing I could use was the _nofail_ option. However with the VM unable to boot, I couldn't SSH into it to change it.

To fix it I did the following -  
* Stopped the instace and unmounted the EBS volume. 
* Fired up a new t2.micro instance
* Attached the volume as /dev/sdf
* Booted up the new VM
* Ran the following 
```
mkdir ~/temp
sudo mount /dev/xvdf ~/temp
```  
* This now mounts the volume in my new VM
* I can now manually edit the /etc/fstab
* Once saved, unmount the drive
```
sudo umount ~/temp
```
* Unattach the volume from the VM
* Attach the volume back to the original.  

A little note about this, AWS puts a warning you can only attach devices above /dev/sdf. But this was originally a boot device. You can manually enter /dev/sda1 and AWS will accept it. 
Now the VM successfully completes it's boot sequence.  