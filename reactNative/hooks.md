# Hook
- useEffect vs useLayoutEffect

: 두 hook의 가장 큰 차이점은 실행 시점이다

### useEffect

<동작과정>

컴포넌트 렌더링 - 화면 업데이트 - useEffect실행

=> 비동기적으로 실행됨,

DOM과 인터렉션이 없는 경우에 사용(대부분 경우)

### useLayoutEffect :

<동작과정>

컴포넌트 렌더링 - useLayoutEffect 실행 - 화면 업데이트

=> 동기적으로 실행됨,

렌더링 직후 DOM요소의 값을 읽을 때 유용함(scroll position등),

DOM을 mutate할 경우에 사용

// useEffect를 사용할 경우 effect가 실행됨과 동시에 DOM에 mutation이 일어날 경우 flickering이 발생할 수 있다. 이러한 경우 useLayoutEffect를 사용해서 flickering을 막을 수 있다.
