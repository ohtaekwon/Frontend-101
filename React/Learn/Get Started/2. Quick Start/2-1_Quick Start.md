## 학습 내용

- 컴포넌트를 만들고 중첩하는 방법
- 마크업 및 스타일을 추가하는 방법
- 데이터를 표시하는 방법
- 조건 및 목록을 렌더링하는 방법
- 이벤트에 응답하고 화면을 업데이트하는 방법
- 컴포넌트 간에 데이터를 공유하는 방법

## Creating and nesting components

> 컴포넌트 생성 및 중첩하기

React 앱은 `컴포넌트`들로 만들어집니다. 컴포넌트는 고유한 로직과 모양을 가진 UI(사용자 인터페이스)의 일부입니다. 컴포넌트는 버튼만큼 작을 수도 있고, 페이지만큼 클 수도 있습니다.

> React 컴포넌트는 마크업을 반환하는 JavaScript 함수입니다.

```js
function MyButton() {
  return <button>버튼</button>;
}
```

> `MyButton` 컴포넌트를 선언했으므로, 다른 컴포넌트에 중첩할 수 있습니다.

```js
export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```

> **_주목 💡_** `<MyButton />`가 대문자로 시작하는 것에 주목!!

이것이 React 컴포넌트라는 것을 알 수 있는 방법입니다. React 컴포넌트 이름은 항상 대문자로 시작해야 하고, HTML 태그는 소문자로 시작해야합니다.

```jsx
function MyButton() {
  return <button>I'm a button</button>;
}

export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```
