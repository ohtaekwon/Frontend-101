# 1장 타입스크립트 알아보기

## 아이템 3 : 코드 생성과 타입이 관계 없음을 이해하기

큰 그림에서 보면, 타입스크립트 컴파일러는 두 가지 역할을 수행합니다.

1. 최신 타입스크립트/자바스크립트를 브라우저에서 동작할 수 있도록 구버전의 자바스크립트로 `트랜스파일(transpile)`을 합니다.
2. 코드의 타입 오류를 체크합니다.

위의 두 가지 서로 독립적입니다. 즉, 타입스크립트가 자바스크립트로 변환될 때, 코드 내의 타입에는 영향을 주지 않습니다. 또한, 자바스크립트의 실행 시점에도 타입은 영향을 미치지 않습니다.

### 1.3.1. 타입 오류가 있는 코드도 컴파일이 가능합니다.

컴파일은 `타입 테크`와 독립적으로 동작하기 때문에, `타입 오류`가 있는 코드도 컴파일이 가능합니다.

```ts
// test.ts
let x;
x = 1234;
```

```shell

tsc test.ts

```

- `test.ts:2:1 - error TS232: '12234' 형식은 'string'에 할당할 수 없습니다.`

> **Key Point💡**
>
> 타입스크립트는 C나 자바의 경고(warning)과 유사합니다. 문제가 될 만한 부분을 잡아주지만, 그렇다고 `빌드`를 멈추지 않습니다.

타입 오류가 있음에도 컴파일이 된다는 것은 엉성해 보일 수 있으나 실제 도움이 됩니다. 예를 들어 웹 애플리케이션을 만들면서 어떤 문제가 발생했을 경우, 타입스크립트는 여전히 컴파일된 산출물을 생성하기 때문에, 문제가 된 오류를 수정하지 않더라도, 애플리케이션의 다른 부분을 테스트할 수 있게됩니다.

만약 오류가 있을 떄, 컴파일하지 않으려면 `tsconfig.json`에 `noEmitOnError`를 설정하거나 빌드 도구에 동일하게 적용됩니다.

### 1.3.2. 런타임에는 타입 체크가 불가능합니다.

```ts
interface Square {
  width: number;
}
interface Rectangle extends Square {
  height: number;
}

type Shape = Square | Rectangle;

function calculateArea(shape: Shape) {
  if (shape instanceof Rectangle) {
    // Rectangle 에러 'Rectangle' only refers to a type, but is being used as a value here.ts(2693)
    // 직역하자면, Rectangle은(는) 형식만 참조하지만, 여기서는 값으로 사용되고 있습니다.

    return shape.width * shape.height;
    // height 에러, Property 'height' does not exist on type 'Shape'.
    // 직역하자면, Shape 형식에 height 속성이 없습니다.
  } else {
    return shape.width * shape.width;
  }
}
```

`instanceof` 체크는 런타임에 일어나지만, Rectangle은 타입이기 때문에 런타임 시점에 아무런 역할을 할 수 없습니다. 타입스크립트의 타입은 `제거가능(erasable)`합니다.

> **Key Point💡**
>
> 실제로 자바스크립트로 컴파일되는 과정에서 모든 인터페이스, 타입, 타입 구문은 그냥 제거되어 버립니다.

- 위의 코드에서 다루고 있는 `shape`를 명확하게 하려면, 런타임에 타입 정보를 유지하는 방법이 필요합니다. 하나의 방법은 `height`속성이 존재하는지 체크해 보는 것입니다.

```ts
function calculateArea(shape: Shape) {
  if ("height" in shape) {
    shape; // 타입이 Rectangle
    return shape.width * shape.height;
  } else {
    shape; // 타입이 Square
    return shape.width * shape.width;
  }
}
```

속성 체크는 런타임에 접근 가능한 값에만 관련되지만, `타입 체커` 역시도 `shape`타입을 `Rectangle`로 보정해 주기 때문에 오류가 사라집니다. 타입 정보를 유지하는 또다른 방법으로는 런타임에 접근 가능한 타입 정보를 명시적으로 저장하는 `태그` 기법이 있습니다.

