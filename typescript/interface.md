# Interface vs Type

## type vs interface

: 둘 다 객체 타입의 이름을 지정하는것

### Type alias

```jsx
type Point = {
  x: number,
  y: number,
};

type SetPoint = (x: number, y: number) => void;
```

### Interface

```jsx
interface Point {
  x: number;
  y: number;
}

interface SetPoint {
  (x: number, y: number): void;
}
```

<차이점>

1. **상속받는 방법**

   interface는 extends를 type에서는 &를 이용해 상속을 통한 확장을 한다.

   ```jsx
   interface interface1 {
     a: string;
   }

   interface interface2 extends interface1 {
     b: string;
   }

   const interfaceConst: interface2 = {
     a: "a",
     b: "b",
   };

   type type1 = {
     a: string,
   };

   type type2 = type1 & {
     b: string,
   };

   const typeConst: type2 = {
     a: "a",
     b: "b",
   };
   ```

2. **선언적 확장 / 자동 확장**

   interface는 같은 이름의 객체를 다시 한번 선언하면 자동으로 확장이 되지만, type은 불가능하다.

   ```jsx
   interface interface1 {
     a: string;
   }
   interface interface1 {
     b: string;
   }
   ```

   ⇒ 가능 ( 문제없음 )

   ```jsx
   type type1 = {
     a: string,
   };
   type type1 = {
     b: string,
   };
   ```

   ⇒ 불가능

3. **type alias 방식에서는 intersection(&), union(|) 키워드와 tuple 사용 가능**

```jsx
type PartialPointX = { x: number };
type PartialPointY = { y: number };

// intersection
type IntersectionPoint = PartialPointX & PartialPointY;

// union
type UnionPoint = PartialPointX | PartialPointY;

// tuple
type Data = [number, string];
```

4. **type alias는 VSCode 상에서 프리뷰 기능을 통해 해당 타입 내의 속성 정보 조회 가능**

interface 키워드로 선언된 타입의 경우에는 인터페이스명만 조회됨
