# this

- 다른 객체지향 언어에서 this는 클래스로 생성한 인스턴스 객체를 의미하므로 클래스에서만 사용할 수 있다.
- 그러나 JS에서의 this는 실행 컨텍스트가 생성될 때 즉, 함수가 호출될 때 결정되며 어디든 사용할 수 있다.

1. 전역 공간

전역 실행 맥락에서 this는 전역 객체를 참조한다.

```
// 웹 브라우저에서는 window 객체가 전역 객체
console.log(this === window); // true

a = 37;
console.log(window.a); // 37

this.b = "MDN";
console.log(window.b)  // "MDN"
console.log(b)         // "MDN"
```

2. 함수 내부

함수 내부에서 this의 값은 함수를 호출한 방법에 의해 결정된다.

2-1. 단순호출

```
var obj = {a: 'Custom'};

var a = 'Global';

function whatsThis() {
  return this.a;  // 함수 호출 방식에 따라 값이 달라짐
}

whatsThis();          // this는 'Global'. 함수 내에서 설정되지 않았으므로 global/window 객체로 초기값을 설정한다.

// this의 값을 한 문맥에서 다른 문맥으로 넘기려면 call()이나 apply()사용

whatsThis.call(obj);  // this는 'Custom'.
whatsThis.apply(obj); // this는 'Custom'.
```

2-2. 객체의 메서드

함수를 어떤 객체의 메서드로 호출하면 this의 값은 그 객체를 사용한다.

```
var o = {
  prop: 37,
  f: function() {
    return this.prop;
  }
};

console.log(o.f()); // 37

```

2-3. 객체의 프로토타입 체인

```
var o = {
  f:function() { return this.a + this.b; }
};
var p = Object.create(o);
p.a = 1;
p.b = 4;

console.log(p.f()); // 5

```
