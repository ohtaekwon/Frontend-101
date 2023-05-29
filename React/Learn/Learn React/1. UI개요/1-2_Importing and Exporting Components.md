## Importing and Exporting Components

> 컴포넌트 import 및 export

## 학습 내용

- 루트 컴포넌트란 무엇인지
- 컴포넌트를 import하고 export하는 방법
- default 및 이름 있는 import / export 를 사용해야 하는 경우
- 하나의 파일에서 여러 컴포넌트를 import / export 하는 방법
- 컴포넌트를 여러 파일로 분할하는 방법

## The root component file

> 루트 컴포넌트 파일

[첫 번 째 컴포넌트](https://github.com/ohtaekwon/Frontend-101/blob/main/React/Learn/Learn%20React/1.%20UI%EA%B0%9C%EC%9A%94/1-1_First%20Component.md)에서 만든 `Profile` 컴포넌트와 `Gallery`컴포넌트는 아래와 같이 랜더링이 됩니다.

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

여기서 컴포넌트들은 모두 `App.js`라는 **`root 컴포넌트 파일`**에 존재합니다. **CRA**에서는 앱 전체가 `src/App.jsx`에서 실행됩니다. 설정에 따라 root 컴포넌트가 다른 파일에 위치할 수 있습니다. `Next.js`처럼 `파일 기반``으로 라우팅하는 프레임워크일 경우 페이지별로 root 컴포넌트가 다를 수 있습니다.

## Exporting and importing a component

> 컴포넌트 import(불러오기) 및 export(내보내기) 하기

컴포넌트는 다음 세 단계로 이동할 수 있습니다.

1. 컴포넌트를 넣을 JS파일을 **생성**합니다.
2. 새로 만든 파일에서 함수 컴포넌트를 **export**합니다. (**default** 또는 **named** export 방식을 사용합니다.)
3. 컴포넌트를 사용할 파일에서 **import**합니다. (**default** 또는 **named** export에 대응 하는 방식으로 import합니다.)

여기서 `Profile`과 `Gallery`는 모두 `App.jsx`에서 `Gallery.jsx`라는 새 파일로 이동했습니다. 이제, `App.jsx`를 변경하여 `Gallery.jsx`에서 `Gallery`를 import할 수 있습니다.

```jsx
import Gallery from "./Gallery.js";

export default function App() {
  return <Gallery />;
}
```

## Exporting and importing multiple components from the same file

> 동일한 파일에서 여러 컴포넌트 import 및 export하기

갤러리 대신 하나의 `Profile`만 표시하고 싶다면 어떻게 해야 할까? `Profile`컴포넌트도 export 할 수 있습니다. 하지만, `Gallery.jsx`에는 이미 **default export**가 있으며, **default export** 를 두 개 가질 수는 없습니다. 새 파일을 만들어 **default export**하거나 혹은 `Profile`에서 named export를 추가할 수도 있습니다.

> **한 파일은 default export를 하나만 가질 수 있지만, named export는 여러개 가질 수 있습니다.**

먼저 named export 반식을 사용해서 `Gallery.jsx`에서 `Profile`를 **export**합니다. (default 키워드를 사용하지 않습니다.)

```jsx
export function Profile() {
  // ...
}
```

그 다음엔 **named import** 방식으로 `Gallery.jsx`에서 `Profile`를 `App.jsx` 파일로 import 합니다 (중괄호를 사용합니다):

```jsx
import { Profile } from "./Gallery.jsx";
```

마지막으로 `<Profile />`을 App 컴포넌트에서 **렌더링**합니다:

```jsx
export default function App() {
  return <Profile />;
}
```

이제 `Gallery.jsx`에는 **default** `Gallery` **export**와 named Profile export라는 두 가지의 export가 존재합니다. `App.jsx`에서는 두 컴포넌트를 import 해서 사용합니다. 아래의 예제에서 `<Profile />`과 `<Gallery />`를 교차해서 사용할 수 있습니다.

```jsx
import Gallery from "./Gallery.jsx";
import { Profile } from "./Gallery.jsx";

export default function App() {
  return <Profile />;
}
```

### 이제 default와 named export 방식 둘 다 사용할 수 있게 됐습니다.

#### `Gallery.jsx`

- `Profile` 컴포넌트를 `Profile`로 named export 합니다.
- `Gallery` 컴포넌트를 default export 합니다.

#### `App.jsx`

- `Gallery.jsx`에서 `Profile`를 `Profile`로 named import 합니다.
- `Gallery.jsx`에서 `Gallery`를 default import 합니다.
- root App 컴포넌트를 default export 합니다.
