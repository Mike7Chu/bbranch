---
layout: post
title:  "WSL에서 SAMBA 마운트하기"
date:   2020-09-13 22:20:22 +0900
image:  samba/wsl.JPG
tags:   [wsl, samba]
---
## WSL에서 SAMBA  
WSL에서 다음 명령어로 마운트 시 에러가 발생하면서 마운트가 되지 않습니다.  
```bash
mount -t cifs '\\192.168.219.102/share' ~/samba
```
>![ErrorImage](../img/samba/error.png)  
mount error: cifs filesystem not supported by the system  
mount error(19): No such device  

<br>
에러 로그를 보면 이 시스템에서 지원하지 않는다고 하는데요, wsl에서는 Window Driver를 사용하여 samba를 마운트해야 한다고 합니다. 따라서 아래 타입으로 마운트를 시도하시면 됩니다.  

```bash
mount -t drvfs '\\192.168.219.102/share' ~/samba
```
<br>

성공적으로 mount가 되는 것이 확인 됩니다.  
번외로  
기본적으로는 일반 linux system에서는 cifs타입으로 하면 마운트가 됩니다. 만약 cifs가 되지 않는다면 cifs와 smbclient를 설치 후 하시는 걸 추천합니다.

```bash
apt-get install smbclient cifs-utils
```

감사합니다.