## [ Module ]

- 모듈은 대개 클래스 하나 혹은 특정한 목적을 가진 복수의 함수로 구성된 라이브러리 하나로 구성.
- 모듈은 단지 파일 하나에 불과하며, 스크립트 하나는 모듈 하나이다.
- 스크립트의 크기가 점차 커지고 기능도 복잡해지자 자바스크립트 커뮤니티는 특별한 라이브러리를 만들어 필요한 모듈을 언제든지 불러올 수 있게 해준다거나 코드를 모듈 단위로 구성해 주는 방법을 만드는 등 다양한 시도함.

  ```
  1) AMD – 가장 오래된 모듈 시스템 중 하나로 require.js라는 라이브러리를 통해 처음 개발되었습니다.
  2) CommonJS – Node.js 서버를 위해 만들어진 모듈 시스템입니다.
  3) UMD – AMD와 CommonJS와 같은 다양한 모듈 시스템을 함께 사용하기 위해 만들어졌습니다.

  >> 이런 모듈 시스템은 오래된 스크립트에서 여전히 발견할 수 있는데, 이제는 역사의 뒤안길로 사라져가고 있다.
  ```

- 이 이후로 관련 문법은 진화를 거듭해 이제는 대부분의 주요 브라우저와 Node.js가 모듈 시스템을 지원하고 있다.

Module 사용 예시

- 모듈에 특수한 지시자 export와 import를 적용하면 다른 모듈을 불러와 불러온 모듈에 있는 함수를 호출하는 것과 같은 기능 공유가 가능하다.

  ```
  export 지시자를 변수나 함수 앞에 붙이면 외부 모듈에서 해당 변수나 함수에 접근할 수 있다(모듈 내보내기).
  import 지시자를 사용하면 외부 모듈의 기능을 가져올 수 있다(모듈 가져오기).

  // example.js
  export function examFunc(user) {
    alert(`Hello, ${user}!`);
  }

  // main.js
  import {examFunc} from './example.js';

  alert(examFunc); // 함수
  sayHi('John'); // Hello, John!
  ```

- 모듈은 특수한 키워드나 기능과 함께 사용되므로 \<script type="module"> 같은 속성을 설정해 해당 스크립트가 모듈이란 걸 브라우저가 알 수 있게 해줘야함.

  ```
  <!doctype html>
  <script type="module">
  import {sayHi} from './say.js';

  document.body.innerHTML = sayHi('John');
  </script>
  ```

- 모듈은 로컬 파일에서 동작하지 않고, HTTP 또는 HTTPS 프로토콜을 통해서만 동작한다.  
  로컬에서 file:// 프로토콜을 사용해 웹페이지를 열면 import, export 지시자가 동작하지 않음.  
  로컬 웹 서버인 static-server나, 코드 에디터의 ‘라이브 서버’ 익스텐션(Visual Studio Code 에디터의 경우 Live Server Extension)을 사용하여 테스트 가능.

Module 핵심기능

- 항상 Strict mode 로 실행됨
  - 모듈은 항상 엄격 모드(use strict)로 실행됨. 선언되지 않은 변수에 값을 할당하는 등의 코드는 에러를 발생.
    ```
    <script type="module">
    a = 5; // 에러
    </script>
    ```
- Module Level Scope 적용

  - 모듈은 자신만의 스코프가 있다. 따라서 모듈 내부에서 정의한 변수나 함수는 다른 스크립트에서 접근할 수 없다.
  - 외부에 공개하려는 모듈은 export 해야 하고, 내보내진 모듈을 가져와 사용하려면 import 해줘야 함.

    ```
    // hello.js
    import {user} from './user.js';
    document.body.innerHTML = user; // John

    // user.js
    export let user = "John";

    // index.html
    <!doctype html>
    <script type="module" src="hello.js"></script>
    ```

  - 브라우저 환경에서도 \<script type="module">을 사용해 모듈을 만들면 독립적인 스코프가 만들어짐.

    ```
    <script type="module">
    // user는 해당 모듈 안에서만 접근 가능합니다.
    let user = "John";
    </script>

    <script type="module">
    alert(user); // Error: user is not defined
    </script>
    ```

