# Firebase

## setting

vscode에서 세팅하기 전 firebase 홈페이지에서 새로운 프로젝트를 추가해서 SDK를 만들어놓아야함

1. npm install firebase
2. 파일에 SDK 추가(깃허브에 올릴 때 보안 목적으로 .env 파일에 상세 주소 적어놓기)

```
import { initializeApp } from 'firebase/app';

const firebaseConfig = {
  apiKey: process.env.REACT_APP_API_KEY,
  authDomain: process.env.REACT_APP_AUTH_DOMAIN,
  projectId: process.env.REACT_APP_PROJECT_ID,
  storageBucket: process.env.REACT_APP_STORAGE_BUCKET,
  messagingSenderId: process.env.REACT_APP_MESSAGING_ID,
  appId: process.env.REACT_APP_APP_ID,
  measurementId: process.env.REACT_APP_MEASUREMENT_ID,
};

const app = initializeApp(firebaseConfig);
```

3. 사용이 필요한 시점에 함수를 추가적으로 import 해준다.

ex) auth 기능이 필요한 경우

- <firsbase 파일>

```
import { getAuth } from 'firebase/auth';

export const auth = getAuth(app);
```

- <해당 기능 필요한 파일>

```
import { auth } from '../firebase';
```

## Authentication

firebase를 이용하면 간편하게 signup/signin을 구현할 수 있다.

```
import { createUserWithEmailAndPassword, signInWithEmailAndPassword } from 'firebase/auth';
import { auth } from '../firebase';
```

- signup

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

- signin

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
