# Introduction
Now that you have the SD cards set up for Ubuntu 20.044.2 LTS and your Raspberry Pis on the platform, it is time to set up the server on each Raspberry Pi. 

#   Fix the resolution on the Pi
Once you boot up your Pi, the console seems very zoomed out. If that is the way you pefer it, that is completely fine. If you are like me and pefer a more zoomed in version, then follow these steps. Type this command in the console ```sudo dpkg-reconfigure console-setup ``` This will lead you to a user interface where it will ask what incoding to use. The option I picked was **UTF-8**. Then the screen will ask you what character to support, the one that I used is **Combined-Latin: Slavic Cyrlllic: Greek**. It will then ask you what font for the console, this is all up for user perference but the one I chose was the **TerminusBold**. Last but not least, it will ask you what font size you would like, the one that I chose was the **16x32(framebuffer only)**. Now that I have my console set up, it is time to move on to enabling cgroup memory.   

# Enabling cgroup memory 
In order for Kubernetes to work, we will have to modify the **syscfg.txt** by enabling cgroup memory. The directroy for **syscfg.txt** is boot/firmware/syscfg.txt.
Using the **nano** editor, please add this code to the .txt file.

```
net.ifnames=0
dwc_otg.lpm_enable=0
console=serial0,115200       
console=tty1
root=LABEL=writable
rootfstype=ext4
elevator=deadline
rootwait
fixrtc
cgroup_memory=1
cgroup_enable=memory
swapaccount=1

```
# Getting the IP adress from the Raspberry Pi.
If you know how to navigate around your router and you have the Raspberry Pi hooked up to your switch properly, then you can most likely find the ip under Ubuntu in your router settings. If you want to find the ip using the terminal, follow these steps. Type in the console ``` ip a ```. Looking at what the console returned, find **eth0** look for inet. There is a set of numbers that ussaly starts with **192.xxx.x.xxx**. This is the ip address for the Pi you just set up. Next step is too add the SSH key.

# Adding the SSH key to your Raspberry Pi.

sudo cp k3sup-arm64 /user/local/bin/k3sup
