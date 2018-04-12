---
layout: post
title:  "[windows] cmder 터미널을 특정 폴더에서 바로 열기"
date:   2018-04-12 13:50:00 +0900
categories: FrontEnd
---
### Problem
1. 윈도우에서 기본으로 제공되는 터미널은 Copy & Paste 및 창사이즈 조절에 제한이 있어 불편
2. 터미널에서 cd 명령을 이용해 특정 경로로 이동하는 것도 귀찮고
<br>
<br>

### Solution
1. 잘 알려진 [윈도우용 터미널 cmder](http://cmder.net/) 를 `C:\cmder_mini` 경로에 설치한다.  
(설치 경로를 변경하고자 한다면 아래 레지스트리 편집기 내용을 수정하면 된다.)
![img0](/images/addCmder0.png)

2. 마우스 오른쪽 메뉴에 바로가기 등록을 위해 아래 레지스트리 편집 명령을 사용한다.
- 마우스 오른클릭 메뉴에 바로가기 등록: [AddCmder.reg](/files/AddCmder.reg)
- 관리자 권한 실행 : [AddCmderAdmin.reg](/files/AddCmderAdmin.reg)
- 등록했던 바로가기 삭제: [DelCmder.reg](/files/DelCmder.reg)
- 관리자 권한 실행 삭제: [DelCmderAdmin.reg](/files/DelCmderAdmin.reg)

3. 특정 경로에서 마우스 오른 클릭을 하면 바로가기 가능!
![img1](/images/addCmder1.png)
<br>
<br>
![img2](/images/addCmder2.png)
<br>
<br>


### Ref.
<http://minq.tistory.com/667>
