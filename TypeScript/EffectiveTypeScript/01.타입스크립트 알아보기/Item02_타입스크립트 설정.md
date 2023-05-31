# 1장 타입스크립트 알아보기

타입스크립트는 사용 방식 면에서 독특한 언어이다. 인터프리터(파이썬,루비)같은 걸로 실행되는 것이 아니고, 저수준 언어로 컴파일(자바, c)로 되는 것도 아니다. **고수준 언어인 자바스크립트로 컴파일 되며 실행 역시 타입스크립트가 아닌, 자바스크립트로 이루어집니다.** 그래서 타입스크립트와 자바스크립트는 필연적인 관계입니다.

## 아이템 2 : 타입스크립트 설정 이해하기

```ts
function add(a, b) {
  return a + b;
}
add(10, null);
```

다음의 코드는 타입 체커를 통과할 수 없습니다. 이 설정들은 커맨드 라인에서 사용할 수 있습니다.

```bash
tsc --noImplicitAny program.ts
```

또한, `tsconfig.json`설정 파일을 통해서도 가능합니다.

```ts

{
  "compilerOptions":{
    "noImplicitAny":true
  }
}

```

가급적 설정파일을 사용하는 것이 좋습니다. 그래야만 타입스크립트를 어떻게 사용할 계획인지 동료들이나 다른 도구들이 알 수 있습니다. 설정 파일은 `tsc --init`만 실행하면 간단히 생성됩니다.

타입스크립트의 설정들은 어디서 소스 파일을 찾을지, 어떤 종류의 출력을 생성할지 제어하는 내용이 대부분입니다. 언어에서는 허용하지 않는 고수준 설계의 설정입니다. 타입스크립트는 어떻게 설정하느냐에 따라 완전히 다른 언어처럼 느껴질 수 있습니다. 설정을 제대로 사용하려면 `noImplicitAny`와 `strictNullChecks`를 이해해야 한다.

> **Key Point💡**
>
> `noImplicitAny` : 변수들이 미리 정의된 타입을 가져야 하는지 여부를 제어합니다.

다음의 코드는 `noImplicitAny`가 해제되어 있을 때 유효합니다.

```ts
function add(a, b) {
  return a + b;
}
```

편집기에서 `add`부분에 마우스를 올려보면 타입 스크립트가 추론한 함수의 타입을 알 수 있습니다.

```ts
function add(a: any, b: any): any;
```

- `any` 타입을 매개변수에 사용하면 타입 테커는 무력해집니다. `any`는 유용하지만 매우 주의해서 사용해야 합니다.

```ts
function add(a, b) {
  // ~ 'a' 매개변수에는 암시적으로 'any' 형식이 포함됩니다.
  // ~ 'b' 매개변수에는 암시적으로 'any' 형식이 포함됩니다.
  return a + b;
}
```

`any`를 코드에 넣지는 않았지만, `any`타입으로 간주되기 때문에 이를 `암시적 any`라고 부릅니다. 그런데 같은 코드임에도 `noImplicitAny`가 설정되었다면 오류가 됩니다.

> **Key Point💡**
>
> `noImplicitAny`로 인한 오류는 any라고 선언해 주거나 더 분명한 타입을 사용하면 해결할 수 있습니다.

```ts
function add(a: number, b: number) {
  return a + b;
}
```

타입스크립트는 타입 정보를 가질 때 가장 효과적이기 때문에, 되도록이면 `noImplicitAny`를 설정해야 합니다. 새 프로젝트를 시작한다면 처음부터 `noImplicitAny`설정하여 코드를 작성할 때마다 타입을 명시하도록 해야 합니다.

- 코드의 가독성이 좋아지며
- 개발자의 생산성이 향상됩니다.

> **Key Point💡**
>
> `strictNullChecks`는 `null`과 `undefined`가 모든 타입에서 허용되는지 확인하는 설정입니다.

다음은 `strickNullChecks`가 해제되었을 때 유효한 코드입니다.

```ts
const x: number = null; // 정상, null은 유효한 값입니다.
```

그러나 `strictNullChecks`를 설정하면 오류가 나타납니다.

```ts
const x: number = null; // ~ 'null' 형식은 number에 할당할 수 없습니다.
```

null대신 undefined를 써도 같은 오류가 나타납니다. 만약 `null`을 사용하려 한다면 의도를 명시적으로 드러냄으로써 오류를 고칠 수 있습니다.

```ts
const x: number | null = null;
```

만약 null을 허용하지 않으려면, 이 값이 어디서부터 왔는지 찾아야 하고, null을 체크하는 코드나 `단언문(assertion)`을 추가해야 합니다.

```ts
const el = document.getElementById("status");
el.textContent = "Ready";
// ~~ 개체가 null인것 같습니다.

if (el) {
  el.textContent = "Ready"; // 정상, null은 제외됩니다.
}
el!.textContent = "Ready"; // 정상, el이 null이 아님을 단언합니다.
```

`strictNullChecks`는 null과 undefined 관련된 오류를 잡아 내는 데 많은 도움이 되지만, 코드 작성을 더 어렵게 만듭니다. 새 프로젝트를 시작한다면 가급적 `strictNullChecks`를 설정하는 것이 좋지만, 타입스크립트가 처음이거나 자바스크립트 코드를 마이그레이션하는 중이라면 설정하지 않아도 좋다습니다.

`strictNullChecks`를 설정하려면 `noImplicitAny`를 먼저 설정해야 합니다. `strictNullChecks`설정없이 개발하고자 한다면 `undefined`는 객체가 아닙니다. 라는 런타임 오류를 주의해야 합니다.

결국, 이러한 오류들 때문에 엄격한 체크를 설정할 수 밖에 없습니다. 프로젝트가 커질 수록 설정 변경이 어려워질 것이므로, 가능한 초반에 설정하는 것이 좋습니다.

> **Key Point💡**
>
> `strictNullChecks`과 `noImplicitAny`를 모두 체크를 설정하고 싶다면 `strict` 설정을 하면 됩니다.

`strict`설정 시 대부분의 오류를 잡아냅니다.

> **Key Point💡**
>
> 공동 프로젝트 진행 중 동료에게 타입스크립트 코드를 공유했을 때, 오류가 재현되지 않는다면 컴파일러 설정이 동일한지 먼저 확인해봐야 합니다.

## 요약

- 타입스크립트 컴파일러는 언어의 핵심 요소에 영향을 미치는 몇 가지 설정을 포함하고 있습니다.
- 타입스크립트 설정은 커맨드 라인을 이용하기 보다는 `tsconfig.json`을 설정하는 것이 더 좋습니다.
- 자바스크립트 프로젝트를 타입스크립트로 전환하는 게 아니라면, `noImplicitAny`를 설정하는 것이 좋습니다.
- 타입스크립트는 타입 정보를 가질 때 가장 효과적이기 때문에, 되도록이면 `noImplicitAny`를 설정해야 합니다.
- "`undefined`는 객체가 아닙니다." 같은 런타임 오류를 방지하기 위해 `strictNullChecks`를 설정하는 것이 좋습니다.
  - `strictNullChecks`설정을 해제할 경우 발생할 수 있습니다.
- `strictNullChecks`설정시 프로젝트가 커질 수록 설정 변경이 어려워질 것이므로, 가능한 초반에 설정하는 것이 좋습니다.
- 타입스크립트에서 엄격한 체크를 하고 싶다면 `strict`설정을 고려해야 합니다.
