---
description: Writing Markup with JSX
---

# 3⃣ 1.3. JSX로 마크업 작성하기

JSX는 JavaScript를 확장한 문법으로, JavaScript파일 안에 HTML과 유사한 마크업을 작성할 수 있도록 해줍니다. 컴포넌트를 작성하는 다른 방법도 있지만, 대부분의 React개발자는 JSX의 간결함을 선호하여 코드베이스에서 JSX를 사용합니다.

## 학습 내용

* React가 마크업과 렌더링 로직을 같이 사용하는 이유
* JSX와 HTML의 차이점
* JSX로 정보를 보여주는 방법

## JSX: Putting markup into JavaScript

> JSX: JavaScript에 마크업 넣기

**웹은 HTML, CSS, JavaScript를 기반**으로 만들어져 있습니다. 수 년 동안 웹 개발자들은 HTML로 컨텐츠를, CSS로 디자인을, 로직은 JavaScript로 작성해왔습니다. 보통은 각각 분리된 파일로 관리를 합니다. 페이지의 로직인 JavaScript안에서 분리되어 동작하는 동안, HTML안에서는 컨텐츠가 마크업 되었습니다.

```jsx
// HTML
<div>
  <p></p>
  <form></form>
</div>

// JavaScript
isLoggedIn(){}
onClick(){}
onSubmit(){}
```

하지만 웹이 더욱 인터랙티브해지면서 로직이 컨텐츠를 결정하는 경우가 많아졌습니다. 그래서 JavaScript가 HTML을 담당하게 되었습니다. **이것이 바로 React에서 랜더링 로직과 마크업이 같은 위치의 컴포넌트에 함께 있는 이유입니다.**

랜더링 로직과 마크업이 함께 존재한다면 모든 편집에서 서로 동기화 상태를 유지할 수 있습니다. 반대로 서로 관련이 없는 마크업들은 서로 분리하여 각각 개별적으로 변경하는 것이 더 안전합니다.

각 React컴포넌트는 JSX라는 구문 확장자를 사용하여 해당되는 마크업을 표현합니다. JSX는 HTML과 비슷해보이지만 조금 더 **엄격**하며 **동적**으로 정보를 표시할 수 있습니다. JSX를 이해하는 가장 좋은 방법은 일부의 HTML마크업을 JSX마크업으로 변환해보는 것입니다.

> **\_📌 Note \_** JSX와 React는 서로 다른 별개의 개념입니다. 종종 함게 사용되기도 하지만, 독립적으로 사용할 수 도 있습니다. JSX는 **구문 확장**이고, React는 JavaScript라이브러리입니다.

## Converting HTML to JSX

> HTML을 JSX로 변환하기

```html
<h1>Hedy Lamarr's Todos</h1>
<img src="https://i.imgur.com/yXOvdOSs.jpg" alt="Hedy Lamarr" class="photo" />
<ul>
  <li>Invent new traffic lights</li>
  <li>Rehearse a movie scene</li>
  <li>Improve the spectrum technology</li>
</ul>
```

다음의 HTML을 컴포넌트로 만들어 보면,

```jsx
export default function TodoList() {
  return (
    // This doesn't quite work!
    <h1>Hedy Lamarr's Todos</h1>
    <img
      src="https://i.imgur.com/yXOvdOSs.jpg"
      alt="Hedy Lamarr"
      class="photo"
    >
    <ul>
      <li>Invent new traffic lights
      <li>Rehearse a movie scene
      <li>Improve the spectrum technology
    </ul>
  );
}

```

하지만 에러가 발생할 것입니다. 왜냐하면 JSX는 HTML보다 더 **엄격**하며 몇 가지 규칙이 더 있기 때문입니다.

## The Rules of JSX

> JSX 규칙

### 1. Return a single root element

> 단일 루트 엘리먼트를 반환하세요.

