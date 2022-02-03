# Authentication

firebase의 auth기능을 이용하면 간편하게 signup/signin을 구현할 수 있다.

- 기본세팅 : <firsbase 파일>

```
import { getAuth } from 'firebase/auth';

export const auth = getAuth(app);
```

- <해당 기능 필요한 파일>

```
import { auth } from '../firebase';
```

## email & password 사용

```
import { createUserWithEmailAndPassword, signInWithEmailAndPassword } from 'firebase/auth';
import { auth } from '../firebase';
```

- Signup(createUserWithEmailAndPassword)

: async/ await을 사용하여 회원가입을 하는 함수코드 작성

```
  const handleSignUp = async (event: any) => {
    event.preventDefault();
    try {
      await createUserWithEmailAndPassword(auth, userEmail, userPw);
      navigate('/');
    } catch (error: any) {
      alert(error.message);
    }
```

- Signin(signInWithEmailAndPassword)

```
  const handleSignIn = async (event: any) => {
    event.preventDefault();
    try {
      await signInWithEmailAndPassword(auth, userEmail, userPw);
      navigate('/');
    } catch (error: any) {
      alert(error.message);
    }
  };
```

-Signout

```
import { signOut } from 'firebase/auth';

  const logout = async () => {
    await signOut(auth);
  };
```

아주아주 간편하게 코드 한 줄로 signout 할 수 있다.

## onAuthStateChanged

signin 기능 구현 후 바로 새로고침이 되지 않기 때문에 현재 상태에 따라 화면을 바꿔줘야 하는 경우에 onAuthStateChanged를 사용하면 된다.

ex)

```
  useEffect(() => {
    auth.onAuthStateChanged((user: any) => {
      if (user) {
        setUserName(user.email);
        setIsLoggedIn(true);
      }
    });
  }, []);
```
