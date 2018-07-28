---
layout: post
title:  "jekyll 블로그 테마 변경"
date:   2018-07-28 01:00:00 +0900
categories: memo
---
### 테마를 변경하고자 할 때
가끔 집안의 가구 배치를 바꾸면 새로운 기분이 드는 것 같이 블로그의 옷도(theme) 가끔씩 갈아 입혀주면 기분전환에 좋다.

지킬 블로그를 처음 개설하고 디폴트 테마인 minima 로 몇개월간 운영을 해왔는데 다른 블로그들의 멋진 테마들을 보고 욕심이 나서 내 블로그에도 새 옷을 입혀 보기로 했다

<br>
### 적절한 테마 고르기 
지킬블로그 테마는 [jekyllthemes.org](http://jekyllthemes.org) 에서 여러 종류의 테마들을 확인할 수 있다. 나는 심플함과 미니멀리즘의 향기가 듬뿍 묻어나는 [whiteglass](https://yous.be/whiteglass/) 가 마음에 들었다.

<br>
### 테마를 설치하는 방법
1. Gemfile 에 다음을 추가
```
gem "jekyll-whiteglass"
```
1. _config.yml 파일에 다음을 추가
```
theme: jekyll-whiteglass
```
1. 터미널에서 다음을 실행
```
$ bundle
```

테마를 설치할 때 테마관련 리소스들은 현재 나의 블로그 폴더에 직접 설치되는 것은 아니고 ruby 라이브러리 폴더에 전역으로 설치가 된다. 그리고 지킬서버가 시작될 때는 _config.yml 파일의 theme 설정에 따라 전역의 테마를 참조해 블로그가 빌드된다.

기본 테마 양식을 그대로 사용하지 않고 커스터마이징을 하고자 한다면 ruby 라이브러리가 설치되는 경로에서 아래 테마관련 리소스들을 직접 나의 블로그 폴더에 복사해서 넣은 후 수정해야 한다

테마가 설치된 경로는 지킬 블로그 경로에서 아래 명령으로 확인할 수 있다
```
$ bundle show whiteglass
/Library/Ruby/Gems/2.3.0/gems/jekyll-whiteglass-1.7.0
$ 
```
해당 경로에 들어가서 _includes, _layouts, _sass, assets 4가지 폴더를 내 블로그 폴더로 복사해 넣은면 내 입맛에 맞게 디테일을 수정할 수 있다
```
$ cd /Library/Ruby/Gems/2.3.0/gems/jekyll-whiteglass-1.7.0
$ ls -al
total 40
drwxr-xr-x    9 root  wheel   288  7 27 23:50 .
drwxr-xr-x  150 root  wheel  4800  7 28 02:30 ..
-rw-r--r--    1 root  wheel  1044  7 27 23:50 CHANGELOG.md
-rw-r--r--    1 root  wheel  1079  7 27 23:50 LICENSE.txt
-rw-r--r--    1 root  wheel  9834  7 27 23:50 README.md
drwxr-xr-x   12 root  wheel   384  7 27 23:50 _includes
drwxr-xr-x    9 root  wheel   288  7 27 23:50 _layouts
drwxr-xr-x    4 root  wheel   128  7 27 23:50 _sass
drwxr-xr-x    3 root  wheel    96  7 27 23:50 assets
$ 
```

<br>
### github-pages 블로그를 사용하는 경우 주의사항
위와 같이 신나게 테마를 선택하고 커스터마이징해서 깃헙페이지에 배포했을 때 github 으로부터 아래와 같은 이상한? 메일이 한통 들어왔다.

> The page build completed successfully, but returned the following warning for the `master` branch:

> You are attempting to use a Jekyll theme, "jekyll-whiteglass", which is not supported by GitHub Pages. Please visit https://pages.github.com/themes/ for a list of supported themes. If you are using the "theme" configuration variable for something other than a Jekyll theme, we recommend you rename this variable throughout your site. For more information, see https://help.github.com/articles/adding-a-jekyll-theme-to-your-github-pages-site/.

> For information on troubleshooting Jekyll see:

> - https://help.github.com/articles/troubleshooting-jekyll-builds

> If you have any questions you can contact us by replying to this email.

whiteglass는 github-pages 블로그에서 공식적으로 지원하는 테마가 아니라는 안내메세지였다. 서비스는 가능하지만 jekyll 버젼에 따른 차이로 일부 기능 사용에 제약이 있을 수 있다. whiteglass 의 경우에는 categories 기능에 오류가 있었다

github-pages 에서 공식적으로 지원하는 테마 종류는 아래 링크에서 확인할 수 있다
https://pages.github.com/themes/

