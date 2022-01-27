## styled-components

### Theme 추가방법

 우선 src 폴더안에 styled.d.ts 파일을 새로 만들어 준 후 아래 코드를 작성한다.
```
import "styled-components";

declare module "styled-components" {
  export interface DefaultTheme {
    textColor: string;
    bgColor: string;
    btnColor: string;
  }
}
```
{} 안에 지정하고자 하는 프로퍼티들 타입을 지정해주고 theme.ts 파일을 새로 만들어준다.

그 후 themes.ts 파일에서 DefaultTheme를 불러온 후 자유롭게 작성하면 된다.
```
import { DefaultTheme } from "styled-components";

export const lightTheme: DefaultTheme = {
  bgColor: "white",
  textColor: "black",
  btnColor: "tomato",
};

export const darkTheme: DefaultTheme = {
  bgColor: "black",
  textColor: "white",
  btnColor: "teal",
};
```
#### 다만 두 파일의 프로퍼티 이름&종류는 같아야 한다.