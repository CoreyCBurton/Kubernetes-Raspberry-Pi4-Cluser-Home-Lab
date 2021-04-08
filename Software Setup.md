# Introduction
Now that you have the SD cards set up for Ubuntu 20.044.2 LTS and your Raspberry Pis on the platform, it is time to set up the server on each Raspberry Pi. 

# Enabling cgroup memory 
In order to find the syscfg, you will need to use the nano editor and ls comand to navigate around. The path to the boot config is boot/firmware/syscfg.txt. You will 
need to add this line of text to the file. net.ifnames=0 dwc_otg.lpm_enable=0 console=serial0,115200 console=tty1 root=LABEL=writable rootfstype=ext4 elevator=deadline rootwait fixrtc cgroup_memory=1 cgroup_enable=memory swapaccount=1

#   Fix the resolution on the Pi
Type this command in the console to pull up the setup. sudo dpkg-reconfigure console-setup
