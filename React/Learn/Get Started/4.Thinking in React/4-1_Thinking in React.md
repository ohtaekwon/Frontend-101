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

## Step 2: Build a static version in React

> React로 정적인 UI 만들기

## Step 3: Find the minimal but complete representation of UI state

> 최소한의 완전한 UI state 찾기

## Step 4: Identify where your state should live

> 최소한의 완전한 UI state 찾기

## Step 5: Add inverse data flow

> 역방향 데이터 흐름 추가하기
