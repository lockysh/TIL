# React navigation
### get started

1. 터미널에 설치

```
npm install @react-navigation/native

npm install react-native-screens react-native-safe-area-context

npm install @react-navigation/native-stack
```

2. 최상단에 NavigationContainer로 감싸주기
3. createNativeStackNavigator()을 사용하여 Stack.Navigatior 안에 Stack.페이지 만들기

```
import * as React from 'react';
import { View, Text } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

function HomeScreen() {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Home Screen</Text>
    </View>
  );
}

const Stack = createNativeStackNavigator();

function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={HomeScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

export default App;
```

### 화면전환

- navigation.navigate() 이용

```
onPress={() => navigation.navigate('Details')}
```

- navigation.push() 이용 : 이 경우에는 현재 페이지로 다시 이동을 시도하면 새 화면으로 나온다.

```
 onPress={() => navigation.push('Details')}
```

- 뒤로 이동 : navigation.goBack()
- 최상단으로 이동 navigation.popToTop()
