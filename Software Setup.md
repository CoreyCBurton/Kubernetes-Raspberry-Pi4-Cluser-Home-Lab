# Booting up the Raspberry Pi
To start off, you have to use a mini hdmi cable to connect to your monitor. Once you boot up the Pi, Ubunu 20.04.2 will start up and ask you for a login in. As a 
security messure, the log in is username ubuntu and password is ubuntu. It will then ask you to make a new one. 

# Enabling cgroup memory 
In order to find the syscfg, you will need to use the nano editor and ls comand to navigate around. The path to the boot config is boot/firmware/syscfg.txt. You will 
need to add this line of text to the file. net.ifnames=0 dwc_otg.lpm_enable=0 console=serial0,115200 console=tty1 root=LABEL=writable rootfstype=ext4 elevator=deadline rootwait fixrtc cgroup_memory=1 cgroup_enable=memory swapaccount=1

#   Fix the resolution on the Pi
Type this command in the console to pull up the setup. sudo dpkg-reconfigure console-setup
