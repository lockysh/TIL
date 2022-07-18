# Geolocation
사용한 라이브러리 :
https://github.com/react-native-geolocation/react-native-geolocation

위도/ 경도 불러오는 코드

```
import Geolocation from '@react-native-community/geolocation';

 Geolocation.getCurrentPosition(
        position => {
          const {latitude, longitude} = position.coords;
          setLocation({
            latitude,
            longitude,
          });
        },
        error => {
          console.log(error.message);
        },
        {enableHighAccuracy: true, timeout: 15000},
      );

```

코드 작성 후 테스트 하는데 위치에 대한 권한 허용이 안됐다는 에러메세지가 계속 떴다..

<해결책>

https://reactnative.dev/docs/permissionsandroid

작업을 수행하기 전에 권한 허용이 되어있는지 판단하는 전처리 작업이 필요함( PermissionsAndroid 사용)

```
import {PermissionsAndroid} from 'react-native';


const granted = await PermissionsAndroid.request(
      PermissionsAndroid.PERMISSIONS.ACCESS_FINE_LOCATION,
    );
    if (granted === PermissionsAndroid.RESULTS.GRANTED) {
      console.log('권한 얻기 성공');
      //위도 & 경도 불러오는 함수
          } else {
      console.log('권한얻기 실패 :', granted);
    }
  };
```

PermissionsAndroid.RESULTS의 값은 3가지로 나뉜다.

1. GRANTED: 'granted'
2. DENIED: 'denied'
3. NEVER_ASK_AGAIN: 'never_ask_again'

따라서 현재 위치에 대한 권한을 허용했는지를 판단하고 해당 값이 **"granted"** 라면 지정된 작업을 시행하도록 코드 수정
