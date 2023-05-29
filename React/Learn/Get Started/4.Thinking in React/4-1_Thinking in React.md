## Thinking in React

> React로 사고하기

React는 디자인을 바라보는 방식과 앱을 빌드하는 방식을 바꿀 수 있습니다. React로 사용자 인터페이스를 빌드할 때는 먼저 **컴포넌트**라고 하는 조간으로 분해합니다. 그다음, 각 **컴포넌트**에 대해 서로 다른 시각적 상태를 기술합니다. 마지막으로 컴포넌트를 서로 **연결**해 데이터가 흐르도록 합니다.

## Start with the mockup

> mockup으로 시작하기

이미 JSON API와 디자이너의 목업이 있다고 가정해 보겠습니다. JSON API는 다음과 같은 데이터를 반환합니다:

```json
[
  { "category": "Fruits", "price": "$1", "stocked": true, "name": "Apple" },
  {
    "category": "Fruits",
    "price": "$1",
    "stocked": true,
    "name": "Dragonfruit"
  },
  {
    "category": "Fruits",
    "price": "$2",
    "stocked": false,
    "name": "Passionfruit"
  },
  {
    "category": "Vegetables",
    "price": "$2",
    "stocked": true,
    "name": "Spinach"
  },
  {
    "category": "Vegetables",
    "price": "$4",
    "stocked": false,
    "name": "Pumpkin"
  },
  { "category": "Vegetables", "price": "$1", "stocked": true, "name": "Peas" }
]
```

React에서 UI를 구현하려면 일반적으로 동일한 5단계를 따릅니다.

## Step 1: Break the UI into a component hierarchy

> UI를 컴포넌트 계층 구조로 나누기

먼저 목업(Mockup)의 모든 컴포넌트와 하위 컴포넌트 주위에 상자를 그리고 이름을 지정합니다.
(디자이너와 함께 작업하는 경우 디자이너가 디자인 도구에서 이러한 컴포넌트의 이름을 이미 지정했을 수 있습니다.)

### 배경에 따라 디자인을 여러가지 방식으로 컴포넌트로 분할하는 것을 생각해볼 수 있습니다.

