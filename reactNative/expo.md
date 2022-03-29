# Expo go

expo go를 이용하여 앱을 개발하면서 java나 xcode의 설치없이 테스트 해볼 수 있다.

사용방법

0. 핸드폰에 expo go 설치 후 회원가입

1. npm install --global expo-cli

2. expo init [프로젝트명]

=> 이 과정에서 CategoryInfo : 보안 오류: (:) [], PSSecurityException가 발생하면

1.PowerShell을 윈도우 검색창에 검색 후 '관리자로 실행'
2.Set-ExecutionPolicy -ExecutionPolicy Unrestricted 입력 후 질문이 나오면 'A' (모두 예) 키를 입력
3.expo init 파일명 실행하시면 오류 해결..

3. expo login : id/pw입력

4. npm start 하면 폰으로 바로 연동된다. (같은 네트워크 환경에서 실행해야함!)
   => 이 과정에서 timeout 에러가 나면 방화벽 고급 설정에서 19000~19002포트를 추가해보거나 연결환경을 LAN에서 tunnel로 변경하면 된당.