- 단 한 번만 평가됨

  - 동일한 모듈이 여러 곳에서 사용되더라도 모듈은 최초 호출 시 단 한 번만 실행.
  - 실행 후 결과는 이 모듈을 가져가려는 모든 모듈에서 공유.

    ```
    // admin.js
    export let admin = {
    name: "John"
    };

    // aa.js
    import {admin} from './admin.js';
    admin.name = "Pete";

    // bb.js
    import {admin} from './admin.js';
    alert(admin.name); // Pete

    >> aa.js와 bb.js 모두 같은 객체를 가져오므로, aa.js에서 객체에 가한 조작을 bb.js에서도 확인할 수 있다.
    ```

- 지연 실행

  - 모듈 스크립트는 항상 지연 실행된다. 외부 스크립트, 인라인 스크립트와 관계없이 마치 defer 속성을 붙인 것처럼 실행된다.

    ```
    - 외부 모듈 스크립트 <script type="module" src="...">를 다운로드할 때 브라우저의 HTML 처리가 멈추지
      않는다. 브라우저는 외부 모듈 스크립트와 기타 리소스를 병렬적으로 불러온다.
    - 모듈 스크립트는 HTML 문서가 완전히 준비될 때까지 대기 상태에 있다가 HTML 문서가 완전히 만들어진 이후에
      실행된다. 모듈의 크기가 아주 작아서 HTML보다 빨리 불러온 경우에도 마찬가지이다.
    - 스크립트의 상대적 순서가 유지된다. 문서상 위쪽의 스크립트부터 차례로 실행됨.

    >> 이런 특징 때문에 모듈 스크립트는 항상 완전한 HTML 페이지를 ‘볼 수’ 있고 문서 내 요소에도 접근할 수 있음.
    ```

Module System 종류

1. CommonJS

- require 키워드를 사용하여 외부 모듈을 불러옴.
- NodeJS에서 사용되고 있는 CommonJS 키워드.
- 필요성
  ```
  많은 프로젝트에서 ES6 모듈 시스템을 점점 더 널리 사용되고 있는 추세이기는 하지만, 안타깝게도 아직까지 항상 import 키워드를 사용해서 코딩을 할 수 없다. <script> 태그를 사용하는 브라우저 환경에서는 물론이고, NodeJS에서도 CommonJS를 기본 모듈 시스템으로 채택하고 있기 때문에, Babel과 같은 ES6 코드를 변환(transpile)해주는 도구를 사용할 수 없는 상황에서는 좋든 싫든 require 키워드를 사용해야 한다. 따라서 CommonJS 사용 방법도 어느 정도 숙지하고 있어야 한다.
  ```
- 사용법

  CommonJS 방식으로 모듈을 내보낼 때는 ES6처럼 명시적으로 선언하는 것이 아니라 특정 변수나 그 변수의 속성으로 내보낼 객체를 세팅해줘야 한다. 특히, 제일 햇갈리는 부분이 바로 유사해보이는 exports 변수와 module.exports 변수를 상황에 맞게 잘 사용해야 한다는 것이다.

  - 여러 개의 객체를 내보낼 경우, exports 변수의 속성으로 할당한다.

    ```
    1. 복수 객체 내보내기/불러오기

    // test.js
    const exchangeRate = 0.91;

    function roundTwoDecimals(amount) {
    return Math.round(amount * 100) / 100;
    }

    const canadianToUs = function (canadian) {
    return roundTwoDecimals(canadian * exchangeRate);
    };

    function usToCanadian(us) {
    return roundTwoDecimals(us / exchangeRate);
    }

    exports.canadianToUs = canadianToUs; // 내보내기 1
    exports.usToCanadian = usToCanadian; // 내보내기 2


    // call-test.js
    const currency = require("./test");

    console.log("50 Canadian dollars equals this amount of US dollars:");
    console.log(currency.canadianToUs(50));

    console.log("30 US dollars equals this amount of Canadian dollars:");
    console.log(currency.usToCanadian(30));
    ```

  - 딱 하나의 객체를 내보낼 경우, module.exports 변수 자체에 할당한다.

    ```
    2. 단일 객체 내보내기/불러오기

    // test.js
    const exchangeRate = 0.91;

    // 안 내보냄
    function roundTwoDecimals(amount) {
    return Math.round(amount * 100) / 100;
    }

    // 내보내기
    const obj = {};
    obj.canadianToUs = function (canadian) {
    return roundTwoDecimals(canadian * exchangeRate);
    };
    obj.usToCanadian = function (us) {
    return roundTwoDecimals(us / exchangeRate);
    };
    module.exports = obj;


    // call-test.js
    const currency = require("./test");

    console.log("50 Canadian dollars equals this amount of US dollars:");
    console.log(currency.canadianToUs(50));

    console.log("30 US dollars equals this amount of Canadian dollars:");
    console.log(currency.usToCanadian(30));
    ```

