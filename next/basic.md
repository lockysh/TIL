# Next.js

[https://nextjs.org/docs/getting-started](https://nextjs.org/docs/getting-started)

기본 개념 ⇒ react로 만드는 서버사이드 렌더링 프레임워크.

클라이언트 렌더링 단점 보완:

- 클라이언트 렌더링의 경우 모든 js 파일을 로드하고 사용자가 웹을 보기까지 많은 시간을 대기해야함.

⇒ 서버에서 자바스크립트를 로딩함으로 클라이언트 측에서는 자바스크립트를 로딩하는 시간이 줄어듬

- seo 문제 - 클라이언트 사이드의 경우 자바스크립트가 로드 되지 않았을때 구글의 검색엔진의 경우 자바스크립트가 로드되지 않은 페이지를 검색엔진으로 스캔함으로 결론적으로 검색에 아무 페이지도 안나옴.

⇒ 검색엔진이 자바스크립트를 읽는 것이 아닌 서버 측에서 자바스크립트를 만들어 컨텐츠를 직접 업로드(검색ㅇ)

next.js 의 주요 기능

hot reloading/automatic routing/ single file components/ server landing/ code splitting
