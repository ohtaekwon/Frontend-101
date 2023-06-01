## Start a New React Project

> 새 React 프로젝트 시작하기

새 앱이나 새 웹사이트를 React로 완전히 구축하기 위해서는 커뮤니티에서 인기 있는 React 기반 프레임워크 중 하나를 선택하는 것이 좋습니다.
프레임워크로는 `라우팅`, `데이터 패치하기`, `HTML 생성` 등 대부분의 앱과 사이트에서 궁극적으로 필요로 하는 기능을 제공합니다.

### Note

You need to install Node.js for local development. You can also choose to use Node.js in production, but you don’t have to. Many React frameworks support export to a static HTML/CSS/JS folder.

> **로컬 개발을 위해서는** Node.js를 설치해야 합니다. 프로덕션 환경에서 Node.js를 선택하여 사용할 수도 있지만, 반드시 그럴 필요는 없습니다. 많은 React 프레임워크가 정적 HTML/CSS/JS 폴더로 내보내기를 지원합니다.

## Production-grade React frameworks

> 프로덕션 등급 React 프레임워크

### Next.js

Next.js는 **풀스텍 React 프레임워크**로서, 이 프레임워크는 다용도로 사용할 수 있으며, 정적인 블로그부터 복잡한 동적 애플리케이션에 이르기까지 모든 규모의 React 앱을 만들 수 있다. 새 Next.js프로젝트를 생성하려면 터미널에서 다음과 같이 실행하시오.

```shell
npx create-next-app
```

### 추가적으로 최신의 Next.js 13버전을 설치하려면

```shell
npx create-next-app@latest --experimental-app

```

> Next.js를 처음 사용하는 경우 [Next.js 튜토리얼](https://nextjs.org/learn/foundations/about-nextjs)을 확인하세요.

Next.js는 Vercel에서 유지 관리합니다. Node.js또는 서버리스 호스팅 또는 자체 서버에 Next.js 앱을 배포할 수 있으며, 완전히 정적인 Next.js앱은 모든 정적 호스팅에 배포할 수 있습니다.

## Custom toolchains

### Choose Package Managers

패키지 관리자를 사용하면 패키지를 설치, 업데이트 및 관리할 수 있습니다.

- 인기있는 패키지 관리자 : `npm(Node.js내장)`, `yarn`, `pnpm`

### Compiler

컴퍼일러를 사용하면 최신 언어 기능과 `JSX` 또는 브라우저용 타입 어노테이션과 같은 추가 구문을 컴파일할 수 있습니다.

- 인기있는 컴파일러 : `바벨`, `타입스크립트`, `SWC`

**\*컴파일러란?**

> 프로그래밍언어로 작성된 소스 코드를 다른 프로그래밍 언어나 기계어로 변환해주는 소프트웨어 도구입니다. 컴파일러는 소스 코드를 입력하고 받아들여 그것을 분석하고, 중간 단계를 거쳐 최종적으로 기계어로 변환하여 실행 파일을 생성합니다.

컴파일러는 보통 다음과 같은 단계로 동작합니다.

- `구문분석`, `의미분석`, `중간 코드 생성`, `최적화`, `목적코드 생성`

### Bundler

번들러를 사용하면 모듈식 코드를 작성하고 이를 작은 패키지로 묶어 로드 시간을 최적화할 수 있습니다.

- 인기있는 번들러 : `웹팩`, `파셀`, `에스필드`, `SWC`, `Rollup`

**\*번들러란?**

> 번들러는 프론트엔드 웹 개발에서 사용되는 도구로, 여러 개의 소스 파일 및 종속성을 하나의 단일 파일로 번들링하는 역할을 합니다. 웹 애플리케이션은 보통 다수의 HTML, CSS, JavaScript 파일 및 이미지, 폰트 등의 리소스로 구성되어 있습니다. 번들러는 이러한 파일들을 하나로 묶어 웹 페이지 로딩 속도를 향상시키고, 개발자가 모듈화된 구조로 코드를 작성하고 관리하도록 도와주는 역할을 합니다.

번들러의 작동원리

- `의존성 관리`, `번들링`, `트렌스파일링`, `압축 및 최적화`

### Minifier

미니파이어를 사용하면 코드를 더 압축하여 더 빠르게 로드할 수 있습니다.

- 인기있는 미니파이어 : `Terser`, `SWC`

**\*미니파이어란?**

> 미니파이어는 소스 코드의 크기를 최소화하기 위해 공백, 주석, 줄 바꿈 등을 제거하고 도구 또는 알고리즘을 말합니다. 미니파이어를 사용하면 파일 크기를 줄이고, 웹 페이지의 로딩 속도를 향상 시킬 수 있습니다.

미니파이어는 주로 JavaScript, CSS, HTML과 같은 웹 프론트엔드 리소스를 대상으로 적용됩니다.

#### e.g. JavaScript minifier

```js
// 원본 JavaScript 코드
function sayHello(name) {
  console.log("Hello, " + name);
}

sayHello("John");

// 미니파이어 적용 후
function sayHello(a) {
  console.log("Hello, " + a);
}
sayHello("John");
```

- 미니파이어 도구와 라이브러리 : `UglifyJS`, `Terser`, `Closure Compiler`

### Server

서버는 컴포넌트를 HTML로 랜더링할 수 있도록 서버 요청을 처리합니다.

- 인기있는 서버 : `Express`

### Linter

린터는 코드에 일반적인 실수가 있는지 검사하고 교정을 하도록 합니다.

- 인기있는 린터 : `ESLint`

### Test

테스트 러너를 사용하면 코드에 대한 테스트를 실행할 수 있습니다.

- 인기있는 테스트 러너 : `Jest`
- 추가 : `Vitest`, `react-testing-library`, `cypress`, `playwright`
