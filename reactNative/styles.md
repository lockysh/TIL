### Styles
1. stylesheet

https://reactnative.dev/docs/stylesheet

```
import React from "react";
import { StyleSheet, Text, View } from "react-native";

const App = () => (
  <View style={styles.container}>
    <Text style={styles.title}>React Native</Text>
  </View>
);

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 24,
    backgroundColor: "#eaeaea"
  },
  title: {
    marginTop: 16,
    paddingVertical: 8,
    borderWidth: 4,
    borderColor: "#20232a",
    borderRadius: 6,
    backgroundColor: "#61dafb",
    color: "#20232a",
    textAlign: "center",
    fontSize: 30,
    fontWeight: "bold"
  }
});
```

2. styled-components

https://styled-components.com/

리액트 네이티브에서 스타일 컴포넌트 사용하면 import 뒤에 native를 붙여줘야 정상작동한다.

```
import styled from 'styled-components/native';
```

```
const Button = styled.a`
  display: inline-block;
  border-radius: 50px;
  padding: 0.5rem 0;
  margin: 0.5rem 1rem;
  width: 11rem;
  background: transparent;
  color: white;
  border: 2px solid white;
  ${props => props.primary && css`
    background: white;
    color: black;
  `}
`

render(
  <div>
    <Button
      href="https://github.com/styled-components/styled-components"
      target="_blank"
      rel="noopener"
      primary
    >
      GitHub
    </Button>

    <Button as={Link} href="/docs">
      Documentation
    </Button>
  </div>
)
const Button = styled.a`
  display: inline-block;
  border-radius: 50px;
  padding: 0.5rem 0;
  margin: 0.5rem 1rem;
  width: 11rem;
  background: transparent;
  color: white;
  border: 2px solid white;
  ${props => props.primary && css`
    background: white;
    color: black;
  `}
`

render(
  <div>
    <Button
      href="https://github.com/styled-components/styled-components"
      target="_blank"
      rel="noopener"
      primary
    >
      GitHub
    </Button>

    <Button as={Link} href="/docs">
      Documentation
    </Button>
  </div>
)
```

### props로 값 전달 후 스타일 지정

```
// props로 전달할 값 지정

const FollowButton = ({onPress, text, isFollow}) => {
  return (
    <FollowBtn onPress={onPress} isFollow={isFollow}>
      <FollowText isFollow={isFollow}>{text}</FollowText>
    </FollowBtn>
  );
};

const FollowBtn = styled.TouchableOpacity`
  ...
  // 전달된 값을 통해 스타일 지정

  border: ${props => (props.isFollow ? '#b7b4df' : 'white')};
  background-color: ${props => (props.isFollow ? 'white' : '#b7b4df')};
`;

```

- FollowBtn / FollowText 에서 공통적으로 isfollow라는 boolean 값을 전달받아서 팔로우 여부를 판단하여 값에 따라 다른 스타일 지정

### 화면 높이/ 넓이 구하기

```
// import
import { Dimensions} from 'react-native';

// 사용할 값 선언
const {width} = Dimensions.get('window');

// component props로 지정
 <HashTagContainer width={width}>
          {Object.keys(myGenres)
            .filter(a => a !== ('matrix_seq', 'kakao_user_number'))
            .map(tags => {
              return (
                <HashTagBtn>
                  <SelectedTags isSelected={idx.includes(tags)}>
                    {tags}
                  </SelectedTags>
                </HashTagBtn>
              );
            })}
        </HashTagContainer>
...

// style 값 지정
const HashTagContainer = styled.TouchableOpacity`
  width: ${({width}) => width * 0.9};
`;
```
