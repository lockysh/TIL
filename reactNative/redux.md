# Redux
redux는 상태관리 라이브러리로 하나의 스토어(store)안에 있는 객체 트리에 앱의 state가 저장된다. 개발하다보니 컴포넌트 간의 데이터 전달이 점점 복잡해지는 경우가 많이 생기면서 props를 통한 방식의 한계를 느꼈고, 그에 대한 대책으로 edux를 사용하기 시작했다.

### 사용법

1. install

```
npm install redux react-redux
npm install reduxjs/toolkit
```

2. store.js 생성

```
import {configureStore} from '@reduxjs/toolkit';
import rootReducer from './reducers/rootReducer';

const store = configureStore({reducer: rootReducer});

export default store;

```

3. 최상단에 정의해주기

```
//App.js

import {Provider} from 'react-redux';
import store from './src/store';

 <Provider store={store}>
          <NavigationContainer>
            <Navigation />
          </NavigationContainer>
        </Provider>
```

4. action type 정의해주기

```
const types = {
    SAVE_KAKAO_UID: 'SAVE_KAKAO_UID',
...
}

exports.saveKakaoUidAction = parameter => {
  return {
    type: types.SAVE_KAKAO_UID,
    payload: parameter,
  };
};
```

5. rootReducer/ 개별 reducer 정의해주기

```
// root Reducer

const rootReducer = combineReducers({
  kakaoUid: kakaoUidReducer,
  ...
});
```

```
// kakaoUid reducer

const initialState = {
  kakaoUid: null,
};

const kakaoUidReducer = (state = initialState, action) => {
  switch (action.type) {
    case types.SAVE_KAKAO_UID:
      return {
        ...state,
        kakaoUid: action.payload,
      };
    default:
      return state;
  }
};
```

6. 사용하기

- 값 저장하기

```
import {useDispatch} from 'react-redux';
import actions from '../../actions/index';

const function() => {
    const dispatch = useDispatch();

dispatch(actions.saveKakaoUidAction("저장할 값"));
}
```

- 저장한 값 사용

```
import {useSelector} from 'react-redux';
const function() => {
  // kakaoUid 라는 값으로 컴포넌트 안에서 사용
  const {kakaoUid} = useSelector(state => state.kakaoUid);
}

```
