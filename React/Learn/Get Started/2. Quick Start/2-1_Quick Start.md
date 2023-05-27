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

## 참고

React 컴포넌트는 항상 대문자로 시작해야 하지만, 함수명이 대문자일 필요는 없습니다.**그러나 JSX 안에서 컴포넌트가 사용될 때에는 반드시 대문자로 시작해야 합니다.**

#### _함수가소문자로 시작할 경우에도 문제 없이 동작하는 여러가지 기법_

- `default export`의 경우
  - `import` 시에 대문자로 시작하는 새로운 이름을 부여 (ex: `DefaultProfile`)
- `named export`의 경우
  - `import` 시에 `as` 로 대문자로 시작하는 새로운 이름을 부여 (ex: `NamedTwo`)
  - 컴포넌트 **외부**에서 대문자로 시작하는 새로운 변수에 할당 (ex: `NamedThree`)
  - 컴포넌트 내부에서 대문자로 시작하는 새로운 변수에 할당 (ex: `NamedFour`)

```jsx
import DefaultProfile from "./ExportedDefaultProfile";
import {
  NamedExportedProfileOne,
  namedExportProfileTwo as NamedTwo,
  namedExportProfileThree,
} from "./Profiles";

const user = {
  imageUrl: "https://i.imgur.com/yXOvdOSs.jpg",
  imageSize: 90,
};

const NamedThree = namedExportProfileThree;

export default function App() {
  const NamedFour = namedExportProfileThree;
  return (
    <>
      <DefaultProfile user={{ ...user, name: "DefaultProfile" }} />
      <NamedExportedProfileOne user={{ ...user, name: "NamedExported" }} />
      <NamedTwo user={{ ...user, name: "namedExported2" }} />
      <NamedThree user={{ ...user, name: "NamedThree" }} />
      <NamedFour user={{ ...user, name: "NamedFour" }} />
    </>
  );
}
```

> **_주의💡 _**
> 하지만, `vercel`을 통해 빌드한 프로덕션은 배포하는 과정에서 대문자 파일명이 아니었을 경우 에러가 발생하는 경우가 있었다. 물론, `vercel.json`을 통해서 이러한 부분을 컴파일을 지정할 수 있을 수도 있겠지만, 그냥 여러 `대문자`로 시작하는 것이 여러므로 좋다는 판단(?)..

## Writing markup with JSX

> JSX로 마크업 작성하기

위에서 본 마크업 구문을 `JSX`라고 합니다. 선택 사항이지만, 대부분의 React 프로젝트는 편의성을 위해 JSX를 사용합니다.

JSX는 HTML보다 더 엄격합니다. `<br/>` 과 같은 태그를 닫아서 사용해야 합니다. 또한 컴포넌트는 여러 개의 JSX 태그를 반환할 수 없습니다. `div>...</div>` 또는 빈 `<>...</>` 또는 `<Fragment>...</Fragment>`로 감싸야 합니다. Wrapper와 같이 하나의 공유 부모로 감싸야 합니다.

```jsx
function AboutPage() {
  return (
    <>
      <h1>About</h1>
      <p>
        Hello there.
        <br />
        How do you do?
      </p>
    </>
  );
}
```

## Adding styles

> 스타일 추가하기

React에서는 `className`으로 CSS 클래스를 지정해서 사용합니다. HTML `class` 어트리뷰트와 같은 방식으로 작동합니다.

```jsx
<img className="avatar" />
```

그런 다음 별도의 CSS 파이렝 해당 CSS 규칙을 작성합니다.

```css
/* In your CSS */
.avatar {
  border-radius: 50%;
}
```

## Displaying data

> 데이터 표시하기

JSX를 사용하면 JavaScript에 마크업을 넣을 수 있습니다. `중괄호{}`를 사용하면 코드에서 일부 변수를 삽입하여 사용자에게 표시할 수 있습니다.

- JavaScript로 `이스케이프` 할 수 있습니다.

```jsx
return <h1>{user.name}</h1>;
```

JSX 속성에서 JavaScript로 이스케이프할 수도 있지만, 따옴표 대신 `중괄호`를 사용해야 합니다. 예를 들어, `className="avatar"` 문자열을 CSS클래스로 전달하지만, `src={user.imgUrl}`는 JavaScript `user.imgUrl`변수 값을 읽은 다음 해당 값을 `src` 어트리뷰트로 전달합니다.

```jsx
return <img className="avatar" src={user.imageUrl} />;
```

JSX 중괄호 안에 문자열 연결과 같이 더 복잡한 표현식을 넣을 수도 있습니다.

```jsx
const user = {
  name: "Hedy Lamarr",
  imageUrl: "https://i.imgur.com/yXOvdOSs.jpg",
  imageSize: 90,
};

export default function Profile() {
  return (
    <>
      <h1>{user.name}</h1>
      <img
        className="avatar"
        src={user.imageUrl}
        alt={"Photo of " + user.name}
        style={{
          width: user.imageSize,
          height: user.imageSize,
        }}
      />
    </>
  );
}
```

위의 예시에서 `style={{}}`은 JSX 중괄호 안에 있는 일반 `{}`객체입니다. 스타일이 JavaScript 변수에 의존할 때, style속성을 사용할 수 있습니다.

## Conditional rendering

> 조건부 랜더링

React에서는 조건을 작성하기 위한 특별한 문법이 없습니다. 대신 일반 JavaScript코드를 작성할 때 사용하는 것과 동일한 기법을 사용하면 됩니다.

예를 들어, `if`문을 사용하여 조건부로 JSX를 포함할 수 있습니다.

```jsx
let content;
if (isLoggedIn) {
  content = <AdminPanel />;
} else {
  content = <LoginForm />;
}
return (
  <div>
    {content}
  </div>

```

JSX에서 조건문을 사용하기를 원한다면, **조건부 `?` 연산자를 사용할 수 있습니다.**, `if`문은 JSX의 마크업부분의 내부에서 사용할 수 없지만, 이를 위해 조건부 연산자를 사용할 수 있습니다.

```jsx
<div>{isLoggedIn ? <AdminPanel /> : <LoginForm />}</div>
```

`else` 분기가 필요하지 않은 경우 더 짧은 논리 `&&` 구문을 사용할 수도 있습니다:

```jsx
<div>{isLoggedIn && <AdminPanel />}</div>
```

**\*falsy값과 0**

```jsx
import Profile from "./Profile.js";
const user = [
  {
    id: 0,
    name: "Hedy Lamarr",
    imageUrl: "https://i.imgur.com/yXOvdOSs.jpg",
    imageSize: 90,
  },
  {
    id: "Hedy Lamarr1",
    name: "Hedy Lamarr",
    imageUrl: "https://i.imgur.com/yXOvdOSs.jpg",
    imageSize: 90,
  },
];

export default function App() {
  return (
    <>
      {user.map(
        (userInfo) =>
          userInfo.id && <Profile user={userInfo} key={userInfo.id} />
      )}
    </>
  );
}
```

JavaScript에서 0은 falsy 값이므로 아무것도 렌더링이 되지 않아야 합니다. 하지만 위의 예제에서는 0이 렌더링 되어 보여집니다.

JavaScript에서 `&&` 연산자는 앞의 조건이 `falsy`한 값이 라면, 해당 객체를 반환하기 때문에, 0이 반환되어 랜더링이 됩니다.

## 요약

- JSX식에는 반드시 부모 요소가 하나 이상은 있어야 한다.
