# HOC

HOC는 컴포넌트를 인자로 받아서 새로운 컴포넌트를 리턴하는 "함수"이다.

- 컴포넌트 로직 안에서 재사용할 수 있는 리액트 기술.
- React API와는 관련이 없다.
- 리액트 내에서 상속받거나 재활용하는 방식이 아닌 조합하는 방식이다.

### 주의할점

- render Method 안에서 사용하지 말 것. 이 경우에 render 될 때마다 새로운 컴포넌트를 만들어내는 일이 발생한다.
- static Method은 반드시 따로 복사해있어야 한다. 이 경우 라이브러리를 통해서 쉽게 사용할 수 있다.
- 레퍼런스들은 바로 통과할 수 없다. 이 경우 React.forwardRef를 사용해야 한다.

---

## withRouter

withRouter 함수는 HOC(higher-order component)로 라우터에 의해서 호출된 컴포넌트가 아니어도 match, location, history 객체에 접근할 수 있도록 해준다.

### 사용방법

1.

```
import { withRouter } from 'react-router-dom';

const ShowPageInfo = withRouter(({ match, location }) => {
  return <div>현재 위치: {location.pathname}</div>;
});

export default ShowPageInfo;
```

라우팅을 하는 컴포넌트가 있고, 해당 컴포넌트에서 다른 컴포넌트를 사용하고자 할 때 쓰면 된다.

2.

```
export default wihtRouter(
    function LoginButton(props) {
        function login() {
            setTimeout(() => {
                props.history.push("/");
            },3000);
        }
    return <button onclick={login} />
});
```

작성한 컴포넌트를 withRouter의 인자로 넣어 해당 결과를 사용함으로써 에러가 나지 않으면서 props에 바로 접근할 수 있다.

=> 이 경우엔 경로 설정하는 페이지에서 Redirect로도 해결가능

```
render={()=> ( isLogin ?<Redirect to="/" /> : <Login />)};
```
