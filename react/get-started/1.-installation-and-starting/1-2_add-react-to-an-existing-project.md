---
description: Add React to an Existing Project
---

# 1.2. 기존 프로젝트에 React 추가하기

### Add React to an Existing Project

> 기존 프로젝트에 React 추가하기

기존 프로젝트에 인터렉션을 추가하고 싶다면, React에서 다시 작성할 필요가 없이 기존 스택에 `React`를 추가하고 `React` 컴포넌트를 랜더링하세요.

### Step 1: Add a root HTML tag

먼저 편집하려는 HTML페이지를 열고, 빈 `<div>`태그를 추가하여 React로 무언가 표시할 지점을 표시합니다. 이 `<div>`에 고유한 `<id>`속성값을 지정합니다.

```html
<div id="root"></div>
```

React 트리가 시작되는 곳이기 때문에 `Root(루트)`라고 부릅니다. 이와 같은 루트 HTML 태그는 `<body>`태그 안의 아무 곳에나 배치할 수 있습니다. React가 그 내용을 React 컴포넌트로 대체할 것이므로 비워두세요.

> 한 페이지에 필요한 만큼의 루트 HTML 태그를 가질 수 있습니다.

### Step 2: Add the script tags

HTML 페이지에서 담는 `</body>` 태그를 바로 밑에 다음 파일에 대한 세 개의 `<script>`태그를 추가합니다.

#### Step 3: Create a React component
