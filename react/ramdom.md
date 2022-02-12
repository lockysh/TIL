# ramdom

프로젝트 진행 도중 Math.random()을 활용해서 랜덤으로 질문을 반환하는 코드를 짰다.

```
function questionlist() {
  const questions: any = [1, 2, 3, 4, 5, 6, 7, 8, 9];
  const randomQuestion =
    questions[Math.floor(Math.random() * questions.length)];

  return <div>{randomQuestion}</div>;
}

export default questionlist;

```

Math.ceil()을 하면 첫번째 값이 호출이 안되기 때문에 Math.floor()을 해줬다.
