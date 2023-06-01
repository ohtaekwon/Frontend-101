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

## Rendering Lists

> 목록 랜더링

컴포넌트 목록을 랜더링하려면, `for` 문을 통한 Loop 및 배열 `map()` 메서드와 같은 JavaScript 기능을 사용해야 합니다.

#### e.g. 상품 배열

```js
const products = [
  { title: "Cabbage", id: 1 },
  { title: "Garlic", id: 2 },
  { title: "Apple", id: 3 },
];
```

컴포넌트 내에서 `map()` 함수를 사용하여 상품 배열을 `<li>`항목 배열로 반환합니다.

```jsx
const listItems = products.map((product) => (
  <li key={product.id}>{product.title}</li>
));

return <ul>{listItems}</ul>;
```

> `<li>` 에 `Key` 속성이 있다는 것을 주목해야 합니다.

목록의 각 항목에 대해, 형제 항목 중에서 해당 항목을 **고유하게 식별**하는 문자열 또는 숫자를 전달해야 합니다. 일반적으로 Key의 값은 데이터 베이스 ID와 같은 데이터에서 가져와야 합니다.

- React는 나중에 항목을 삽입,삭제 또는 재정령할 때 어떤 일이 일어났는지 이해하기 위해 Key를 사용하기도 합니다.

```jsx
const products = [
  { title: "Cabbage", isFruit: false, id: 1 },
  { title: "Garlic", isFruit: false, id: 2 },
  { title: "Apple", isFruit: true, id: 3 },
];

export default function ShoppingList() {
  const listItems = products.map((product) => (
    <li
      key={product.id}
      style={{
        color: product.isFruit ? "magenta" : "darkgreen",
      }}
    >
      {product.title}
    </li>
  ));

  return <ul>{listItems}</ul>;
}
```

화면에는 `<li>...</li>`로 감싸진 문자들이 나타내진다.

- `Cabbage`, `Garlic`, `Apple`

## Responding to events

> 이벤트에 응답하기

컴포넌트 내부에 **_이벤트 핸들러_** 함수를 선언하여 이벤트에 응답할 수 있습니다.

```jsx
function MyButton() {
  // 클릭 이벤트 함수
  function handleClick() {
    alert("You clicked me!");
  }

  return <button onClick={handleClick}>Click me</button>;
}
```

- 버튼의 `onClick`에 props로 이벤트 핸들링 함수를 전달하면서, React는 사용자가 버튼을 클릭했을 때, 해당 이벤트 핸들러를 호출합니다.

## Updating the screen

> 화면 업데이트 하기

컴포넌트가 특정 정보를 **기억**하여 표시하기를 원하는 경우가 종종 있습니다. 예를 들어, 버튼이 클릭된 횟수를 하고 싶을 때, 이러할 경우 컴포넌트에서 상태관리를 통해 구현할 수 있습니다.

- 상태관리를 위한 대표 훅 : `useState`

useState를 사용하기 위해서는 인자로 `초깃값`을 설정해주어야 합니다. 필수 값은 아니지만, 필수적으로 초기값을 넣어주는 것을 권장되어집니다.

```jsx
import { useState } from "react";

function MyButton() {
  // 이제 컴포넌트 내부에 state 변수를 선언할 수 있습니다:
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return <button onClick={handleClick}>Clicked {count} times</button>;
}
```

`useState`에 두 가지를 얻을 수 있습니다.

- 현재의 상태인 `count`와 이를 업데이트할 수 있는 함수 `setCount`
- 버튼이 처음 표시 될 때는 `useState()` 에 인자로 초깃값 `0`을 전달을 했기 때문에, `count`가 `0`이 됩니다.
- 이때, 버튼을 클릭할 경우 `이벤트 핸들러`가 호출됩니다.
- 이벤트 핸들러 내부에는 `setCount(count + 1)` 로서, 현재의 state에서 `+1`을 해주고 변경된 상태를 전달합니다.
- 증가된 숫자의 상태가 가상 DOM은 이전에 DOM과 비교했을때, 변경이 되어지면서 리랜더링하게 됩니다.
- 결과적으로, `1`이 출력이 됩니다.

## Using Hooks

> 훅 사용하기

