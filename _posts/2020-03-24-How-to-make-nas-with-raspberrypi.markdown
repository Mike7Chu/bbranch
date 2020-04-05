---
layout: post
title:  "자작나스 만들기 (1)!"
date:   2020-03-24 23:30:16 +0900
image:  nas1.png
tags:   [nas, raspberrypi, omv]
---
## Overview
안녕하세요. Raspberrypi로 자작 나스 구축을 다루겠습니다. 저 같은 경우에는 OpenMediaVault를 설치해서 쉽게 구축하였습니다. OMV의 경우 무료이고, plugin과 web 기반 interface가 잘되어있다는 장점이 있습니다.

------------------------
## OMV 설치하기  
[OMV Sourceforge](https://sourceforge.net/projects/openmediavault/files/OMV%205.x%20for%20Single%20Board%20Computers/)를 확인하면 raspberry pi는 아래 링크로 들어가 가이드를 따르라고 합니다.
해당 링크를 가게되면 pdf를 통해서 가이드를 주고 있습니다.  
여기서 문제가 있는데, 제가 설치할 때는 Sourceforge 상에 릴리즈 된 라즈베리파이용 omv이미지가 있었습니다. 하지만 이제는 라즈비안 위에 omv를 설치하도록 [가이드](https://github.com/OpenMediaVault-Plugin-Developers/docs/blob/master/Adden-B-Installing_OMV5_on_an%20R-PI.pdf)를 주고 있습니다.
따라서 다음과 같은 절차로 다운로드 하시면 됩니다.

1, 라즈비안 [다운로드](https://www.raspberrypi.org/downloads/raspbian/)  
1. 라즈비안 sd card올리기 및 ssh enable.  
1. putty를 통하여 ssh 접속  
1. omv 다운로드  
<br>  
```bash
wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash
```
------------------------  

## 마치며  
만약 제 로컬 PC에 이전 설치대로 omv4 라즈베리파이용 이미지가 있다면 업로드해서 추가 가이드 드리도록 하겠습니다.    

![](../img/nas1.png)  

### 추가 omv4 라즈베리파이용 이미지  
[다은로드 링크](http://mike7chu.hopto.org:8000/f/b60af46f7d3e4c01b637/?dl=1)