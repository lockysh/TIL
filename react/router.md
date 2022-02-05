# React Router

### 1. useHistory -> useNavigate

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

2. Switch -> Routes

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
