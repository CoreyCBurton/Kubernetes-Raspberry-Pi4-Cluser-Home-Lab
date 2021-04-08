# Introduction
Now that you have the SD cards set up for Ubuntu 20.044.2 LTS and your Raspberry Pis on the platform, it is time to set up the server on each Raspberry Pi. 

#   Fix the resolution on the Pi
Once you boot up your Pi, the console seems very zoomed out. If that is the way you pefer it, that is completely fine. If you are like me and pefer a more zoomed in version, then follow these steps. Type this command in the console ''' sudo dpkg-reconfigure console-setup '''. This will lead you to a user interface where it will ask what incoding to use. The option I picked was **UTF-8**. Then the screen will ask you what character to support, the one that I used is **Combined-Latin: Slavic Cyrlllic: Greek**. It will then ask you what font for the console, this is all up for user perference but the one I chose was the **TerminusBold**. Last but not least, it will ask you what font size you would like, the one that I chose was the **16x32(framebuffer only)**. Now that I have my console set up, it is time to move on to enabling cgroup memory.   

# Enabling cgroup memory 
In order for Kubernetes to work, we will have to modify the syscfg.txt by enabling cgroup memory. 

In order to find the syscfg, you will need to use the nano editor and ls comand to navigate around. The path to the boot config is boot/firmware/syscfg.txt. You will 
need to add this line of text to the file. net.ifnames=0 dwc_otg.lpm_enable=0 console=serial0,115200 console=tty1 root=LABEL=writable rootfstype=ext4 elevator=deadline rootwait fixrtc cgroup_memory=1 cgroup_enable=memory swapaccount=1

