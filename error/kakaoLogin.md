# Kakao Login Error

> 사용중인 카카오 라이브러리 : https://github.com/react-native-seoul/react-native-kakao-login

## ⚠️ 에러 발생 & 파악

- 반환받았던 error response

```
{"detail":"User not found", "code":"user_not_found"}
```

CodeFlow

1. 로그인 할 계정 / 비밀번호 입력
2. 라이브러리를 통해 카카오에서 auth code 반환
3. 반환받은 auth code를 payload를 통해 서버에 전달
4. 서버에서 인증코드 처리 작업 후 response로 access & refresh code, 로그인 한 유저의 정보값들을 반환

> AOS에서 kakao login이 안된다는 VOC 접수 후 코드를 확인해봤을때, 2번 auth code를 잘 받환받아서 3에서 백 서버에 전달까지 잘되는 상태였고, 4번에서 response 값으로 user not fount error을 전달받고 있었다.

> 따라서 처음에는 백에서 auth code 처리 과정에 문제가 있는것으로 인식하였으나 해당 에러 메세지가 백 코드에서 검색이 되지 않고, 에러로 빠지는 상황이 정확하게 정해져있지 않은 상태였다. 라이브러리 문제인가 싶어서 버전을 올려주었지만, 에러는 여전히 발생.

> 그러다가 에뮬레이터를 돌리다가 debug용으로 빌드하면 정상작동하고, release용으로 빌드하면 에러가 발생하고 있는것을 알게되었고 해당 현상이 재현되었을때 android studio 의 logcat 을 통해 앱이 crash 나고있는지 확인해보니 로그가 하나 찍히고 있는 상태였다.

<해당 에러로그>

```jsx
Process: kr.co.test, PID: 4851

    java.lang.RuntimeException: Unable to create application kr.co.test.utils.GlobalApplication: java.lang.NullPointerException: Argument 'cacheName' cannot be null

        at android.app.ActivityThread.handleBindApplication(ActivityThread.java:7540)

        at android.app.ActivityThread.access$1500(ActivityThread.java:301)

        at android.app.ActivityThread$H.handleMessage(ActivityThread.java:2158)

        at android.os.Handler.dispatchMessage(Handler.java:106)

        at android.os.Looper.loop(Looper.java:246)

        at android.app.ActivityThread.main(ActivityThread.java:8595)

        at java.lang.reflect.Method.invoke(Native Method)

        at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:602)

        at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1130)

     Caused by: java.lang.NullPointerException: Argument 'cacheName' cannot be null

        at com.kakao.util.helper.Utility.notNull(Utility.java:97)

        at com.kakao.util.helper.SharedPreferencesCache.<init>(SharedPreferencesCache.java:82)

        at com.kakao.auth.Session.<init>(Session.java:145)

        at com.kakao.auth.Session.initialize(Session.java:101)

        at com.kakao.auth.KakaoSDK.init(KakaoSDK.java:101)

        at kr.co.test.utils.GlobalApplication.onCreate(GlobalApplication.java:30)

        at android.app.Instrumentation.callApplicationOnCreate(Instrumentation.java:1192)
```

검색해보니 키 해시값들이 제대로 등록이 되어있지 않아서 발생하는 에러였고 kakao developer 페이지를 확인해보니 키 debug는 다 등록되어 있는데 release 키 값들은 제대로 등록이 되어있지 않았다.

## 🧩 해결 방법 : key hash 등록

_참고문서 : [https://developers.kakao.com/docs/latest/ko/getting-started/](https://developers.kakao.com/docs/latest/ko/getting-started/sdk-android#add-key-hash-using-keytool)_

키 해시는 **디버그 키 해시(Debug key hash)와 릴리즈 키 해시(Release key hash)** 두 가지 존재

- 디버그 키 해시: 프로젝트를 처음 생성하거나 디버그할 때, 안드로이드 스튜디오에서 개발 환경에 맞게 자동으로 생성되는 [디버그 인증서](https://developer.android.com/studio/publish/app-signing#debug-mode)에서 해시(hash)한 값
- 릴리즈 키 해시: 앱 스토어에 앱을 배포하기 위해 생성한 릴리즈 인증서로부터 해시한 값

### 1. project terminal에서 키 값 추출

- Debug key hash

```
keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -storepass android -keypass android | openssl sha1 -binary | openssl base64
```

- Release key hash

```
keytool -exportcert -alias pikurate -keystore <RELEASE_KEY_PATH> | openssl sha1 -binary | openssl base64
```

### 2. Google play console에서 키 값 추출

SHA-1 인증서 지문(SHA-1 certificate fingerprint)을 Base64로 인코딩하여 사용

구글 플레이 스토어 콘솔에 접속 ⇒ Setup ⇒ App integrity ⇒ App Signing에 들어가면 SHA -1 값 확인가능

- Debug / Release 동일

```jsx
// PRINTCERT === SHA-1 값
echo "${PRINTCERT}" | xxd -r -p | openssl base64
```

\*\* App signing / Upload key certificate 둘 다 추가 해줘야함.

_참고 : [https://support.google.com/googleplay/android-developer/answer/9842756?hl=ko#upgrade_enroll&zippy=](https://support.google.com/googleplay/android-developer/answer/9842756?hl=ko#upgrade_enroll&zippy=)_

### **생성한 키 해시 값들을 [내 애플리케이션] > [플랫폼] > [Android]에 모두 등록**
