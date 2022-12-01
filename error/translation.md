# Google Translation 오류

## ⛔️ 상황

> 크롬 브라우저 자체의 언어 번역 버튼을 누르고 나면 DOM Exception이 뜨면서 페이지가 마비됨.

### **오류코드**

```jsx
DOMException: Failed to execute 'removeChild' on 'Node': The node to be removed is not a child of this node.
```

검색해보니 대부분의 <></> 와 같은 **Fragment를 최상위 컴포넌트에서 사용중이라 나타나는 문제인듯 싶어서**

div 태그로 최상위에 있는 Fragment로 전부 대체 했으나 여전히 에러가 떴다.

**그러다가**

[https://github.com/facebook/react/issues/11538](https://github.com/facebook/react/issues/11538)

이걸 보고 혹시 구글 번역 자체의 문제가 아닐까 하는 의문이 확신이 되었다 . . .

### ⭐️ 정확한 **원인파악**

1. Google Translate이 자체적으로 내가 만든 페이지에 한글이 입력되어있는 부분의 텍스트를 지우고, Translate한 내용을 <font> Tag로 감싸 append 해주면서 생긴 문제.
2. Google에서 번역기능 사용 시 DOMTree 에 있는 한글로 된 TextNode를 지우고 새로 영어로 만들어진 TextNode를 append 하게되면서, React상에서는 더이상 DOMTree에 없는 TextNode에 대한 참조를 계속 유지하고 있기 때문에 페이지 오류가 나게 되는 것.

실제로 Google Translate로 사이트를 번역하면 아래와 같이 DOM이 변경됨.

```
// 번역 전
<div>안녕하세요!</div>

// 번역 후
<div>
	<font style="vertical-align: inherit;">
		<font style="vertical-align: inherit;">Hello!</font>
	</font>
</div>
```

코드 상의 오류가 아닌, 리액트 + 구글 번역 사이의 문제였기 때문에 많은 사람들이 함께 이런 오류를 겪고 있었다.

## 📜 **해결법**

1. Google Translate 막아버리기 (실제로 가장 많이 사용하는 방법)

   but 시도해보니 사이트 처음 접속 시 팝업 + url 옆 번역기능만 숨길 수 있고 홈화면에서 우클릭 시 번역기능은 여전히 사용가능했다.

   단점 : 임시방편의 느낌이 강하게 들었다. (나~중에 영어 말고 다른 언어도 추가될 수 있기에 …)

2. 모든 TextNode들을 직접 div 태그로 감싸기

   이렇게 하면 Google Translate을 통해 내용들이 <font> 태그로 대체되더라도 React에서 참조하는 노드가 그대로 DOM Tree에 남아있기 때문이다.

   단점 : 프로덕트 코드 내의 textnode를 모두 찾아서 전부 추가해줘야함 _(a.k.a 막노동)_

3. Workaround 사용

   리서치 결과 아래 코드(workaround)를 직접 코드에 넣어서 해결한 사람이 있었다.

   단점 : 말 그대로 "Workaround"일 뿐이여서, 문제를 근본적으로 해결하는 건 아니고,

   **오류를 없애고 페이지가 다운되는 것을 막아주는 역할을 하며 사이트의 성능에 문제가 생길 수 있음.**

```jsx
if (typeof Node === "function" && Node.prototype) {
  const originalRemoveChild = Node.prototype.removeChild;
  Node.prototype.removeChild = function (child) {
    if (child.parentNode !== this) {
      if (console) {
        console.error(
          "Cannot remove a child from a different parent",
          child,
          this
        );
      }
      return child;
    }
    return originalRemoveChild.apply(this, arguments);
  };

  const originalInsertBefore = Node.prototype.insertBefore;
  Node.prototype.insertBefore = function (newNode, referenceNode) {
    if (referenceNode && referenceNode.parentNode !== this) {
      if (console) {
        console.error(
          "Cannot insert before a reference node from a different parent",
          referenceNode,
          this
        );
      }
      return newNode;
    }

    return originalInsertBefore.apply(this, arguments);
  };
}
```

## ✔️채택한 해결법 : (2)번

> 해당 파일 내에 태그로 감싸지지 않거나, 잘못된 태그처리가 되어있는 부분을 전부 수정했다.

언젠간 처리해야 할 작업이며, 프로젝트 전체 코드가 아닌 랜딩페이지 관련 컴포넌트들이 문제였기 때문에
랜딩페이지 관련 컴포넌트들을 하나씩 주석 처리해가면서 소거법으로 문제있는 파일을 4개 추리는데 성공했다.

4개 파일이 공통적으로 문제였던 것은, 랜딩페이지에서 사용자에게 보여지는 데이터들이 프론트단에서 하드코딩으로 타이핑 되어있었고,
이조차 감싸지지 않은 문자열 형식으로 되어있었다. (React 15까지는 문제 없었던 것으로 파악완료. .)

## ⭐️ 마무리

- 남 탓 : 결론적으로 프로덕트 코드가 아닌 구글번역이 중간에 태그들을 자체적으로 바꾸는 것이 문제였다.
- 내 탓 : 급하게 언어기능을 추가하는 과정에서 한국어를 기준으로 작성되어있던 로직이나 코드들이 영어로 변환되었을때 발생할 현상을 사전에 파악하지 못해 발생한 문제였다..
- _이 문제에 대해서 Google에 버그리포트 올렸다고 한 사람이 있는데 아직도 해결이 안된걸 보니 앞으로도 계속 해결이 안될 것 같다.(^_^)

### Reference

[_https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild_](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild)

[https://stackoverflow.com/questions/12238396/how-to-disable-google-translate-from-html-in-chrome/12238414#12238414](https://stackoverflow.com/questions/12238396/how-to-disable-google-translate-from-html-in-chrome/12238414#12238414)

[https://stackoverflow.com/questions/70705945/react-failed-to-execute-removechild-on-node](https://stackoverflow.com/questions/70705945/react-failed-to-execute-removechild-on-node)

[https://stackoverflow.com/questions/66631959/react-failed-to-execute-removechild-on-node-the-node-to-be-removed-is-not](https://stackoverflow.com/questions/66631959/react-failed-to-execute-removechild-on-node-the-node-to-be-removed-is-not)

[https://errorsandanswers.com/react-domexception-failed-to-execute-removechild-on-node-the-node-to-be-removed-is-not-a-child-of-this-node/](https://errorsandanswers.com/react-domexception-failed-to-execute-removechild-on-node-the-node-to-be-removed-is-not-a-child-of-this-node/)

[https://www.syncfusion.com/forums/169679/failed-to-execute-removechild-on-node-the-node-to-be-removed-is-not-a-child-of-this-node](https://www.syncfusion.com/forums/169679/failed-to-execute-removechild-on-node-the-node-to-be-removed-is-not-a-child-of-this-node)