2. import (ES6 Module system)

- import, from, export, default처럼 모듈 관리 전용 키워드를 사용하기 때문에 가독성이 좋다.
- 비동기 방식으로 작동하고 모듈에서 실제로 쓰이는 부분만 불러오기 때문에 성능과 메모리 부분에서 유리하다.
- Named Parameter와 같이 CommonJS에서는 지원하지 않는 기능들이 있다.
- 사용법

  - CommonJS에서는 내보낼 복수 객체들을 exports 변수의 속성으로 할당하는 방식을 썼었는데, ES6에서는 import 키워드의 짝꿍인 export 키워드를 사용해서 명시적으로 선언한다. 이 때 내보내는 변수나 함수의 이름이 그대로 불러낼 때 사용하게 되는 이름이 되며 때문에 이를 Named Exports라고 한다.

  ```
  1. 복수 객체 내보내기/불러오기

  // test.js
  const exchangeRate = 0.91;

  // 안 내보냄
  function roundTwoDecimals(amount) {
    return Math.round(amount * 100) / 100;
  }

  // 내보내기 1
  export function canadianToUs(canadian) {
    return roundTwoDecimals(canadian * exchangeRate);
  }

  // 내보내기 2
  const usToCanadian = function (us) {
    return roundTwoDecimals(us / exchangeRate);
  };

  export { usToCanadian };


  // call-test.js
  // Destructuring
  import { canadianToUs } from "./currency-functions";

  console.log("50 Canadian dollars equals this amount of US dollars:");
  console.log(canadianToUs(50));

  // Alias
  import * as currency from "./currency-functions";

  console.log("30 US dollars equals this amount of Canadian dollars:");
  console.log(currency.usToCanadian(30));

  >> 여러 객체(Named Exports)를 불러올 때는 ES6의 Destructuring 문법을 사용해서 필요한 객체만 선택적으로 전역에서 사용하거나, 모든 객체에 별명을 붙이고 그 별명을 통해서 접근할 수도 있다.
  ```

  - CommonJS에서는 내보낼 단일 객체를 module.exports 변수에 할당하는 방식을 썼었는데, ES6에서는 그 대신 export default 키워드를 사용해서 명시적으로 선언한다. 하나의 모듈에서 하나의 객체만 내보내기 때문에 이를 Default Export라고 부른다.

  ```
  // test.js
  const exchangeRate = 0.91;

  // 안 내보냄
  function roundTwoDecimals(amount) {
      return Math.round(amount * 100) / 100;
  }

  // 내보내기
  export default {
      canadianToUs(canadian) {
          return roundTwoDecimals(canadian * exchangeRate);
      },

      usToCanadian: function (us) {
          return roundTwoDecimals(us / exchangeRate);
      },
  };

  >> 이름이 필요없기 때문에 별도로 변수 할당 없이 바로 객체를 내보내기를 할 수 있습니다. 내보낼 때 어떤 이름도 지정하기 않기 때문에 불러올 때도 아무 이름이나 사용할 수 있습니다.


  // call-test.js
  import currency from "./test";

  console.log("50 Canadian dollars equals this amount of US dollars:");
  console.log(currency.canadianToUs(50));

  console.log("30 US dollars equals this amount of Canadian dollars:");
  console.log(currency.usToCanadian(30));

  >> currency라는 객체명은 불러오는 쪽에서 마음대로 지정할 수 있다. export 객체에 이름이 붙어있다고 해도 import 객체명은 새로 작명할 수 있다.
  ```

- 한 가지 주의점은 Babel 없이 순수하게 Node.js 최신 버전으로 ES 모듈을 사용한다면, import를 사용할 때 .js 확장자를 붙여야 한다.
