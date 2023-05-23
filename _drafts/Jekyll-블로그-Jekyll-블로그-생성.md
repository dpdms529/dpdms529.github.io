---
layout: single
title: "[Jekyll 블로그] Jekyll 블로그 생성"
excerpt: ""
date: 2023-05-20 00:00:00
toc: true
toc_sticky: true
use_math: true
categories: [Experiences, Jekyll 블로그]
tags: [Experiences, Jekyll 블로그]
---

블로그를 한동안 방치했었는데 시간도 생겼고, 다시 잘 운영해보고 싶어서 싹 밀고 새로 만들었다. 한 번 했었으니깐 다시 만들면 금방 만들 줄 았았는데 생각보다 오래 걸렸다... 혹시 또 jekyll 블로그를 새로 만들고 싶어질지도 모르니깐 블로그 생성 과정을 정리해보려고 한다.

## 설치
[Jekyll 위도우 설치](https://jekyllrb.com/docs/installation/windows/)

jekyll을 사용하기 위해서는 먼저 ruby를 설치해야 한다. 나는 window를 쓰고 있기 때문에 [RubyInstaller](https://rubyinstaller.org/)를 통해 ruby를 설치해줬다.

설치 마지막 단계에서 `ridk install`을 체크해준 후 finish 버튼을 누르면 아래와 같은 화면이 띄어진다. 
![Ruby ridk install](https://github.com/dpdms529/dpdms529.github.io/assets/60471550/d8f549db-f437-41a1-8b63-0f2d28674836)
문서 내용으로는 3번만 설치해주면되는거 같지만 나는 그냥 Enter를 눌러서 다 설치해줬다.

ruby 설치가 모두 끝나면 cmd 창에서 `gem install jekyll bundler`을 통해 jekyll과 bundler를 설치해준다. 설치가 끝나면 `jekyll -v`을 통해 jekyll이 제대로 설치됐는지 확인해준다.

## Minimal Mistakes
[Minimal Mistakes 가이드 문서](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)

jekyll theme에는 여러가지가 있는데 나는 Minimal Mistakes를 골랐다. 원래도 이 테마를 썼었는데 가이드 문서가 잘 되어있고, 많은 사람들이 사용하다보니 참고할 글도 많아서 커스터마이징할 때 생기는 문제들을 해결할 때 도움이 많이 됐었어서 그대로 쓰기로 했다.

테마를 설치하는 방법은 여러가지가 있는데 나는 [Github repo](https://github.com/mmistakes/minimal-mistakes)에서 clone해오는 방법을 선택했다.
![minimal-mistakes clone](https://github.com/dpdms529/dpdms529.github.io/assets/60471550/9cd66fca-12c4-49a2-95db-8ed8db57590b)
1. `cd` 명령어로 블로그를 만들 위치로 이동
2. [minimal-mistakes repo](https://github.com/mmistakes/minimal-mistakes)에서 클론할 주소를 복사
    ![minimal-mistakes](https://github.com/dpdms529/dpdms529.github.io/assets/60471550/85e39e2f-cc31-43ae-b5bc-9adebe8f9915)
3. `git clone '복사한 주소'`
    폴더명을 다르게 설정하고 싶다면 `git clone '복사한 주소' 폴더명`으로 해주면 된다.
4. `cd '폴더명'` : 생성된 폴더로 이동


 ![디렉터리 구조](https://github.com/dpdms529/dpdms529.github.io/assets/60471550/013e51b2-d74d-402f-9606-f3c7bb5b58b3){: width="400" height="400"}
 
 클론해오면 위와 같은 디렉터리 구조를 가지는데 빨간 박스 표시를 한 폴더 및 파일들은 예시를 위한 것들이기 때문에 지워주면된다.
