# 1장 타입스크립트 알아보기

## 아이템 4 : 구조적 타이핑에 익숙해지기

자바스크립트는 본질적으로 덕 타이핑 기반입니다.

**\*덕타이핑**

- 객체가 어떤 타입에 부합하는 변수와 메서드를 가질 경우 객체를 해당 타입에 속하는 것으로 간주하는 방식

만약 어떤 함수의 매개변수 값이 몯구 제대로 주어진다면, 그 값이 어떻게 만들어졌는지 신경 쓰지 않고 사용합니다. 즉, 매개변수 값이 요구사항을 만족한다면 타입이 무엇인지 신경 쓰지 않는 동작을 그대로 모델링합니다. 그런데 타입 체커의 타입에 대한 이해도가 사람과 조금 다르기 때문에 가끔 예상치 못한 결과가 나오기도 합니다.

1. 물리 라이브러리와 2D 벡터 타입을 다루는 경우를 가정해보겠습니다.

```ts
interface Vector2D {
  x: number;
  y: number;
}
```

2. 벡터의 길이를 구하는 함수

```ts
function calculateLength(v: Vector2D) {
  return Math.sqrt(v.x * v.x + v.y * v.y);
}
```

3. 이름이 들어간 벡터를 추가

```ts
interface NamedVector {
  name: string;
  x: number;
  y: number;
}
```

`NamedVector`는 `number` 타입의 x와 y속성이 있기 때문에, `calculateLength`함수로 호출이 가능합니다.

```ts
const v: NamedVector = { x: 3, y: 4, name: "Zee" };
calculateLength(v); // 정상, 결과는 5
```

`Vector2D`와 `NamedVector`의 관계를 선언하지 않았지만, `NamedVector`를 위한 별도의 `calculateLength` 코드를 구현할 필요도 없습니다. 타입스크립트 타입 시스템은 자바스크립트의 런타임 동작을 모델링합니다.
`NamedVector`구조가, `Vector2D`와 호환되기 때문에 `calculateLength`함수가 호출이 가능했던 것입니다. 여기서 **구조적 타이핑(Structural Typing)**이라는 용어를 사용합니다.

비슷하게 구조적 타이핑때문에, 문제가 발생하기도 합니다.

```ts
interface Vector3D {
  x: number;
  y: number;
  z: number;
}
```

벡터의 길이를 1로 만드는 정규화 함수를 작성합니다.

```ts
function normalize(v:Vector3D){
  const length = calculateLength(v)
  return {
    x:v.x / length
    y:v.y / length
    z:v.z / length
  }
}

```

그러나 이 함수는 1보다 조금 더 긴(1.41) 길이를 가진 결과를 출력할 것입니다.

```ts
normalize({ x: 3, y: 4, z: 5 });
// {x:0.6, y:0.8, z:1}
```

함수를 작성할 때, 호출에 사용되는 매개변수의 속성들이 매개변수의 타입에 선언된 속성만을 가질거라 생각하기 쉽습니다. 이러한 타입은 `봉인된` 또는 `정확한` 타입이라고 불리며 타입스크립트 타입 시스템에서는 표현할 수 없습니다. 좋든 싫든 타입은 **열려 있습니다.**

```ts
interface Vector3D {
  x: number;
  y: number;
  z: number;
}

function calculateLengthL1(v: Vector3D) {
  let length = 0;

  for (const axis of Object.keys(v)) {
    const coord = v[axis]; // string은 Vector3D의 인덱스로 사용할 수 없기에 엘리먼트는 암시적으로 any 타입입니다.

    length += Math.abs(coord);
  }
  return length;
}
```

앞서 `Vector32D` 는 봉인(다른 속성이 없다)되었다고 가정했습니다. 그런데 코드로처럼 작성할 수도 있습니다.

```ts
const vec3D = { x: 3, y: 4, z: 1, address: "123 Broadway" };
calculateLengthL1(vec3D); // 정상, NaN을 반환합니다.
```

V는 어떤 속성이든 가질 수 있기 때문에, `axis`의 타입은 string이 될 수 도 있습니다. 그러므로 앞서 본 것처럼 `v[axis]`가 어떤 속성이 될지 알 수 없기 때문에, `number`라고 확정할 수 없습니다. 정확한 타입으로 객체를 순회하는 것은 까다로운 문제입니다. 따라서 루프보다는 모든 속성을 각각 더하는 구현이 더 낫습니다.

```ts
function calculateLengthL1(v: Vector3D) {
  return Math.abs(v.x) + Math.abs(v.y) + Math.abs(v.z);
}
```

**구조적 타이핑은 클래스와 관련된 할당문에서도 당황스러운 결과를 보여줄 수 있습니다.**

```ts
class C {
  foo: string;
  constructor(foo: string) {
    this.foo = foo;
  }
}

const c = new C("instance of C");
const d: C = { foo: "object literal" }; // 정상
```

d가 `C` 타입에 할당이 되는 이유는? d는 string 타입의 foo 속성을 가집니다. 게다가 하나의 매개변수(보통은 매개변수 없이 호출되지만)로 호출이 되는 생성자(Object.prototype으부터 비롯된)를 가집니다.

## 요약

- 자바스크립트가 덕 타이핑 기반이고, 타입스크립트가 이를 모델링하기 위해 `구조적 타이핑`을 사용합니다.
- 어떤 인터페이스에 할당 가능한 값이라면 타입 선언에 명시적으로 나열된 속성들을 가지고 있을 것입니다. 타입은 `봉인` 되어 있지 않습니다.
- 클래스 역시 구조적 타이핑 규칙을 따르는 것을 명심해야 합니다.
- 클래스의 인스턴스가 예상과 다를 수 있습니다.
- 구조적 타이핑을 사용하면 유닛 테스팅을 손쉽게 할 수 있습니다.
