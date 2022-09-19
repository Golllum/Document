## Babel: JavaScript Transpiler

- 소스 코드를 머신 코드로 바꿔주는 compile과 달리, transpile은 같은 언어를 유지한체 다른 런타임 환경에서 해당 코드가 정상적으로 해석될 수 있도록 형태만 바꿔준다는 차이가 있다. 필드에서는 이 두 언어를 혼용해서 사용하는 경우가 많다.

- Babel Packages

  ```
  @babel/core : Babel 핵심 패키지
  @bable/cli  : Babel command line 툴 패키지
      > babel 커맨드를 사용하면 자바스크립트 코드를 transpile할 수 있다.
  @babel/preset-env : 가장 범용적으로 사용되는 babel 프리셋
      > env 프리셋은 ES2015 이상의 최신 자바스크립트 문법으로 작성된 코드를 해석할 수 있다.
  @babel/node : transpile & node 실행을 한 번에 할 수 있게 해주는 패키지
      > ASIS $ npx babel --presets @babel/env index.js | node
      > TOBE $ npx babel-node --presets @babel/env index.js
  ```

- 바벨 커맨드를 실행할 때 마다 매번 프리셋 옵션을 붙이기가 번거롭다면 바벨 설정 파일인 .babelrc를 프로젝트 최상위 디렉터리에 작성

  ```
  // .babelrc
  {
     "presets": ["@babel/env"],
  }
  ```

- .babelrc 대신 package.json 파일에 설정할 수도 있다.

  ```
  {
      (... 생략 ...)
      "devDependencies": {
          "@babel/cli": "^7.10.4",
          "@babel/core": "^7.10.4",
          "@babel/node": "^7.10.4",
          "@babel/preset-env": "^7.10.4"
      },
      +  "babel": {
      +    "presets": ["@babel/env"]
      +  },
      (... 생략 ...)
  }

  >> $ npx babel-node index.js
  ```

- npm script에 등록하여 사용하는 방법도 있다.
  ```
  {
      (... 생략 ...)
      "scripts": {
          "start": "babel-node index.js"
      },
      (... 생략 ...)
  }
  ```
