# Typescript

## 설치방법

- 리액트에서 타입스크립트를 사용하길 원하는 경우 npx create-react-app 앱이름 **--template typescript** 을 붙여주면 된다.

- 초기에 타입스크립트를 지정하지 않고 중간에 설치할 경우 터미널에
**npm i --save typescript @types/node @types/react @types/react-dom @types/jest** 를 설치해준다.

#### 코드 실행 전에 오류를 인식하는 것이 Proptypes와의 차이점이당.

## styled-components 

styled-components를 사용하려는 경우 터미널에 **npm i --save-dev @types/styled-conpoments** 를 설치하여 타입스크립트가 타입을 인식할 수 있도록 해야한다.


## 타입지정방법

```
interface ContainerProps {
	bgColor: string;
}
function Container({bgColor} : ContainerProps) {
 return ();
}

const Container = styled.div<ContainerProps>``;
```
타입을 지정하고자 하는 컴포넌트를 interface 를 통해 내부에 설정하면 된다.

### optional type 설정방법

```
bgColor?: string;
```
- 타입지정시 "?" 불여주기 
```
bgColor: string | undefined
```
- | undefined 사용