- 프로그래밍(Programming) : 새 함수나 객체를 생성할지 여부를 결정할 때 동일한 기법을 사용합니다. 이러한 기법 중 하나는 **[단일 책임 원칙](https://react-ko.dev/learn/thinking-in-react#step-4-identify-where-your-state-should-live)**입니다. 만약 컴포넌트가 늘어나게 되면 더 작은 하위 컴포넌트로 분해해야 합니다.

- CSS : 클래스 선택자를 만들 때 무엇을 위해 만들 것인지 생각해 보세요. (단, 컴포넌트는 조금 덜 세분화되어 있습니다.)

- 디자인 : 디자인의 레이어를 어떻게 구성할지 고려하세요.

**\*단일 책임 원칙**

> 컴포넌트는 이상적으로 한 가지 일만 수행을 해야한다는 것

JSON이 잘 구조화되어 있으면 UI의 컴포넌트 구조에 자연스럽게 매핑되는 것을 종종 발견할 수 있습니다. 이는 UI와 데이터 모델이 동일한 정보 아키텍처, 즉, 동일한 형태를 가지고 있는 경우가 많기 때문입니다. UI를 컴포넌트로 분리하면 각 컴포넌트가 데이터 모델의 한 부분과 일치합니다.

![컴포넌트 구조](../../../../assets/React-4-1.png)

> 1. `FilterableProductTable` (회색)에는 전체 앱이 포함합니다.
> 2. `SearchBar` (파란색)는 사용자 입력을 수신합니다.
> 3. `ProductTable` (보라색)은 사용자 입력에 따라 목록을 표시하고 필터링합니다.
> 4. `ProductCategoryRow` (녹색)는 각 카테고리에 대한 제목을 표시합니다.
> 5. `ProductRow` (노란색)는 각 상품에 대한 행을 표시합니다.

`ProductTable` (보라색)을 보면 테이블 헤더(`Name` 및 `Price` 레이블 포함)가 자체 컴포넌트가 아님을 알 수 있습니다. 이것은 선호도의 문제이며 어느 쪽이든 사용할 수 있습니다. 이 예제에서는 `ProductTable`의 목록 안에 표시되므로 `ProductTable`의 일부입니다. 그러나 이 헤더가 복잡해지면(예: 정렬을 추가하는 경우) 이를 별도의 `ProductTableHeader` 컴포넌트로 이동할 수 있습니다.

이제 목업에서 컴포넌트를 식별했으므로 **계층 구조**로 정렬합니다. 모겅ㅂ의 다른 컴포넌트 안에 있는 컴포넌트는 **계층 구조**에서 하위로 나타나야 합니다.

- `FilterableProductTable`
  - `SearchBar`
  - `ProductTable`
    - `ProductCategoryRow`
    - `ProductRow`

## Step 2: Build a static version in React

> React로 정적인 UI 만들기

컴포넌트 계층 구조가 완성되었으니, 이제 앱을 구현해야할 차례 입니다. 가장 간단한 접근은 상호작용을 추가하지 않고 데이터 모델에서 UI를 랜더링하는 버전을 만드는 것입니다.! **정적 버전**을 먼저 만든 다음 상호작용을 별도로 추가하는 것이 더 쉬운 경우가 많습니다. 정적 버전을 만드는 데엔 타이핑이 많이 필요하지만 고민은 크게 필요하지 않은 반면, 상호작용을 추가할 때엔 고민을 더 해야 합니다.

데이터 모델을 랜더링하는 앱의 정적 버전을 만들기 위해서는 다른 컴포넌트를 재사용하는 Components를 만들고, **Props**를 사용하여 데이터를 전달해야 합니다.

State의 개념이 익숙하더라도 이 정적 버전을 빌드할 때에는 state를 사용하지 않는 것을 권장합니다. state는 상호작용, 즉 시간이 지남에 따라 변하는 데이터에만 사용됩니다.

**\*Props**

> 부모에서 자식으로 데이터를 전달하는 방식

계층 구조에서 상위 컴포넌트에서 부터 `하향식`으로 만들거나, 하위 컴포넌트부터 `상향식`으로 만들 수 있습니다. 보통 간단한 예시에서는 하향식으로 진행하는 것이 더 쉽고, 대규모 프로젝트에서는 상향식으로 진행하는 것이 더 쉽습니다.

```jsx
function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">{category}</th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? (
    product.name
  ) : (
    <span style={{ color: "red" }}>{product.name}</span>
  );

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category}
        />
      );
    }
    rows.push(<ProductRow product={product} key={product.name} />);
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar() {
  return (
    <form>
      <input type="text" placeholder="Search..." />
      <label>
        <input type="checkbox" /> Only show products in stock
      </label>
    </form>
  );
}

function FilterableProductTable({ products }) {
  return (
    <div>
      <SearchBar />
      <ProductTable products={products} />
    </div>
  );
}

const PRODUCTS = [
  { category: "Fruits", price: "$1", stocked: true, name: "Apple" },
  { category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit" },
  { category: "Fruits", price: "$2", stocked: false, name: "Passionfruit" },
  { category: "Vegetables", price: "$2", stocked: true, name: "Spinach" },
  { category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin" },
  { category: "Vegetables", price: "$1", stocked: true, name: "Peas" },
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}
```

컴포넌트를 만들고 나면 데이터 모델을 랜더링하는 재사용 가능한 컴포넌트 라이브러리 갖게 됩니다. 이 앱은 정적 앱이므로, 컴포넌트 `JSX`만 반환합니다. 계층 구조의 최상단에 있는 컴포넌트(`FilterableProductTable`)는 데이터 모델을 **Props**로 사용합니다.

> 데이터가 최상위 컴포넌트에서 트리 하단에 있는 컴포넌트로 흘러내리기 때문에 이를 **단방향 데이터 바인딩**이라고 합니다.

## Step 3: Find the minimal but complete representation of UI state

> 최소한의 완전한 UI state 찾기

UI를 상호작용하게 만들려면 사용자가 기반이 되는 데이터 모델을 변경할 수 있도록 해야 합니다. 이를 위해 `state`를 사용합니다.

**state**를 앱이 기억해야 하는 최소한의 변화하는 데이터 집합으로 생각합니다. state를 구조화할 때 가장 중요한 원칙은 **직접 반족하지 않기**를 유지하는 것입니다.

## Step 4: Identify where your state should live

> 최소한의 완전한 UI state 찾기

앱에서 최소한으로 필요한 state 데이터를 식별한 후에는, 이 state를 변경하는 데 책임이 있는 컴포넌트, 즉, state를 **`소유`**하는 컴포넌트를 식별해야 합니다.

React는 **계층 구조**를 따라 부모 컴포넌트에서 자식 컴포넌트로, 아래로 내려가는 단방향 데이터 흐름을 따릅니다. 당장은 어떤 컴포넌트가 state를 가져가야 하는지 명확하지 않을 수 있습니다.

### 애플리케이션의 각 상태(State)에 대해

1. 해당 state를 기반으로 렌더링하는 모든 컴포넌트를 찾기
2. 가장 가까운 공통 상위 컴포넌트, 즉, 계층상 그 state의 영향을 받는 모든 컴포넌트들의 위에 있는 부모 컴포넌트를 찾기
3. state가 어디에 위치할지 결정하기
4. 대게 공통 부모에 state를 그대로 둘 수 있습니다.
5. 혹은 공통 부모보다 더 상위 컴포넌트 state에 둘 수 있습니다.
6. 하지만, 뎁스(deps)가 깊어질 경우 props drilling의 문제를 야기할 수 있습니다.
7. state를 소유할 절절한 컴포넌트를 찾지 못했다면, state를 소유하는 새 컴포넌트를 만들어 **공통 부모 컴포넌트**보다 상위에 추가합니다.

### 위의 state에 대한 전략을 적용해보기

1. **state를 사용하는 컴포넌트들 식별하기 :**

- `ProductTable`은 해당 state(검색어 및 체크박스 값)를 기반으로 제품 목록을 필터링 해야 합니다.
- `SearchBar`는 해당 state(검색어 및 체크박스 값)를 표시해야 합니다.

2. **공통 부모 찾기 :** 두 컴포넌트가 공유하는 첫 번째 부모 컴포넌트는 `FilterableProductTable` 컴포넌트 입니다.
3. **state를 어디에 둘 지 결정하기 :** `FilterableProductTable`에 filter text와 checked state값을 유지합니다.

이제 state 값은 `FilterableProductTable`에 있습니다.

```jsx
function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

```

그런 다음 `filterText`와 `inStockOnly`를 `ProductTable`과 `SearchBar`에 props로 전달합니다.

```jsx
<div>
  <SearchBar filterText={filterText} inStockOnly={inStockOnly} />
  <ProductTable
    products={products}
    filterText={filterText}
    inStockOnly={inStockOnly}
  />
</div>
```

하지만, 타이핑과 같은 사용자 액션에 응답하는 코드를 추가하지 않았습니다. 이것을 설정하는 것이 마지막 단계 입니다.

## Step 5: Add inverse data flow

> 역방향 데이터 흐름 추가하기

현재 앱은 props와 state가 계층 구조 아래로 흐르면서 올바르게 랜더링됩니다. 하지만, 사용자 입력에 따라 state를 변경하려면 계층 구조상 깊은 곳에 있는 폼 컴포넌트가 높은 곳에 있는 `FilterableProductTable`의 state를 업데이트해야 하므로, 역방향으로도 데이터가 흐를 수 있게 해야 합니다.

React의 데이터 흐름은 명쾌하지만, 양방향 데이터 바인딩보다는 더 많은 타이핑이 필요합니다. `<input value={filterText} />`를 작성함으로써 `input`의 `value` 프로퍼티가 항상 `FilterableProductTable`에서 전달된 `filterText` state와 같도록 했기 때문입니다. `filterText` state가 절대 변경되지 않으므로 검색어 역시 변하지 않게 됩니다.

사용자가 form입력을 변경할 떄마다 변경 사항을 반영하도록 state도 업데이트를 해야 합니다. 이 state는 `FilterableProductTable`이 가지고 있으므로 이 컴포넌트만이 `setFilterText` 및 `setInStockOnly`를 호출할 수 있습니다.

따라서, 하위에 있는 `SearchBar`가 상위에 있는 `FilterableProductTable`의 state를 대신 업데이트할 수 있도록 하려면, 이 함수들을 `SearchBar`에 전달해야 합니다

```jsx
function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar
        filterText={filterText}
        inStockOnly={inStockOnly}
        // set함수를 전달해줍니다.
        onFilterTextChange={setFilterText}
        onInStockOnlyChange={setInStockOnly} />

```

## 완성

```jsx
import { useState } from "react";

function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState("");
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar
        filterText={filterText}
        inStockOnly={inStockOnly}
        onFilterTextChange={setFilterText}
        onInStockOnlyChange={setInStockOnly}
      />
      <ProductTable
        products={products}
        filterText={filterText}
        inStockOnly={inStockOnly}
      />
    </div>
  );
}

function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">{category}</th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? (
    product.name
  ) : (
    <span style={{ color: "red" }}>{product.name}</span>
  );

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products, filterText, inStockOnly }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (product.name.toLowerCase().indexOf(filterText.toLowerCase()) === -1) {
      return;
    }
    if (inStockOnly && !product.stocked) {
      return;
    }
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category}
        />
      );
    }
    rows.push(<ProductRow product={product} key={product.name} />);
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar({
  filterText,
  inStockOnly,
  onFilterTextChange,
  onInStockOnlyChange,
}) {
  return (
    <form>
      <input
        type="text"
        value={filterText}
        placeholder="Search..."
        onChange={(e) => onFilterTextChange(e.target.value)}
      />
      <label>
        <input
          type="checkbox"
          checked={inStockOnly}
          onChange={(e) => onInStockOnlyChange(e.target.checked)}
        />{" "}
        Only show products in stock
      </label>
    </form>
  );
}

const PRODUCTS = [
  { category: "Fruits", price: "$1", stocked: true, name: "Apple" },
  { category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit" },
  { category: "Fruits", price: "$2", stocked: false, name: "Passionfruit" },
  { category: "Vegetables", price: "$2", stocked: true, name: "Spinach" },
  { category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin" },
  { category: "Vegetables", price: "$1", stocked: true, name: "Peas" },
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}
```