컴포넌트에서 여러 엘리먼트를 반환하려면, **하나의 부모 태그로 감싸주어야 합니다.** 예를 들면 `<>...</>` 또는 `<div>...</div>`를 사용할 수 있습니다.

```jsx
<>
  <h1>Hedy Lamarr's Todos</h1>
  <img
    src="https://i.imgur.com/yXOvdOSs.jpg"
    alt="Hedy Lamarr"
    class="photo"
  >
  <ul>
    ...
  </ul>
</>
```

> **\_📌 Note \_** `<></>` 빈 태그란? 이러한 빈 태그를 `Fragment`라고 합니다. Fragment는 브라우저상 HTML 트리 구조에서 흔적을 남기지 않고 그룹화해줍니다.

### Why do multiple JSX tags need to be wrapped?

> 왜? 여러 JSX태그를 하나로 감싸주어야 할까?

JSX는 HTML처럼 보이지만 **내부적으로는 JavaScript객체를 반환**합니다. 하나의 배열로 감싸지 않은 하나의 함수에서는 두 개의 객체를 반환할 수 없습니다. 따라서, 다른 태그나 Fragment로 감싸지 않으면 두 개의 JSX태그를 반환할 수 없습ㄴ디ㅏ.

### 2. Close all the tags

> 모든 태그를 닫으세요

JSX에서는 태그를 명시적으로 닫아야 합니다. `<img>`태그처럼 자체적으로 닫는 태그도 반드시 `<img />`로 작성해야하며, `<li>oranges`와 같은 래핑 태그 역시 `<li>oranges</li>`형태로 작성해야 합니다.

### 3. camelCase ~~all~~ most of the things!

> ~~거의~~ 대부분이 카멜 케이스입니다.

JSX는 JavaScript로 바뀌고 JSX로 작성된 어트리뷰는 JavaScript 객체의 키가 됩니다. 종종 컴포넌트 안에서 어트리뷰트를 변수로 읽고 싶은 경우가 있을 것ㅇ비니다. 하지만, JavaScript에는 변수명에 제한이 있습니다. 예를 들어, 변수명에는 대시를 포함하거나 `class`처럼 예약어를 사용할 수 없습니다.

이것이 React에서 많은 HTML과 SVG어트리뷰트가 `캐멀 케이스`로 작성된 이유입니다. 예를 들어, `stroke-width` 대신 `strokeWidth`을 사용합니다. `class`는 예약어이므로, React에서는 대신 해당 DOM 속성의 이름을 따서 `className`을 씁니다:

## Pro-tip: Use a JSX Converter

> 전문가 팁: JSX 변환기 사용

기존 마크업에서 모든 어트리뷰트를 변환하는 것은 지루할 수 있습니다. 변환기를 사용하여 기존 HTML과 SVG를 JSX로 변환하는 것을 추천합니다. 변환기는 매우 유용하지만 그래도 JSX를 편안하게 작성할 수 있도록 어트리뷰트를 어떻게 쓰는지 이해하는 것도 중요합니다.

## 최종 결과

```jsx
export default function TodoList() {
  return (
    <>
      <h1>Hedy Lamarr's Todos</h1>
      <img
        src="https://i.imgur.com/yXOvdOSs.jpg"
        alt="Hedy Lamarr"
        className="photo"
      />
      <ul>
        <li>Invent new traffic lights</li>
        <li>Rehearse a movie scene</li>
        <li>Improve the spectrum technology</li>
      </ul>
    </>
  );
}
```

## Recap

> 요약

JSX가 존재하는 이유와 컴포넌트에서 JSX를 쓰는 방법

* React 컴포넌트는 서로 관련이 있는 마크업과 렌더링 로직을 함께 그룹화합니다.
* JSX는 HTML과 비슷하지만 몇 가지 차이점이 있습니다. 필요한 경우 변환기를 사용할 수 있습니다.
* 오류 메세지는 종종 마크업을 수정할 수 있도록 올바른 방향을 알려줍니다.
