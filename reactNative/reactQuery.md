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

## Infinite Queries

- infinite scroll을 가능하게 해주는 기능으로 useQuery 대신에 useInfiniteQuery를 사용하면 된다.

- useQuery에서 나온 데이터는 API에서 오는 데이터 그대로 전달하지만, useInfiniteQuery는 "pages" 라는 페이지가 포함된 api 응답을 담은 배열을 반환한다.
- 따라서 데이터에 접근하기 위해서는 map을 사용하여 각 페이지의 결과값들에 접근해야 한다.

- 이러면 데이터들이 [[배열], [배열], [배열]...] 처럼 중첩된 배열 형식으로 저장되므로 flat 메소드를 사용하여 배열안의 모든 값들을 배열 밖으로 꺼내주는 작업을 해야한다.

ex)

```
data.pages.map(page => page.results).flat()

```

- getNextPageParam :
  useInfiniteQuery의 prop으로 다음페이지의 값을 찾을 수 있게 실행되는 함수.
  현재 페이지에 있는 데이터들이 다 보여지고 다음 페이지를 불러와야 할 때 현재 페이지 정보와 전체 페이지 값을 비교하여 데이터들을 불러오도록 구현하면 된다.
  ex)

  ```
  (lastPage) => {
    if(lastPage.page + 1 > lastPage.total_pages) {
      return null
    }
    return lastPage.page + 1
  }
  ```

- page parameter을 갖게되면 react Query 에서는 자동적으로 인식하여 pageParam을 fetcher 함수에 즉시 전달한다.
  ({pageParam} => fetch 함수 ...)로 사용가능.

- getNextPageParam을 통해 다음 페이지를 찾은 후에는 useInfiniteQuery에서 queryhasNextPage(boolean) 와 fetchNextPage(function)을 사용하여 infinity scroll을 구현할 수 있다.
