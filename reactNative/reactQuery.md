# React Query
react query는 캐싱기능을 제공해주기 때문에 서버의 값을 가져올 때 업데이트나 에러 핸들링 등 비동기 과정을 더욱 편리하게 만들어준다.

프로젝트를 하던 도중 서버 통신을 더욱 효율적으로 하기 위해 고민하다가 아래의 특징들이 매력적이라고 판단되어 사용해봤다.

1. 캐싱기능
2. 무한 스크롤
3. 비동기 과정의 단순화
4. 중복 호출 허용시간 조절 가능
5. 업데이트 된 데이터에 대한 자동 실행

## 사용하기

```
npm install react-query
```

설치 후 프로젝트의 최상단에 추가적인 세팅이 필요하다.

```
// App.js

import {QueryClient, QueryClientProvider} from 'react-query';


const queryClient = new QueryClient();
const App = () => {
  return (
    <SafeAreaProvider style={{flex: 1}}>
      <QueryClientProvider client={queryClient}>
        <StatusBar hidden={true} />
        <Provider store={store}>
          <NavigationContainer>
            <Navigation />
          </NavigationContainer>
        </Provider>
      </QueryClientProvider>
    </SafeAreaProvider>
  );
};
```

세팅 후 서버에 데이터 요청 예시코드

```
const {
    isLoading: totalPostDataLoading,
    data: totalPostDatas,
    refetch,
  } = useQuery('totalPostDatas', async () => {
    const {data} = await axios(`${BASE_URL}/post/total-posts`, {
      params: {
        key: kakaoUid,
      },
    });
    return data;
    },
    {
        onSuccess: data => {
        console.log(data);
        },
        onError: e => {
        console.log(e.message);
        }
    }
  );
```

- isLoading : 데이터를 가져오고 있을 때는 true, 성공/실패 했을시 false 값으로 바뀜
- data : 요청한 데이터
- refetch : react query 자체에서 제공하는 refetch 함수
- onSuccess : 성공 시 수행 할 작업
- onError : 실패 시 수행 할 작업 (401, 404 같은 error가 아니라 정말 api 호출이 실패한 경우만 호출)
