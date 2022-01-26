## Styled-components

## 비슷한 스타일을 갖는 경우 

```
const Box = styled.div`
  background-color: "red";
  width:200px;
  height:200px;
`;

const Circle = styled(Box)`
    background-color: "blue";
    border-radius: 50%;
`;
```

두개 이상의 컴포넌트에 적용하고자 하는 스타일이 비슷할 때 (ex. 배경 색만 다르게) 
우선 해당 컴포넌트를 하나를 만들고 **styled(컴포넌트 이름)** 을 사용하면 된다.

#### 조금 더 효율적인 코드

- 컴포넌트에 props를 설정해서 해당 값을 불러오게 할 수 있다.

```
<Box bgColor="tomato" />
<Circle bgColor="blue" />

const Box = styled.div`
  background-color: ${(props) => props.bgColor};
  width:200px;
  height:200px;
`;

const Circle = styled(Box)`
  border-radius: 50%;
`;
```
배경색을 bgColor에 설정해두고 밑에서 ${(props) => props.bgColor}로 지정하면 된다.

## as

-as를 사용하여 styled.div로 만든 값도 간단하게 다른 태그로 변결할 수 있다.

```
<Box as= "h3" />
<Circle as="h3" />
```

## attrs

attrs를 사용해서 컴포넌트에 미리 속성을 전달할 수 있다.
```
const Input = styled.input. **attrs({ required: true })**
```
이러면 추후에 Input을 재사용할 때 직접 required를 해주지 않아도 된다!

## animation

우선 keyframes를 불러온다.

```
import {keyframes} from "styled-components";
```

```
const rotationAnimation = keyframes`
  0% {
    transform:rotate(0deg);
    border-radius:0px;
  }
  50% {
    border-radius:100px;
  }
  100%{
    transform:rotate(360deg);
    border-radius:0px;
  }
`;
```
간단하게 빙글빙글 돌아가는 도형 완성!

이렇게 애니메이션을 스타일을 지정해준 뒤에 해당 스타일을 원하는 컴포넌트의 styled안에서 **animation: ${rotationAnimation}** 를 설정하면 된다.

#### (&: hover) 을 통해 간단하게 hover을 입혀줄 수 있다. 