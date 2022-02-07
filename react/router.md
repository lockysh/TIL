# React Router

## 1. useHistory -> useNavigate

기존에 useHistory가 v6로 업데이트 되면서 useNavigate로 바꼈다.

- 사용법

```
import { useNavigate } from "react-router-dom";

function App() {
  const navigate = useNavigate();

  return (
    <>
      <button onClick={() => navigate(-1)}>Go back</button>
      <button onClick={() => navigate(1)}>
        Go forward
      </button>
    </>
  );
}
```

Link와 비슷한 기능도 쓸 수 있당.

```
 //메인화면으로 이동
 navigate("/");
```

## 2. Switch -> Routes

마찬가지로 업데이트 되면서

1. 기존의 Switch가 Routes로 바뀌고
2. 경로 지정시 <path="/" elemaents={<이름 />} />로 바뀜

```
import {
  BrowserRouter,
  Routes,
  Route,
  Link
} from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="users/*" element={<Users />} />
      </Routes>
   </BrowserRouter>
  );
}
```

## 3. Typescript hook

typescript를 사용할 떄 useParams의 경우 사용방법이 변경되었다.

```
// 이전 버전
const { name } = useParams<{ name: string }>();

// 업데이트 후
const { id } = useParams<'id'>();
```

## 4. optional parameters 지원 중지

기존 버전에서 "?"를 붙여 parameter의 선택적 존재여부를 명시해주던 문법이 사라졌다.

```
<Route path="/search" element={<SearchPage/>}>
  <Route path=":keyword" element={<SearchPage/>} />
</Route>
```

이 경우 이런식으로 중첩 router를 사용해서 해결 가능하다.
