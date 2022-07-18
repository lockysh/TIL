# React Query
https://tanstack.com/query/v4/docs/react-native

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

## Hook : useMutation

변경사항이 생겼을 때 useMutation 훅을 사용하여 실행할 작업을 선언할 수 있다.

```
const mutation = useMutation(newTodo => {
return axios.post('/todos', newTodo)
})
```

mutation의 status 값은 4가지로 나뉜다.

1. isIdle : 변경이 일어날 값들이 idle/ fresh 상태
2. isLoading : 현재 진행 중
3. isError : 에러사항 발생
4. isSuccess : 작업 성공 후 새로운 데이터 값들 사용가능

useMutation에 사용할 수 있는 옵션 값들

```
onMutate: variables => {
    변경사항이 일어나기 직전 실행되는 함수

    // Optionally return a context containing data to use when for example rolling back
    return { id: 1 }
  },
  onError: (error, variables, context) => {
   에러가 발생했을 떄 실행되는 함수

    console.log(`rolling back optimistic update with id ${context.id}`)
  },
  onSuccess: (data, variables, context) => {
    작업 수행이 성공적으로 완료되었을 떄 실행되는 함수
  },
  onSettled: (data, error, variables, context) => {
    작업 수행 후 성공/ 실패 여부와 관계없이 실행되는 함수
  },
```
