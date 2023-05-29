# Your First Component

> 첫 번째 컴포넌트

## 학습 내용

- 컴포넌트가 무엇인지
- React 어플리케이션에서 컴포넌트의 역할
- 첫번째 React 컴포넌트를 작성하는 방법

## Components: UI building blocks

> 컴포넌트 : UI구성 요소

웹에서는 HTML을 통해 <h1>, <li>와 같은 태그를 사용하여 풍부한 구조의 문서를 만들 수 있습니다:

```html
<article>
  <h1>My First Component</h1>
  <ol>
    <li>Components: UI Building Blocks</li>
    <li>Defining a Component</li>
    <li>Using a Component</li>
  </ol>
</article>
```

이 마크업은 아티클을 `<article>`로, 제목은 `<h1>`로, 목차를 정렬된 목록 `<ol>`로 나타냅니다. 이와 같은 마크업은 스타일을 위한 CSS, 상호작용을 위한 JavaScrip와 결합되어 웹에서 볼 수 있는 모든 사이드바, 아바타, 모달 드롭다운 등 모든 UI의 기반이 됩니다.

React를 사용하면 마크업, CSS, JavaScript를 **앱의 재사용 가능한 UI 요소**인 사용자 정의 `컴포넌트`로 결합할 수 있습니다. 위에서 본 마크업 코드는 모든 페이지에 랜더링할 수 있는 `<TableOfContents />` 컴포넌트로 전환될 수 있습니다.

HTML태그와 마찬가지로 컴포넌트를 작성, 순서 지정 및 중첩하여 전체 페이지를 디자인할 수 있습니다. 예를 들어, 읽고 있는 문서 페이지는 React 컴포넌트로 구성되어 있습니다.

```jsx
<PageLayout>
  <NavigationHeader>
    <SearchBar />
    <Link to="/docs">Docs</Link>
  </NavigationHeader>
  <Sidebar />
  <PageContent>
    <TableOfContents />
    <DocumentationText />
  </PageContent>
</PageLayout>
```

프로젝트가 성장함에 따라 이미 작성한 컴포넌트를 재사용하여 많은 디자인을 구성할 수 있으므로 개발 속도가 빨라집니다. `<TableOfContents />`를 사용하여 어떤 화면에서도 추가할 수 있습니다. UI라이브러리와 같은 React 오픈 소스 라이브러리를 사용하여 빠르게 구현할 수 있습니다.

## Defining a component

> 컴포넌트 정의하기

기존에는 웹 페이지를 만들 때 웹 개발자가 콘텐츠를 마크업한 다음 JavaScript를 통해 상호작용을 추가했습니다. 이는 웹에서 상호작용이 중요했던 시절에 효과적이었지만, 이제 많은 사이트와 앱에서 상호작용을 하도록 하고 있습니다. React는 동일한 기술을 사용하면서도 상호작용을 우선시 합니다. **React 컴포넌트는 마크업으로 뿌릴 수 있는 JavaScript함수입니다.**

### 예시) 이미지를 출력하는 `<Profile/>` 컴포넌트

```jsx
export default function Profile() {
  return <img src="https://i.imgur.com/MK3eW3Am.jpg" alt="Katherine Johnson" />;
}
```

## Step 1: Export the component

> 컴포넌트 내보내기

`export default` 접두사는 표준 JavaScript 구문입니다. 이 접두사를 사용하면 나중에 다른 파일에서 가져올 수 있도록 파일에 주요 기능을 표시할 수 있습니다.

## Step 2: Define the function

> 함수 정의하기

함수를 선언문과 표현식으로 정의할 수 있습니다.

```jsx
// 함수 선언문
function Profile(){}
...
// 함수 표현식
const Profile = () => {}
```

`function Profile() { }`을 사용하면 `Profile`이라는 이름의 JavaScRIPT 함수를 정의할 수 있습니다.

## Step 3: Add markup

> 마크업 추가하기

이 컴포넌트는 `src` 및 `alt` 속성을 가진 `<img/>` 태그를 반환합니다. `<img/>`는 HTML처럼 작성되었지만 실제로는 JavaScript입니다. 이 구문을 JSX라고 하며, JavaScript안에 마크업을 삽입할 수 있습니다.

