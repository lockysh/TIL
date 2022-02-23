# SPA deploy

특징

1. 서버에 모든 요청을 하고 받아오는 형태가 아님.
2. 라우팅 경로에 상관없이 리액트 앱을 받아 실행 후에 적용됨.
3. static 파일을 제외한 모든 요청을 index.html로 응답하도록 작업 -> 404같은 페이지가 문제 없이 동작되도록 함.

4. serve -s build

```
npm install serve -g //전역 설치
serve -s build
```

-s 옵션은 어떤 라우팅으로 요청해도 index.html을 응답하도록 한다.

2. AWS S3에 배포
3. node.js express

```
npm i express

const express = require('express');
const path= require('path');

const app = express();

app.use(express.static(path.join(__dirname, 'build')));

// static 외 경우 처리
app.get('*', (req, res) => {
    res.sendFile(path.join(__dirname, 'build', 'index.html'));
});

app.listen(9000);
```
