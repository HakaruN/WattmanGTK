# WattmanGTK
This is a Python3 program which uses a simple GTK gui to view, monitor and in the future overclock a Radeon GPU on Linux. 
![Main screen](https://i.imgur.com/ahrQrEO.png)

NOTE: This is a branch of the original wattmanGTK by user: BoukeHaarsma23. This branch allows for setting values from the UI (not just looking at them)
## What can it do?
 * View memory and GPU P-states including voltages.
 * Ability to monitor signals from GPU sensors by means of plotting
 * Write a bash file with overclock settings
 * Multi GPU support in top dropdown list
 * Directly apply values from GUI (What this branch brings to the table)
## What can't it do? 
 * Fan control
 * Monitor multiple GPU's

## Hardware Requirements

* A Radeon card which uses the AMDGPU kernel driver

## OS Requirements

* Linux kernel 4.8+ (Ubuntu 16.10 or newer)
* The overdrive kernel parameter must be set.
* Python3 (3.6+)

## Virtual Environment Requirements

Production Environment

    sudo apt install --yes \
        python3-matplotlib
        python3-gi
        python3-setuptools
        python3-cairo

Development Environment

    python3.7 -m venv venv
    source venv/bin/activate
    python -m pip install --upgrade \
        matplotlib \
        setuptools \
        pycairo

## Usage/ installation

Clone the repository and open a terminal in this folder and install the required packages. For installation run

Production Installation

```
    sudo ./install.sh
```

Development Installation

```
    python -m pip install -e .
```


After installation, the downloaded files may be deleted.


After installation, to run type in any terminal window:

```
    sudo wattmanGTK
```



in a terminal where you cloned the repository. 
When you want to apply the settings given in the GUI click apply, and instructions will be given on how to apply the overclock. This is at your own risk!
## Contributing & Donations
Contributions can be made in terms of:
 * Hardware debugging, please let me know if your configuration runs or not (mine is run with 4.19 and an RX480)
 * Feature additions, some TODO's are given in the files
 * Packaging of the software
 * Feedback on the code
 * Donations can be made on http://paypal.me/pools/c/89hdUKrx2Z
 * Other contributions are also possible, please let me know
 ## FAQ
 ### How do I know my card has the overdrive bit enabled
 Just try to run WattmanGTK. It will tell you if your card does not 
 support overdrive. Even if this is not the case you can set a kernel 
 parameter to force overdrive to be enabled (may not work on all cards).
 For more information on how to set the parameter check the [Arch Wiki](https://wiki.archlinux.org/index.php/kernel_parameters)

 For GRUB based systems (like ubuntu): edit the /etc/default/grub file and edit the line:
```
    GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```
And change it to:
```
    GRUB_CMDLINE_LINUX_DEFAULT="quiet splash amdgpu.ppfeaturemask=<the suggested value by WattmanGTK>"
```
Then grub needs to be updated, for ubuntu this is done by running
```
    sudo update-grub
```
For distro agnostic updating this can be done by running

on BIOS systems: ```# grub2-mkconfig -o /etc/grub2.cfg```

on UEFI systems: ```# grub2-mkconfig -o /etc/grub2-efi.cfg```

Then reboot the machine. Once rebooted you can check the current featuremask by 
```
   printf "0x%08x\n" $(cat /sys/module/amdgpu/parameters/ppfeaturemask)
```
 ### Setting the kernel parameter causes artifacts and glitching
 It could be that setting the kernelparameter can enable features that 
 should not be enabled which could be the cause.
 ### The program does not work for me
 Please open an issue here. Furthermore, refer to this thread on reddit for additional help: [link](https://www.reddit.com/r/linux/comments/9tnijg/a_gtk_wattman_like_gui_for_amd_radeon_users/)
 
 ### The program can not find a certain senor path and fails
Please refer to: https://github.com/BoukeHaarsma23/WattmanGTK/issues/1

