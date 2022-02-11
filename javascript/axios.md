# Axios

axios는 브라우저, node.js를 위한 Promise API를 활용하는 HTTP 비동기 통신 라이브러리다.

### axios vs fetch

자바스크립트에 기본적으로 존재하는 fetch api와 몇가지 차이점이 있다.

1. 라이브러리 별도 설치가 필요하다.
2. 자동으로 JSON 형태로 변환된다.
3. 요청을 취소할 수 있고 타임아웃을 걸 수 있다.
4. HTTP 요청을 가로챌 수 있다.

이 외에도 여러 차이점이 있으며 종합해보면 axios는 별도의 설치가 필요하다는 단점을 커버할만한 기능 지원을 해준다.

개인적으로는 간단한 기능을 구현할 때는 기본 내장되어있는 fetch를 사용하고 그 외엔 axios를 쓰는게 편리한 것 같다.

### 사용방법

```
npm install axios
```

npm에서 설치 후 자유롭게 사욯하면 된다.

## 요청 메소드 종류

1. axios.get(url[, config])

기본값으로 서버에서 데이터를 가져올 때 사용한다.

ex)

```
axios.get('/test', {
	params: {
		name: 'veneas'
	}
})
.then((response) => {
	console.log(response);
})
.catch((error) => {
	console.log(error);
});
```

2. axios.post(url[, data[, config]])

서버에 데이터를 새로 생성할 때 사용한다.

```
axios.post('/test',
	{
		name: 'venese'
	}
)
.then((response) => {
	console.log(response);
})
.catch((error) => {
	console.log(error);
});
```

3. axios.delete(url,[, config])

서버에 있는 내용을 삭제할 때 사용하기에 두번째 인자를 전달하지 않는다.

4. axios.put(url[, data[, config]])

특정 데이터를 수정할 때 사용한다. 여러번 요청을 해도 새로운 데이터가 지속적으로 추가되지 않고 결과값이 동일한 것이 post와 차이점이다.
