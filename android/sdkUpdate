### 안드로이드 API 버전 업데이트

: 2022.11월 기준으로 API 기준 수준이 30에서 31로 올라감에 따라서 스토어에 업로드 하려면 몇가지 코드 수정을 해줘야했다.

- 마주한 에러

```
현재 앱이 30의 API 수준을 타겟팅하고 있지만, 보안 및 성능에 최적화된 최신 API를 기반으로 앱을 빌드하려면 API 수준 31 이상을 타겟팅해야 합니다. 앱의 타겟팅 API 수준을 31 이상으로 변경하세요
```

- 해결방법

1. bundle.gradle 에서 compileSdkVersion 과 defaultConfig의 targetSdkVersion을 31로 변경.

2. AndroidManifest.xml에 activity 마다 `android:exported="true"` 추가.

3. release용으로 빌드 시 버전 에러나는 라이브러리들 최신화, 추가 변경사항 있을 경우 수정.

위 3가지를 해주니 스토어 등록이 문제없이 완료되었다.