## Using a component

> 컴포넌트 사용학기

`Profile` 컴포넌트를 정희했으므로, 다른 컴포넌트 안에 중첩할 수 있습니다. 예를 들어, 여러 `Profile` 컴포넌트를 사용하는 `Gallery`컴포넌트를 내보낼 수 있습니다

```jsx
function Profile() {
  return <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />;
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```

## What the browser sees

> 브라우저에 표시되는 내용

### 대소문자의 차이에 유희

- `<section>` 은 소문자이므로 React는 HTML 태그를 가리킨다고 이해합니다.
- `<Profile />` 은 대문자 `P` 로 시작하므로 React는 `<Profile/>` 이라는 컴포넌트를 사용하고자 한다고 이해합니다.

그리고 `<Profile />` 은 더 많은 HTML `<img />`가 포함되어 있습니다. 결국 브라우저에 표시되는 내용은 다음과 같습니다.

```html
<section>
  <h1>Amazing scientists</h1>
  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
</section>
```

## Nesting and organizing components

> 컴포넌트 중첩 및 구성

컴포넌트는 일반 `JavaScript`함수이므로 같은 파일에 여러 컴포넌트를 포함할 수 있습니다. 컴포넌트가 상대적으로 작거나 서로 밀접하게 관련되어 있을 때 편리합니다. 이 파일이 복잡해지면 언제든지 `Profile` 을 별도의 파일로 옮길 수 있습니다.

이 방법은 바로 다음 챕터인 컴포넌트 `import` 및 `export` 페이지에서 확인할 수 있습니다.

`Profile` 컴포넌트는 `Gallery`내에 랜더링되기 때문에 `Gallery`는 각 `Profile`의 **자식**으로 랜더링하는 **부모 컴포넌트**라고 할 수 있습니다. 이렇게 컴포넌트를 한 번 정의하면 원하는 곳에서 원하는 만큼 재사용할 수 있습니다.

### Pitfall

> 컴포넌트는 다른 컴포넌트를 랜더링할 수 있지만, **그 정의를 중첩해서는 안됩니다.**

```jsx
export default function Gallery() {
  function Profile() {
    // ...
  }
  // ...
}
```

위의 스니펫은 **매우 느리고 버그를 촉발**할 수 있습니다. 대신 최상위 레벨에서 모든 컴포넌트를 정의해야 합니다.

> **_성능저하의 이유?_**

- 예를 들어서 상위 컴포넌트(`Gallery`)에서 Props가 변경이 될 때마다, 함수 선언문은 `재선언`이 발생하게 되고, 그럴 때마다 `Profile`은 다시 재선언이 발생하게 되고, 선언이 다시 발생할떄마다 그만큼의 성능저하를 가져오기 됩니다.

```jsx
export default function Gallery() {
  // ...
}

// ✅ Declare components at the top level
function Profile() {
  // ...
}
```

- 하지만 바깥에 존재하게 될 경우, `Gallery`이 재선언 된다 해도 `Profile`의 경우 재사용하면 되기 떄문에 성능저하를 줄일 수 있게 된다.
- 따라서, 재선언이 될 수 있는 컴포넌트의 내부 함수같은 경우에는 `useMemo`또는 `useCallback`을 사용하여 이러한 성능상의 이슈를 해결하는 방법을 고안할 수 있습니다.
- 하지만 가급적 밖으로 빼서 사용하는 것을 권장되어집니다.

> 자식 컴포넌트에 부모 컴포넌트의 일부 데이터가 필요한 경우, 정의를 중첩하는 대신 props로 전달하세요.

## Recap

> 요약

### React의 핵심 사항

- React를 사용하면 앱의 **재사용 가능한 UI요소**인 컴포넌트를 만들 수 있습니다.
- React 앱에서 모든 UI는 컴포넌트입니다.
- React 컴포넌트는 다음 몇 가지를 제외하고는 일반적인 JavaScript함수 입니다.
  1. 컴포넌트의 이름은 항상 대문자로 시작합니다.
  2. JSX 마크업을 반환합니다.
