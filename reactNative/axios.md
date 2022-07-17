# React-native에서 axios
기존에 리액트에서 개발했을 때는 서버에 사진을 올리려면 formdata처리를 한 후에 axios나 fetch를 사용하여 서버통신을 했다.

RN으로 프로젝트를 진행하면서 프로필 사진 변경이나 게시글에 사진을 올리는 기능을 구현하고자 똑같이 했는데, 계속해서 "network request failed" 라는 오류가 났다.

1. 오류를 검색해보니 formdata 작업을 수행할 때 uri 부분에 "file://" 을 붙여주면 된다고 해서 붙여줬더니 요청이 정상적으로 처리됐다.

그러나 오류 해결과 동시에 "505 error" 가 뜨면서 서버에 전송된 데이터가 undefined라는 새로운 오류가 생겼고, 문제를 파악해보니 서버 쪽에서 multer을 사용하여 사진을 받아야하는데 데이터 파싱이 제대로 되지 않고 있었다.

2. 이번에도 역시 구글링을 통해서 axios에서 formdata를 넘겨줄 때 transformRequest라는 옵션을 추가해줘야 한다는 것을 알게되었다.

```
transformRequest: (data, headers) => return data;
```

해당 옵션을 코드에 추가해줬더니 에러가 마법 같이 해결되었다!

그러나 merge후에 처음 에러였던 uri 값에 "file://"을 추가하는 방법이 안드로이드 9에서 테스트했던 나에게는 해결법이지만 오히려 안드로이드 10 이상에서는 추가를 안해야 정상적으로 작동한다는 것을 알게되었다.

이 문제는 안드로이드 버전에 따른 문제라는 생각이 들어서 각자 콘솔에 전달받는 uri값을 찍어보니 10이상에서는 자동적으로 uri앞에 "content://" 가 붙은 형식의 값이 전달된다는 것을 알게되었다.

3. 따라서 이 문제는 formdata 처리를 할 때 삼항연산자를 사용하여 전달 받은 uri 값이 이미 "://" 형식으로 되어있는지를 검사하는 코드를 작성하여 해결하였다.

## 최종 코드

```
const uploadImages = async uploadImgs => {
  try {
    const formdata = new FormData();
    await uploadImgs.map(image => {
      formdata.append('multipleImg', {
        uri: image.path.includes(':') ? image.path : 'file://' + image.path,
        type: image.mime,
        name: image.fileName,
      });
    });
    const result = await axios.post(`${BASE_URL}/s3/post-images`, formdata, {
      redirect: 'follow',
      headers: {
        'Content-Type': 'multipart/form-data',
      },
      transformRequest: (data, headers) => {
        return data;
      },
    });
    return result.data;
  } catch (error) {
    console.log(error);
  }
};
```