```ts
interface Square {
  kind: "square";
  width: number;
}
interface Rectangle {
  kind: "rectangle";
  width: number;
  height: number;
}

type Shape = Square | Rectangle;

function calculateArea(shape: Shape) {
  if (shape.kind === "rectangle") {
    shape; // 타입이 Rectangle
    return shape.width * shape.height;
  } else {
    shape; // 타입이 Square
    return shape.width * shape.width;
  }
}
```

`Shape` 는 `태그된 유니온`의 한 예시입니다. 이 기법은 런타임에 타입 정보를 손쉽게 유지할 수 있기 때문에, 타입스크립트에서 흔하게 볼 수 있습니다.
타입(런타임 접근 불가)과 값(런타임 접근 가능)을 둘 다 사용하는 기법도 있습니다. 타입을 `클래스`로 만들면 됩니다. Square와 Rectangle을 클래스로 만들면 됩니다.

```ts
class Square {
  constructor(public width: number) {}
}

class Rectangle extends Square {
  constructor(public width: number, public height: number) {
    super(width);
  }
}
type Shape = Square | Rectangle;

function calculateArea(shape: Shape) {
  if (shape instanceof Rectangle) {
    shape; // 타입이 Rectangle
    return shape.width * shape.height;
  } else {
    shape; // 타입이 Square
    return shape.width * shape.width;
  }
}
```

- 클래스로 작성해주면서 앞서 발생했었던 참조만 읽고 값으로서의 오류를 해결할 수 있었다.

> **Key Point💡**
>
> 인터페이스는 타입으로만 가능하지만, Rectangle을 클래스로 선언하면 타입과 값으로 모두 사용할 수 있디.

`type Shape = Square | Rectangle;` 부분에서 `Rectangle`은 탕비으로 참조되지만, `shape instanceof Rectangle`부분에서는 값으로 참조됩니다.

### 1.3.3. 타입 연산은 런타임에 영향을 주지 않습니다.

`string` 또는 `number` 타입인 값을 항상 `number`로 정제하는 경우를 가정해보자. 다음의 코드는 타입체커를 통과하지만 잘못된 방법을 사용했습니다.

```ts
function asNumber(val: number | string): number {
  return val as number;
}
```

변환된 자바스크립트 코드를 보면 이 함수가 실제로 어떻게 동작하는지 알 수 있습니다.

```js
function asNumber(val) {
  return val;
}
```

즉, 코드에 아무런 정제 과정이 없습니다. ~~(내가 여지껏 잘 못 사용했었다...)~~`as number` 는 타입 연산익도 런타임 동작에는 아무런 영향을 미치지 않습니다. 값을 정제하기 위해서는 런타임의 타입을 체크해야 하고 자바스크립트 연산을 통해 변환할 수행해야 합니다.

```ts
function asNumber(val: number | string): number {
  return typeof val === "string" ? Number(val) : val;
}
```

> **Key Point💡**
>
> `as` as `타입 단언문` 입니다. 컴파일러가 가진 정보를 무시하고 프로그래머가 원하는 임의의 타입을 값에 할당하는 것을 말한다. 즉, 컴파일 자체에 영향을 미치지 못한다.

### 1.3.4. 런타임 타입은 선언된 타입과 다를 수 있습니다.

```ts
function setLightSwitch(value: boolean) {
  switch (value) {
    case true:
      turnLightOn();
      break;
    case false:
      turnLightOff();
      break;
    default:
      console.log("실행되지 않을까 봐 걱정입니다.");
  }
}
```

타입스크립트는 일반적으로 실행되지 못하는 죽은 코드를 찾아내지만, 여기서는 `strict` 를 설정하더라도 찾아내지 못합니다. 그러면 마지막 부분을 실행할 수 있는 경우는 무엇일까? `:boolean` 타입선언문이라는 것에 주목해야 합니다. 타입스크립트의 타입이기 때문에 `:boolean`은 런타임에 제거 됩니다. 자바스크립트였다면 실수로 `setLightSwitch`을 `ON`으로 호출할 수 있었을 것입니다. 타입스크립트에서 마지막 `default`코드를 실행하는 방법이 있습니다.

```ts
function setLightSwitch(value: boolean) {
  switch (value) {
    case true:
      turnLightOn();
      break;
    case false:
      turnLightOff();
      break;
    default:
      console.log("실행되지 않을까 봐 걱정입니다.");
  }
}

interface LightApiResponse {
  lightSwitchValue: boolean;
}

async function setLight() {
  const response = await fetch("/light");
  const result: LightApiResponse = await response.json();
  setLightSwitch(result.lightSwitchValue);
}
```

