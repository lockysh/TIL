# React-Hook-Form

react를 쓰다보면 로그인/회원가입 페이지 만들 때 hooks를 너무 많이 쓰게되는 상황이 오는데 react-hook-form을 사용하면 보다 간단하게 코드를 짤 수 있다.

### 실행방법

1. 터미널에서 설치 : npm i react-hook-form
2. 파일에서 불러오기 : import {useForm} from "react-hook-form"
3. 해당 input 이름 설정후 불러오기

```
const {
    register,
    handleSubmit,
    formState: { errors },
    setValue,
  } = useForm<IForm>({
    defaultValues: {
      email: '@naver.com',
    },
  });

<input  {...register("이름"}>
```

defaultValue : form입력시 초기값 설정(생략가능)

### register : 많은 양의 코드가 필요한 useState()를 대체

```
<input
  {...register('email', {
    required: 'Email is required',
    minLength: {
              value: 5,
              message: 'Your password is too short.',
            },
    pattern: {
    value: /^[A-Za-z0-9._%+-]+@naver.com$/,
        message: 'Only naver.com emails allowed',
            },
  })}
  placeholder='Email'
/>
```

#### register 안에서 원하는 설정들을 할 수 있다.

- required : JS 안에서 필수 값 설정(HTML X)
- pattern : 포함되야하는 값 지정가능
- minlength : 최소 길이

...등등 기본 HTML에 설정하는 값들도 JS안에서 설정가능

value: 설정하고 싶은 값 지정

message: 조건에 부합하지 않았을 경우 에러메세지 설정

### handleSubmit : onSubmit 시 실행 할 함수를 대체

```
onSubmit={handleSubmit(성공 시 실행 함수, 실패 시 실행 함수)}
```

### formState로 에러값들을 불러올 수 있다

```
{errors?.email?.message}
```

위에 코드처럼 {error} 로 미리 꺼내놓은 경우 이렇게 쓰일수 있다.

\*\*form 자체에 대한 에러를 설정하고 싶은 경우 extraError사용

```
{errors?.extraError?.message}
```

## 에러를 설정하는 방법(3)

1. 위에서 다룬 formState :{error} 사용
2. setError 사용

- handleSubmit 지정 시 성공 후 실행되는 함수 안에서 지정할 수 있다.

```
  const onValid = (data: IForm) => {
    if (data.password !== data.password1) {
      setError(
        "password1",
        { message: "Password are not the same" },
        { shouldFocus: true }
      );
      //함수 실행 후 초기값 지정 가능
      setValue("toDo", "")
    }
```

\*shoudFocus는 수정이 필요한 input으로 바로 이동한다.

3. valiadate 사용 : 유효성 검사 시 에러설정

```
<input
  {...register("firstName", {
    validate: {
      noA: (value) =>
        value.includes("A") ? "no A allowed" : true,
      noB: (value) =>
        value.includes("B") ? "no B allowed" : true,
    },
  })}
  placeholder="First Name"
/>
```

- register 안 validate 속성에서 원하는 설정값과 에러메세지를 설정할 수 있다.
