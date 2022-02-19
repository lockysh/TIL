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
