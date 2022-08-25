### next/router 사용

pages 폴더 안에 컴포넌트를 생성하면 자동으로 경로가 설정된다.

(\* 경로명은 export되는 컴포넌트 이름이 아닌 파일명을 기준)

1. 정적 라우팅 : 사전에 지정된 주소로 이동

Link 컴포넌트를 사용해 주소를 이동 → react-router-dom 과 유사함

(SPA처럼, 클라이언트 사이드 라우팅으로 페이지 이동이 가능.)

```jsx
import Link from "next/Link";
...
return (
    <div>
      <h2>Link to 'tomato' Page</h2>
      <Link href="/tomato">
        <a>move to tomato</a>
      </Link>
    </div>
  );
```

Link 컴포넌트는 next/Link 모듈에서 불러오며 **href** 속성으로 이동할 경로를 지정한다.

다만 임의의 컴포넌트를 감쌀 시에는 라우팅 X. <a>로 감싸는게 젤 좋은듯

브라우저의 **History API**를 지원하여 뒤로가기를 하더라도 이전에 렌더링한 페이지를 불러온다.

1. 동적 라우팅

하나의 동적 경로에는 한 개의 동적 페이지만이 존재 가능함.

대괄호 [ ] 로 파일명을 감싸면 해당 페이지는 동적으로 경로가 지정되는 페이지가 됨.

```jsx
//동적 페이지가 존재하는 경로에서 대입한 주소를 쿼리명으로 갖는 페이지로 이동가능.
<div>
  <h2>Link to 'potato' Page</h2>
  <Link href="/vegetable/potato">
    <a>move to /vegetable/potato</a>
  </Link>
</div>
```

1. 라우터 객체 : 함수 내에서 라우팅을 수행하기 위해서는 라우터 객체를 활용.

next/router 모듈에서 **`useRouter`** 훅을 불러와서 사용.

<종류>

- **router.back()** : 직전 페이지로 이동
- **router.push("url")** : 지정한 경로로 이동 & 히스토리 스택에 URL 추가.
- **router.replace("url")** : 지정한 경로로 이동 & 히스토리 스택에 URL를 추가X.

그러나 SEO에 영향을 미치는 크롤러는 router.push() 가 다른 페이지로 이동하는 링크라고 인식X.

따라서 Link 컴포넌트를 활용해 시멘틱한 구조를 유지하는 것이 권장됨.
