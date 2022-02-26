# 프로그래머스 Lv.1

프로그래머스 코딩테스트를 풀면서 사용한 개념 간단 정리

### Array

- Array(n).fill(x) : 배열 안에 n개의 인자들을 x로 채움
- Array(n).push(x) : 배열 뒤에 x추가

- reduce(()=> {}) : 배열 안 요소들에 reduce 안에 들어가는 함수가 적용됨.

-splice() : 배열의 기존 요소를 삭제,교체, 추가할 수 있다.(원본 배열 자체를 수정할 수 있음)

-Math.min()/Math.max() :배열에서 사용하려면 ES6의 destruction 할당 사용. (Math.min(...Array))

### functions

- "".repeat(x) : x만큼 ""안에 문자열 반복
- string.substring(x) : 문자열의 x번째부터 끝까지 반환
