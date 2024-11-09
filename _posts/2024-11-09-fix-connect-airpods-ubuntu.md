---
title: Fix Connect Airpods Ubuntu
date: 2024-11-09 01:01:01 +0700
categories: [fix]
tags: [fix]     # TAG names should always be lowercase
---

## 1. Fix Connect Airpods Ubuntu
``` bash
pactl info
sudo apt-get upgrade pulseaudio
sudo gedit /etc/bluetooth/main.conf
```

Add ControllerMode = bredr

``` bash
sudo /etc/init.d/bluetooth restart
```

## 2. Reference
- [https://www.youtube.com/watch?v=3TJDgIveiI8&t=343s](https://www.youtube.com/watch?v=3TJDgIveiI8&t=343s)
- [https://askubuntu.com/questions/1408647/unable-to-pair-airpods-pro-with-ubuntu-22-04](https://askubuntu.com/questions/1408647/unable-to-pair-airpods-pro-with-ubuntu-22-04)