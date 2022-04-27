# AsyncStorage
https://react-native-async-storage.github.io/async-storage/docs/usage/

웹에서 개발할 때 사용자의 정보를 저장해둘 수 있는 local storage 기능이 react native 에서는 AsyncStorage 이다.

현재 리액트 네이티브 팀에서 서비스 제공을 중단했기 때문에 사용을 하려면 라이브러리를 사용해야한당.

1. npm install

```
npm install @react-native-async-storage/async-storage
```

2. import

```
import AsyncStorage from '@react-native-async-storage/async-storage';
```

### 값 저장하기

- string 값 저장하기

```
const storeData = async (value) => {
  try {
    await AsyncStorage.setItem('@storage_Key', value)
  } catch (e) {
    // saving error
  }
}
```

- object 값 저장하기

```
const storeData = async (value) => {
  try {
    const jsonValue = JSON.stringify(value)
    await AsyncStorage.setItem('@storage_Key', jsonValue)
  } catch (e) {
    // saving error
  }
}
```

### 값 불러오기

```
const getData = async () => {
  try {
    const value = await AsyncStorage.getItem('@storage_Key')
    if(value !== null) {
      // value previously stored
    }
  } catch(e) {
    // error reading value
  }
}
```
