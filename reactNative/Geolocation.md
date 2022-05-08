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
