---
layout: post
title:  "Windows git server 셋팅(Bonobo Git)"
date:   2020-09-06 23:20:22 +0900
image:  bonobogit/logo.JPG
tags:   [Git, Bonobo Git]
---
## Overview  
외부에 나가서 버전 컨트롤이 따로 없는것도 물론이고, 서버 리소스도 받지 않아 다음과 같은 방법으로 노트북에 깃서버를 구성하여 프로젝트를 진행한 적이 있습니다. Bonobo Git을 설치하였는데, Bonobo Git만으로도 코드 변경점, 배포를 효율적으로 할 수 있습니다.  
<br>
[1. 사전 준비](#사전-준비)  
[2. 설치](#설치)  
[3. 마치며](#마치며)  

------------------------  

## 사전 준비  
Bonobo GIt은 다음과 같은 사전 셋팅이 필요합니다.  
* IIS 활성화  
* Git 설치  
  * Link : https://git-scm.com/  
* Bonobo Git 설치  
  * Link : https://bonobogitserver.com/  
* .Net Framework 4.6 설치
  * Link : https://www.microsoft.com/en-gb/download/details.aspx?id=48130  

기본적으로 Windows 7 이상이어야 하고 .Net이 4.0 이상에서 돌려야 합니다. 우선 IIS를 활성화 하기 위해서 최상위 .Net 기능 활성화와 아래 이미지 처럼 체크 하시면 됩니다.  
![IIS셋팅](../img/bonobogit/bonobogit.png)  

------------------------  

## 설치  

* [Bonobo Git 설치](https://bonobogitserver.com/)를 먼저 합니다.  
Bonobo Git을 받은 뒤 압축을 풀어 줍니다.  
* 그룹 권한 추가  
해당 디렉토리의 그룹 권한을 추가 해줍니다.  
![그룹 추가](../img/bonobogit/iis_1.JPG)   
<br>
* IIS(인터넷 정보 서비스) 관리자에서 압축푼 경로를 추가해줍니다.  
저는 다음과 같은 순서로 추가하였습니다.  
  * Default Web Site 아래에 가상디렉토리 추가  
  * 우측클릭 후 애플리케이션 변환 클릭  
  * 애플리케이션 풀 선택 - .Net 4.5 선택  
  ![.Net4.5추가](../img/bonobogit/iis_2.JPG)  
  <br>
* http://localhost/gitserver/ 접속해서 확인
접속해서 확인하면 접속할 수 있습니다.  
  ![bonobo git](../img/bonobogit/bonobo_1.JPG)  
<br>

bonobo git은 쉽게 설치하고 운용할 수 있습니다. 첫 admin ID/PW 은 admin/admin 입니다. 이후 기본적인 Setting에서 권한 설정 후 사용하시면 됩니다. ssh는 지원하지 않고, http를 지원하고 있습니다. 사용에 참고하시면 됩니다.  

------------------------

## 마치며
번외로 만약 iis가 아닌 apach나 nginx를 설치해서 사용도 하고있고, Linux 환경에서도 운영할 수 있습니다. 아무래도 가볍다보니 gitlab을 설치하는 것보다 더 빠르고 유용하지만 다만 보안 프로토콜을 지원하지 않아 이 부분이 필요하다면 gltlab을 도입하는 것도 좋은 방법입니다.  
