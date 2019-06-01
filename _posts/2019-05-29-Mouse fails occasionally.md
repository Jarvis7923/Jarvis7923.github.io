---
layout: post
category: ubuntu
---
## Problem descriptions     
The mouse occasionally fails after reboot. Actually, it's more like the mouse is suspended or asleep if it is not used for several seconds.  

## Solution
### Work around 1
Unplug the mouse and reconnect every time after reboot.

### Change the laptop-mode configuration
Edit `runtime-pm.config`
```
sudo vi /etc/laptop-mode/conf.d/runtime-pm.conf
```
Close the autosuspend, set:
```
CONTROL_RUNTIME_AUTOSUSPEND = 0
```
Then restart the computer. 