`/light`를 요청할 때, 결과로 `LightApiResponse`를 반환하라고 선언했지만 실제로 그렇게 되리라는 보장이 없습니다. API를 잘못 파악해서 `LightApiResponse`가 문자열이었다면, 런타임에는 `setLightSwitch` 함수까지 전달 될 것입니다. 또는 배포된 후에 API가 변경되어 ` lightSwitchValue`가 문자열이 되는 경우도 있을 수 있습니다. 타입스크립트에서 런타임 타입과 선언된 타입이 맞지 않을 수 있습니다. 선언된 타입이 언제든지 달라질 수 있다는 것을 인지해야 합니다.

### 1.3.5. 타입스크립트는 타입으로는 함수를 오버로드할 수 없습니다.

C++같은 언어는 동일한 이름에 매개변수만 다른 여러 버전의 함수를 허용합니다. 이를 `함수 오버로딩`이라고 합니다. 그러나 타입스크립트에서는 타입과 런타임의 동작이 무관하기 때문에, 함수 오버로딩은 불가능합니다.

```ts
function add(a: number, b: number) {
  // 중복된 함수 구현입니다.

  return a + b;
}
function add(a: string, b: string) {
  // 중복된 함수 구현입니다.

  return a + b;
}
```

타입스크립트가 함수 오버로딩 기능으 ㄹ지원하기는 하지만, 온전히 타입 수준에서만 동작합니다. 하나의 함수에 대해 여러 개의 `선언문`을 작성할 수 있지만, `구현체()implementation`는 오직 하나 뿐입니다.

```ts
function add(a, b) {
  return a + b;
}

const tree = add(1, 2); // 타입이 number
const twelve = add("1", "2"); // 타입이 string
```

`add`에 대해 처음 두 개의 선언문은 타입 정보를 제공할 뿐입니다. 이 두 선언문은 타입스크립트가 자바스크립트로 변환되면서 제거되며, 구현체만 남게 됩니다.

### 1.3.6. 타입스크립트 타입은 런타임 성능에 영향을 주지 않습니다.

타입과 타입 연산자는 자바스크립트 변환 시점에 제거되기 때문에, **런타임의 성능에 아무런 영향을 주지 않습니다.** 타입 스크립트의 정적 타입은 실제로 비용이 전혀 들지 않습니다. 타입스크립트를 쓰는 대신 런타임 오버헤드를 감수하며 타입 체크를 해 본다면, 타입스크립트 팀이 주의사항들을 얼마나 테스트했는지 알 수 있습니다.

- `런타임` 오버헤드가 없는 대신, 타입스크립트 컴파일러는 `빌드타임` 오버헤드가 있습니다. 타입스크립트 팀은 컴파일러 성능을 매우 중요하게 생각합니다. 따라서, 컴파일은 일반적으로 상당히 빠른 편이며 특히 증분빌드시에 더욱 체감됩니다. 오버헤드가 커지면 빌드 도구에서 `트랜스파일`만 을 설정하여 타입 체크를 건너 뛸 수 있습니다.

- 타입스크립트가 컴파일하는 코드는 오래된 런타임 환경을 지원하기 위해 호환성을 높이고 성능 오버헤드를 감안할지 호환성을 포기하고 성능 중심의 네이티브 구현체를 선택할지의 문제에 맞닥뜨릴 수 있습니다. 에를 들어, 제너레이터 함수가 ES5 타깃으로 컴파일되려면 타입스크립트 컴파일는 호환성을 위한 특정 핼퍼 코드를 추가해야합니다.

## 요약

- 코드 생성은 타입 시스템과 무관하다.
- 타입스크립트 타입은 런타임 동작이나 성능에 영향을 주지 않는다.
- 타입 오류가 존재하더라도 코드 생성(컴파일)은 가능하다.
- 타입스크립트 타입은 런타임에 사용할 수 없다.
- 런타임에 타입을 지정하려면 타입 정보 유지를 위한 별도의 방법이 필요하다. 일반적으로는 태그된 유니온과 속성 체크 방법을 사용한다.
- 또는 클래스 같은 타입스크립트 타입과 런타임 값 둘다 제공하는 방법이 있다.
