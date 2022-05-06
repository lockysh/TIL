# Map (지도 기능)
프로젝트 도중에 사용자의 위치를 가져와야 하는 기능이 필요해서 지도를 띄우고 위도, 경도를 가져오는 코드를 짰다.

지도를 띄울 때 사용한 라이브러리 :
https://github.com/react-native-maps/react-native-maps

- 기본코드

```
import MapView from 'react-native-maps';

<MapView
          style={{flex: 1}}
          provider={PROVIDER_GOOGLE}
          initialRegion={{
            latitude: location.latitude,
            longitude: location.longitude,
            latitudeDelta: 0.0922,
            longitudeDelta: 0.0421,
          }}
          <Marker
            coordinate={{
              latitude: location.latitude,
              longitude: location.longitude,
            }}
          />
```

- Marker : 현재위치를 핀으로 나타내게 하기 위함

사용자의 위치가 변했을 때 정보 가져오기

```
          onRegionChange={region => {
            setLocation({
              latitude: region.latitude,
              longitude: region.longitude,
            });
          }}>
```
