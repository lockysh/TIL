## extends vs implement

## extends vs implement

: Typescript class 상속의 유형들

1. extends

Classes may extend from a base class. A derived class has all the properties and methods of its base class, and also define additional members.

⇒ class를 그야말로 상속하는 개념으로, 원하는 클래스를 명시하면 해당 클래스의 프로퍼티와 메서드를 따로 구현하지 않아도 부모 클래스의 속성/메소드를 그대로 사용가능하다.

```jsx
class Animal {
  move() {
    console.log("Moving along");
  }
}

class Dog extends Animal {
  woof(times: number) {
    for (let i = 0; i < times; i++) {
      console.log("woof");
    }
  }

const d = new Dog();
// Base class method
d.move();
// Derived class method
d.woof(3);
```

⇒ **다중 상속 불가능**

1. implements

You can use an implements clause to check that a class satisfies a particular interface. An error will be issued if a class fails to correctly implement it.

상속의 느낌보다는 class의 속성이나 메소드에 제약조건을 추가하는 것에 더 가까운 것 같다.

interface로 타입을 지정해줄 뿐, 내부 구현을 상속하는 것은 아니기 때문에 속성이나 메소드를 반드시 override해서 써야 한다.

```jsx
interface Study {
  read(): void;
}

//이것은 가능
class Coding implements Study {
  read() {
    //타입에 내부구현은 정의되어 있지 않으므로, override해야 한다.
    console.log("공식문서를 읽자!");
  }
}

//이렇게 하면 에러
class Coding implements Study {
  //read가 없으므로 에러가 뜬다
  write() {
    console.log("test");
  }
}
```

⇒ **다중 상속 가능**
