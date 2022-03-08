# 프로그래머스 Lv.1

프로그래머스 코딩테스트를 풀면서 사용한 개념 간단 정리

### Array

- Array(n).fill(x) : 배열 안에 n개의 인자들을 x로 채움

- Array(n).push(x) : 배열 뒤에 x추가

- reduce((a,b,i)=> {} , 0) : 배열 안 요소들에 reduce 안에 들어가는 함수가 적용됨. => a의 초기값을 0으로 설정. b는 현재 값, i는 현재 인덱스.

- splice() : 배열의 기존 요소를 삭제,교체, 추가할 수 있다.(원본 배열 자체를 수정할 수 있음)

- Math.min()/Math.max() :배열에서 사용하려면 ES6의 destruction 할당 사용. (Math.min(...Array))

- filter(function) : function의 기준대로 배열 속 요소를 거를 수 있다.

- every() : 배열의 각 요소에 대해서 테스트 함수의 값이 모두 true인지 확인. (하나라도 false면 false)

- some() : 배열의 각 요소에 대해 테스트 함수의 반환 값이 하나라도 true가 있는지 확인.(하나라도 true면 true)

-a.pop() : 배열 맨 뒤의 요소를 삭제.

### methods

- "".repeat(x) : x만큼 ""안에 문자열 반복

- string.substring(a,b) : 문자열의 a번째부터 b까지 반환

- string.slice(a,b) : 문자열의 a부터 b까지 반환

- split('') & split(' ') : 전자는 모든 요소를 다 나누고, 후자는 띄어쓰기를 기준으로 나눈다.

- join('') & join(' ') : 전자는 공백없이 합쳐지고, 후자는 띄어쓰기 제외하고 합쳐진다.

- sort((a,b) => b-a) : 내림차순으로 정렬
- sort().reverse() : 유니코드에 따라서 내림차순 정렬

- Math.sqrt() / Math.pow : 제곱근/ 제곱수

- 문자열 정수로 바꾸는 법 : Number() , +, 1을 곱하거나 나누기.

- includes(x) : x를 포함하는지 확인할 수 있음

- match() : 특정 텍스트 안에 찾고싶은 단어가 있는 경우 해당 텍스트가 문구에 포함되어 있는지 확인 가능.

- n.toString(number) : n을 number진법으로 간편하게 변환 가능.

### Set 객체

set 객체는 중복되지 않는 유일한 값들의 집합으로 동일한 값을 중복하여 포함할 수 없고 인덱스로 요소에 접근할 수 없다.

객체 생성 : new Set
// .add .delete .has .size .clear
