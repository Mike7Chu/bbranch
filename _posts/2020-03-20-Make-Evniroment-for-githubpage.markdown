---
layout: post
title:  "Githubpage 포스팅 하기!"
date:   2020-03-20 08:30:12 +0900
image:  galada-post.jpg
tags:   [githubpage]
---
## Overview
안녕하세요. 오늘은 제가 포스팅 하는 방법에 대해서 써보려고 합니다. 현재 blog는 jekyll 기반으로 되어있습니다. 따라서 localpc에 jekyll 환경을 구축하고, 포스팅하는 방법을 알아보겠습니다.  

------------------------
## jekyll 환경 구축하기
[jekyll docs](https://jekyllrb.com/docs/)를 확인하면  다음과 같이 소개하고 있습니다.  
```bash
# 1. Install a full Ruby development environment.
gem install jekyll bundler # 2. Install a full Ruby development environment.
jekyll new myblog # 3. Create a new Jekyll site at ./myblog.
cd myblog # 4. Change into your new directory
bundle exec jekyll serve # 5. Build the site and make it available on a local server.
```
<br>
그러면 Ruby 환경을 설치하라고 나와있으니 우선 Ruby환경부터 구성하도록 하겠슨니다.

------------------------
### Ruby 환경 구성  
[Ruby download page](https://www.ruby-lang.org/en/downloads/)를 가면 아래 사진처럼 version controller를 이용하거나 바로 Stable releases를 다운받아라고 나옵니다.
저는 아래 명령어를 사용하여 version controller 중 [RVM](http://rvm.io/)을 설치하였습니다.  
```bash
gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
\curl -sSL https://get.rvm.io | bash -s stable
\curl -sSL https://get.rvm.io | bash -s stable --rails
rvm -v
```    
<br>
![githubpage5](../img/githubpage5.png)  


저 같은 경우는 설치되더라고 rvm이 실행이 안되어서 rvm 설치된 경로로 가서 다음을 실행해주었습니다.
만약 정상적으로 설치 되었으면 아래 이미지 처럼 Version 정보가 나옵니다.
<br>
![githubpage6](../img/githubpage6.png)  

```bash  
source /usr/local/rvm/scripts/rvm
rvm -v
```  
<br>
**편하게 하려면 다음 방법을 추천합니다.**  

```bash  
echo "source /usr/local/rvm/scripts/rvm" >> ~/.bashrc
exec bash
``` 
-------------------
### jekyll gem 설치  
jekyll은 ruby의 gem입니다. 따라서 다음 명령어로 설치할 수 있습니다.  
```bash
gem install jekyll bundler
``` 
<br>
설치가 완료되면 나의 gitpage repository를 받은 후 테스트로 실행을 해봅니다. [위의 설명](Ruby-환경-구성)에서 3번은 [이전 포스팅](https://mike7chu.github.io/Make-githubpage/)에서 repository를 fork뜬 것으로 완료 되었습니다.
아래 명령어는 4번 5번을 실행하는 것입니다.
```bash
cd ~/$(MY_REPOSITORY_PATH)/
bundle exec jekyll serve
```      
<br>
![githubpage7](../img/githubpage7.png)  
<br>
위 사진에서 --host 옵션은 호스팅 할 주소를 옵션으로 주는 것입니다. --port 옵션으로 port도 변경 가능합니다.  

------------------------
## 포스팅  
 _posts/ 아래 경로에 글을 포스팅하고 나서 위 주소<span style="color:orange">(https://localhost:4000)</span>를 입력하면 접속이 가능합니다. 네, 저는 나스에서 위 명령어들을 실행하기 때문에,
host를 변경해주었습니다. host 변경 시 다음 주소로 접근하셔야합니다.<span style="color:orange">(https://HOSTADRESS:4000)</span>  
<br>
![githubpage8](../img/githubpage8.png)  


------------------------
## 마치며  
오늘은 포스팅 및 jekyll 환경 구축을 해보았습니다. 이런 환경이 익숙하지 않았던 저는 많이 애먹었는데 많은 분들이 도움이 되셨으면 좋겠습니다.
다른 오류가 발생하면 메일을 주면시 알려드리도록 하겠습니다. 감사합니다.  
