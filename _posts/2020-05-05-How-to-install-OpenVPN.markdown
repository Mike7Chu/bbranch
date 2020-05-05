---
layout: post
title:  "OpenVPN 서버 구축"
date:   2020-05-05 23:55:26 +0900
image:  openvpn1.jpg
tags:   [OpenVPN, Docker]
---
## Overview
안녕하세요. 요즘 코로나 영향으로 자택근무가 주목받고 있습니다. 보안과 자택근무 환경과 관련된 VPN망 구축을 아래와 같이 알려드리려고 합니다.   
[1. OpenVPN이란](#OpenVPN이란)  
[2. Docker를 이용한 OpenVPN 설치](#OpenVPN-설치)  
[3. OpenVPN 설정](#OpenVPN-설정)  
[4. OpenVPN 실행](#OpenVPN-실행)    

------------------------  

## OpenVPN이란  
*OpenVPN이란 OpenVPN Technologies, Inc.에서 제작하고 배포하는 오픈소스 VPN 프로토콜과 그 접속 프로그램을 말한다.*[*나무위키*](https://namu.wiki/w/OpenVPN#toc)  
나무위키 설명과 더불어 OpenVPN은 ssl 인증서를 이용하여 로그인 인증을 하고 있으며 ssl인증서를 관리하므로서 사용자를 관리할 수 있습니다.  
참고로 VPN은 Virtual Private Network로서 가상 사설 망으로 해석됩니다. 보통 회사에서 사설망을 운용하는데 외부에서 접근을 보안상 목적으로 차단하고 있습니다. 이에 따라 외부에서 사설망에 접근하기 위하여 외부에서도 사설망에 연결 되어 있는 것처럼 해주는 것이 VPN 입니다.

------------------------  

## OpenVPN 설치  
OpenVPN은 Ubuntu인 경우 [Install Guide](https://openvpn.net/vpn-software-packages/)를 참고하여 설치가 가능하지만, 저는 [Docker](https://hub.docker.com/r/kylemanna/openvpn)를 이용하여 손쉽게 설치하였습니다.  
```bash
OVPN_DATA="ovpn-data-example"
docker volume create --name $OVPN_DATA
docker run -v $OVPN_DATA:/etc/openvpn --log-driver=none --rm kylemanna/openvpn ovpn_genconfig -u udp://VPN.SERVERNAME.COM
docker run -v $OVPN_DATA:/etc/openvpn --log-driver=none --rm -it kylemanna/openvpn ovpn_initpki
```
<br>  

설치 후 아래 명령어를 통하여 OpenVPN 서버를 실행할 수 있습니다.  
```bash
docker run -v $OVPN_DATA:/etc/openvpn -d -p 1194:1194/udp --cap-add=NET_ADMIN kylemanna/openvpn
```
<br>
*위 명령어에서 알 수 있듯이 1194 port는 개방되어 있어야 합니다. 포트 포워딩으로 개방 해주도록 해줍시다.*  

------------------------  

## OpenVPN 설정  
OpenVPN 실행이 완료 되었다면 Client 인증서를 관리해야하는데요. Client 인증서는 아래 명령어로 생성이 가능합니다.  
```bash
#비밀번호가 필요없는 계정 (CLIENTNAME이 유저명 입니다.)
docker run -v $OVPN_DATA:/etc/openvpn --log-driver=none --rm -it kylemanna/openvpn easyrsa build-client-full CLIENTNAME nopass

#비밀번호가 필요한 계정
docker run -v $OVPN_DATA:/etc/openvpn --log-driver=none --rm -it kylemanna/openvpn easyrsa build-client-full CLIENTNAME

#생성된 ssl을 가져오기
docker run -v $OVPN_DATA:/etc/openvpn --log-driver=none --rm kylemanna/openvpn ovpn_getclient CLIENTNAME > CLIENTNAME.ovpn

```
<br>  
계정 생성이 완료하였으면 현재 경로에 CLIENTNAME.ovpn이 생성된 것을 확인할 수 있습니다.

------------------------

## OpenVPN 실행  
생성된 CLIENTNAME.ovpn을 Mobile에 저장하거나 다른 pc로 가져와서 실행을 해주면 됩니다. 참고로 [Windows용](https://openvpn.net/client-connect-vpn-for-windows/) [Android용](https://play.google.com/store/apps/details?id=net.openvpn.openvpn&hl=ko) [Mac용](https://openvpn.net/client-connect-vpn-for-mac-os/) 링크 드립니다.
<br>
<center>
<img src="../img/openvpn3.jpg" alt="drawing" style="width:200px;"/>
<img src="../img/openvpn2.jpg" alt="drawing" style="width:200px;"/>
</center>

-----------------------  

## 마치며
OPENVPN을 구축하면서도 Docker의 편리함을 정말 느낄 수 있습니다. Docker를 두번 쓰세요. 많이 쓰세요....