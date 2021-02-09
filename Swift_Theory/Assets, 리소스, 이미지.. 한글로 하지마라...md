[ ㅡㅡ ]
( xcode git clone unassigned )
깃헙에서 클론했을때 처음 빌대할때 이미지셋 이상한건가?
맙소사 그러하다..

후우 에셋 이미지들 다시 세팅하고 클린빌드하면 되긴하네
클린 된거 깃에 올리고 다시 받아도 안되냐?

https://stackoverflow.com/questions/50504242/xcode-some-image-assets-appear-unassigned-after-git-clone
xcode 가 영어 외의 문자를 읽는데에 취약한 것으로 생긴 버그로 추측.
에셋에 한글인 애들 영어로 다 바꾸고있는데..
xcode에서만 바꾸면 파일명은 한글이라 ㅋㅋ 아에 다시 넣어줘야할듯 ㅠ
그렇게 다 영어로하니까 깃에서 받아도 잘 받아먹네.....후우..

와 단순노동 오지게해서 다 바꿨따..

첨엔 xcode server 문젠줄 알았는데 알고보니 깃 클론시 엑스코드가 한글 에셋을 잘 못붙히는 거였음.. ㅇㅋㅇㅋ; 포스팅거리 ㄱㅇㄷ
