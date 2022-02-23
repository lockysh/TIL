# context api

context를 이용하면 단계마다 props를 넘겨주지 않고도 컴포넌트 트리 전체에 데이터를 제공할 수 있다.

- 사용방법 : 가장 상위 컴포넌트에서 데이터를 set한 뒤에 컨슈머나 useContext로 get하면 된다.

### Date Set

1. 컨텍스트 생성(context api)

```
const PersonContext = createContext();
```

2. 상위 컴포넌트에서 context.Provider 사용

```
const persons = [
    {id: 0 , name: 'hello' }
];

<PersonContext.Provider value = {persons}>
    <App />
</PersonContext.Provider>
```

### Date Get (1) Consumer

```
<PersonContext.ConSumer>
    {(persons)=> (
        <ul>
            {persons.map((person)=> (
                <li>{person.name}</li>
            ))}
        </ul>
    )}
</PersonContext.ConSumer>
```

### Data Get (2) useContext

```
const persons = useContext(PersonContext);
        <ul>
        {persons.map((person)=> (
            <li>{person.name}</li>
        ))}
    </ul>

```
