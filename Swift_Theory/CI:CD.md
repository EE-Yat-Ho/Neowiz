# CI/CD

[ CI ( Continuous Integration ) 공부 ]
자동 빌드 및 테스트!!
CD( Continuous Deployment )가 자동 배포!

종류
1. Xcode server : 애플에서 서비스하고, 인증서 관리도 편함. 웹으로 접근도 가능(오 유료 서버 불필요? 하긴 개발자 계정이 얼만데 ㅡㅡ) / Xcode랑 깃 연동 필요, 배포(Test Flight 등)는 자동화 안해줌.

Xcode 프리퍼런스에서 서버 & 봇을 킴
설정에서 Xcode Helper 권한을 주라함 줌 ㅇㅇ
Xcode 서버 & 봇의 퍼미션을 올 유저로 줌 -> 3가지 선택지가 있음
Accounts로 감
좌측하단 + 버튼으로 Xcode Server 추가.

야이씨 쉘로 커밋하니까 자동 빌드 안함 ㅡㅡ
서버는 지금 나의 맥..! 유료서비스 없이 집에있는 맥북을 서버로 그냥 쓸수도있다는 소리..? 는 아니쥐

2. JenKins
불편한 만큼 커스텀이 짱짱

로컬 젠킨스 시작
$ docker pull jenkins/jenkins:lts
$ docker run -d \
    -p 8080:8080 -p 50000:50000 \
    --name jenkins jenkins/jenkins:lts
    
20210215
야이씌 그냥 jenkins start 하면됨;
jenkins stop
jenkins restart도 됨..


3. Fastlane

4. Github actions

4종류 모두 포스팅하기


무료 서버
네이버 1년
aws 1년
오라클 무제한 


와 오라클 가입..
VM 인스턴스 생성..
ssh 접속.. 까지 성공!!

[ ssh 접속 ]
https://docs.oracle.com/en-us/iaas/Content/Compute/Tasks/accessinginstance.htm# 여기서 리눅스 인스턴스에 연결에 SSH 보면됨!
ssh -i /Users/EEYatHo/Desktop/Neowiz/sshKey/Oracle_Cloud_Free_tier/ssh-key-2021-02-09.key opc@193.123.227.179

모 일단 VM 인스턴스가 기본적으로 ssh가 깔려있는건지, 다 깔려있는건지 환경세팅은 잘 모르것음
그런데 리눅스 환경에서 ssh접속시 root는 기본적으로 opc임.
ip는 공용 ip임.
key는 공개키 말고 개인키고,
chmod 400으로 읽기모드로 바까줘야함.

여기 있는 애들 ls만 치면 안보이는 이유가 다 숨김파일이라 ( 앞에 .이 붙은 친구들 ) 그럼.
그래서 ls -a 로 숨김파일까지 다 보기로 봐야 보임.

헛짓거리 하다가
스토리지 서비스로 넘어옴..

스토리지 서비스로 업로드하는 스크립트 찾는 와중에
CLI로 하는 방법 있길래 찾아보니까 homebrew로 oci-cli 라는걸 깔아야함..

oci-cli를 세팅하는 작업이 필요. ( 아무나 내 스토리지에 올릴순없자너 )
파이썬 설치,
파이썬 가상환경 세팅,
oci-cli 설치,
oci-cli 세션 시작,

https://mproject.tistory.com/32 와 규ㅜ세주..
https://thekoguryo.github.io/oci/chapter14/1/2/2/ 캬 이게되네


- 명령어 정리
인스턴스에 콘솔로 접속 : 
ssh -i [개인키] opc@193.123.227.179
ssh -i /Users/EEYatHo/Desktop/Neowiz/sshKey/Oracle_Cloud_Free_tier/ssh-key-2021-02-09.key opc@193.123.227.179

파일 보내기 : 
scp -i [개인키] [보낼파일] opc@193.123.227.179:[보낼경로]
scp -i /Users/EEYatHo/Desktop/Neowiz/sshKey/Oracle_Cloud_Free_tier/ssh-key-2021-02-09.key /Users/EEYatHo/Desktop/Neowiz/sshKey/Oracle_Cloud_Free_tier/test.png opc@193.123.227.179:CD
