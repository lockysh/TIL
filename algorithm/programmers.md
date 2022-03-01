# 프로그래머스 Lv.1

프로그래머스 코딩테스트를 풀면서 사용한 개념 간단 정리

### Array

- Array(n).fill(x) : 배열 안에 n개의 인자들을 x로 채움

- Array(n).push(x) : 배열 뒤에 x추가

- reduce(()=> {}) : 배열 안 요소들에 reduce 안에 들어가는 함수가 적용됨.

-splice() : 배열의 기존 요소를 삭제,교체, 추가할 수 있다.(원본 배열 자체를 수정할 수 있음)

-Math.min()/Math.max() :배열에서 사용하려면 ES6의 destruction 할당 사용. (Math.min(...Array))

- filter(function) : function의 기준대로 배열 속 요소를 거를 수 있다.

### methods

- "".repeat(x) : x만큼 ""안에 문자열 반복

- string.substring(a,b) : 문자열의 a번째부터 b까지 반환

- string.slice(a,b) : 문자열의 a부터 b까지 반환

- split('') & split(' ') : 전자는 모든 요소를 다 나누고, 후자는 띄어쓰기를 기준으로 나눈다.

-join('') & join(' ') : 전자는 공백없이 합쳐지고, 후자는 띄어쓰기 제외하고 합쳐진다.

- sort((a,b) => b-a) : 내림차순으로 정렬
- sort().reverse() : 유니코드에 따라서 내림차순 정렬

- Math.sqrt() / Math.pow : 제곱근/ 제곱수

- 문자열 정수로 바꾸는 법 : Number() , +, 1을 곱하거나 나누기.

- includes(x) : x를 포함하는지 확인할 수 있음

- match() :

- every() :
