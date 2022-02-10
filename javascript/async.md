# Async

기존의 비동기 처리 방식인 콜백함수와 Promise의 단점을 보완한 문법이다.

```
async function test(){
	return 100;
}
```

async를 붙이면 해당 함수는 항상 Promise를 반환한다. Promise가 아닌 값은 Promise로 감싸서 반환한다.

## await

await은 async 함수 안에서만 동작하며 Promise가 처리될 때까지 기다렸다가 값을 반환한다.

```
async function test(){
	const promise = new Promise((resolve,reject)=>{
    	setTimeout(()=>resolve('호출완료!'),1000)
    });
  	const result = await promise;
  	alert(result);
}

test()
```

함수를 호출하고 실행되는 도중 <result>함수가 중단되었다가 Promise가 처리되면 객채의 결과 값이 할당되며 실행이 재개된다.

### 에러 핸들링

await가 던진 에러는 try..catch를 사용해 잡을 수 있다.

```
async function test(){
  try{
    const response = await fetch('url')
    const user = await response.json()
  }
  catch(error)
}

test();
```

혹은

```
async function test(){
	const response = await fetch('url')
}
//foo()는 거부 상태의 Promise가 된다.
tset.catch(alert);
```
