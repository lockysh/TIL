## Typescript + React

#### useState
```
   const [value, setValue] = useState<string>("");
```
- useState 사용시 **useState<number | string>** 이런식으로 타입을 지정해주면 된다.

#### event & target

```
  const onChange = (event: React.FormEvent<HTMLInputElement>) => {
    const {
      currentTarget: { value },
    } = event;
    setValue(value);
  };
```

- event를 쓸 때도 마찬가지로 타입을 지정해줘야한다. : **React.FormEvent** 사용.
 
- < HTMLInputElement >를 붙여서 onChange 함수가 HTML의 input 항목을 바꾼다는 것을 타입스크립트에게 알려준다.
- target이 아닌 currentTarget을 사용한다. (기능은 같당)
