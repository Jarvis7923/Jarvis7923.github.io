---
layout: post
category: ubuntu
---
## Problem descriptions     
The laptop display can not be restarted after closing the lid while the sound works well. In fact, after restarting the laptop-mode several times, it still doesn't work out. Therefore, I believe it's time to say goodbye to the hibernation mode of the Ubuntu.  

## Environment
Ubuntu version, results from command `sudo lsb_release -a`:
```
>  Distributor ID: Ubuntu
>  Description:    Ubuntu 16.04.6 LTS
>  Release:    16.04
>  Codename:   xenial
```
Kernel version, results from command `uname -a`:
```
> 4.15.0-50-generic #54~16.04.1-Ubuntu SMP Wed May 8 15:55:19 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
```

## Solution
### Install laptop-mode-tools
Run this in the terminal to check the status of package `laptop-mode-tools`
```
dpkg -l | grep laptop-mode-tools
```
if you catch the output like:
```
ii  laptop-mode-tools    1.68-3ubuntu1    all    Tools for Power Savings based on battery/AC status
   
```
Then you already have the package installed, if not, run:
```
sudo apt-get install laptop-mode-tools
```
        
### Check the status of the laptop mode

Run `cat /proc/sys/vm/laptop_mode` to check if the laptop mode has already activated. '0' means it *does not* start, other number means it start. 

### Change the configuraton

Try to change or remove the comment of this line:
```
ENABLE_LAPTOP_MODE=true
```
in `/etc/default/acpi-support`. if you find there is no such line in this file but you get:
```
# Note: to enable "laptop mode" (to spin down your hard drive for longer
# periods of time), install the laptop-mode-tools package and configure
# it in /etc/laptop-mode/laptop-mode.conf. 
```
Then it's time to change the perspective. Edit `/etc/laptop-mode/laptop-mode.conf`, change the following lines to true:
```
ENABLE_LAPTOP_MODE_ON_BATTERY=1

ENABLE_LAPTOP_MODE_ON_AC=1

ENABLE_LAPTOP_MODE_WHEN_LID_CLOSED=1
```
After that, restart the laptop node service by `/etc/init.d/laptop-mode restart`. Check if it has taken effect by `cat /proc/sys/vm/laptop_mode` as mentioned before, 
    
Most of the blogs said that you can restart your laptop and try to close your lid and check if the system can be evoked. 

But unfortuately, I myself didn't take the advange of this workaround. So if you still want to see your lovely graphic interface after you close the lid, prohibit the hibernation functionality once and for all. 


### Close the hibernation
Check the systme config file
```
grep -r HandleLidSwitch /etc/systemd/logind.conf
```
Change the config file 
```
sudo sed -i 's/#HandleLidSwitch=suspend/HandleLidSwitch=ignore/g' /etc/systemd/logind.conf
```
and restart the service
```
systemctl restart systemd-logind.service
```
Then feel free to try closing the lid. At least it works for my laptop. 











 

