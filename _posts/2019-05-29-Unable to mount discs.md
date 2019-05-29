---
layout: post
project: default
category: ubuntu
---
## Problem descriptions     
Unable to get access to a different hard disc from Ubuntu. 

The error looks like:
![test](https://raw.githubusercontent.com/Jarvis7923/pictures/master/Screenshot%20from%202019-05-29%2017-02-32.png)

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
Try command `sudo ntfsfix /dev/sda2` 
in which `sda2` is the name of the disc that you want to mount. 

The result looks like:
```
>  Mounting volume... OK
>  Processing of $MFT and $MFTMirr completed successfully.
>  Checking the alternate boot sector... OK
>  NTFS volume version is 3.1.
>  NTFS partition /dev/sda2 was processed successfully.
```




