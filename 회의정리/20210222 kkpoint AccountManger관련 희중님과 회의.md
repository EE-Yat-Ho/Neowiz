[ 20210222 로그인 관련 사항 내부회의 ]
- AccountManager
isLogged
name
email
social
accessToken
refreshToken

- UserDefault
accessToken
refreshToken
자동 로그인 켜진 상태면 앱 실행시마다 토큰으로 이전 로그인 체킹 + 자동 로그인
( 로그인시 자동로그인 체크했으면 유저 디폴트에 true )
( 로그아웃 할때만 false )