`use`로 시작하는 함수를 **훅(Hook)**이라고 합니다. `useState`는 React에서 제공하는 **빌트인 훅**입니다. 리액트를 설치했을 때, 내장된 훅입니다.

이러한 훅은 기존의 훅을 조합하여 커스텀하여 훅을 작성할 수 있습니다.

훅은 일반 함수보다 더 제한적입니다. 컴포넌트(또는 다른 훅)의 **최상위 레벨**에서만 훅을 호출할 수 있습니다. 조건문이나 반복문에서 `useState`를 사용하고 싶다면, 대신 새로운 컴포넌트를 추출하고, 그 컴포넌트에서 작성해야 합니다.

## What Is Hooks?

> 훅이란 무엇인가?

리액트 Hook은 함수형 컴포넌트에서 **상태(state\*)**와 **생명주기(Life Cycle)**기능을 제공하는 리액트의 기능을 말합니다. Hook은 함수형 컴포넌트에서도 상태 관리와 부작용(Side-Effect)을 처리할 수 있게 해주며, 기존 클래스형 컴포넌트에서 제공되는 기능들을 함수형 컴포넌트에서도 사용할 수 있도록 합니다.

쉽게 말하자면, 마치 요리를 할 때, 사용하는 다양한 도구들과 비슷하다고 볼 수 있습니다. 요리를 하려면 식재료를 잘라내거나 섞는 등의 작업을 해야하고 그 과정에서 다양한 도구들이 필요한데, 이떄 사용하는 것들을 Hook이라 보면 됩니다.

예를 들어서, `useState`의 경우 마치 요리할 떄 사용하는 식재료 자르기 도구라고 가정하면, `useState` Hook은 컴포넌트에 상태를 추가할 수 있는데, 이는 마치 요리에 필요한 재료를 자르고 추가하는 것과 비슷하다고 볼 수 있습니다.

상태를 정의하고, 그 값을 변경하는 함수를 사용하여 원하는 대로 상태를 조작할 수 있도록 합니다.

- React에서 Hook은 `use`라는 접두사를 가지고 있는 함수로, 리액트 빌트인 훅을 사용하거나, 직접 커스텀 Hook을 만들어 사용할 수 있습니다.

- 자주 사용하는 빌트인 훅 : `useState`, `useEffect`

#### useEffect란?

생명주기(Life Cycle)와 관련된 작업을 할 수 있게 해주는 Hook입니다. 컴포넌트가 랜더링 된 후에 실행되는 작업을 처리하기 위한 기능을 제공합니다. 이때, Side Effect가 발생할 수 있습니다.

예를 들어서, 요리 과정에서의 다양한 작업들을 처리하는 도구라고 볼 수 있습니다. 요리를 하다가 팬에 음식물이 끼는 것을 방지하기 위해 팬을 깨끗하게 닦는 작업이 필요할 수 있습니다. 이떄, 요리 후 팬을 깨끗히 닦도록 동작을 수행하도록 명령을 한다면 이것이 useEffect와 비슷하다고 볼 수 있습니다.

## Sharing data between components

> 컴포넌트 간 데이터 공유하기

이전 예제에서는 각각의 `<MyButton/>` 컴포넌트에 독립적인 `count`가 있었고, 각 버튼을 클릭하면 클릭한 버튼의 `count`만 변경이 되었습니다.

하지만, **데이터를 공휴하고 항상 함께 업데이트**하기 위한 컴포넌트가 필요할 수 있습니다. 이떄, 최상위 컴포넌트에서 상태관리를 통해서 구현할 수 있습니다.

```jsx
export default function MyApp() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setCount((prev) => prev + 1);
  };
  return (
    <div>
      <MyButton count={count} onClick={handleClick} />
      <MyButton count={count} onClick={handleClick} />
    </div>
  );
}
```

`<MyButton/>` 컴포넌트에 클릭 이벤트 핸들러와 count의 상태(state)를 자식요소로 전달하면서 최상위 컴포넌트인 `<App/>`에서 상태를 관리할 수 있게 됩니다.

이렇게 될 경우, 버튼 중 하나의 버튼만 클릭해도 각각의 `<MyButton/>`에 같은 상태(state)를 props로 전달하게 됩니다.
