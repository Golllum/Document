## Javascript

- Falsy value

  - 0, "", null, undefined, NaN
  - array는 Object 이므로 toString() 함수를 가지는데, 이 함수는 각 원소를 ,로 구분하여 문자열로 만드는 함수이다. 따라서 array가 연산에 사용됐을 때 내부적으로 toString() 함수가 호출되어 array를 string으로 바꾸고 연산을 한다.

    ```
    if([] == 0) {
      // true
    }

    // 1단계 - [] == 0 => '' == 0  :  배열 []이 빈 문자열 ''로 변환된다.
    if('' == 0) {
      // true
    }

    // 2단계 - '' == 0 => 0 == 0 : 문자열 ''이 숫자 0으로 변환된다.
    if(0 == 0) {
      // true
    }

    // 3단계 - 0 == 0 => true
    if(true) {
      // true
    }
    ```

- Single Threaded Language

  - 하나의 Stack에서 실행되기 때문에 병렬 처리를 할 수 없다.
  - 한 번에 코드 하나만 실행 가능하다.
  - ajax, eventListener, setTimeout 등은 stack에 쌓아두고 대기하지 않는다.
  - 대기 공간에 저장해뒀다가 실행 타이밍에 callback Queue OR event Queue에 올라간다.

- promise API (ES6)

  - 자바스크립트는 비동기 처리를 위해 콜백함수를 사용한다. 하지만 콜백함수 남용으로 인해 콜백 지옥에 빠질 수 있다.
  - 에러처리가 힘들고 여러 개의 비동기 처리를 한번에 하는데 한계가 있다.
  - Promise 객체는 비동기 로직을 마치 동기처럼 사용할 수 있는 기능을 제공한다.
  - promise 특징
    ```
    1. 비동기 처리 시점을 명확하게 표현할 수 있다.
    2. 연속된 비동기 처리 작업을 수정, 삭제, 추가하기 편하고 유연하다.
    3. 비동기 작업 상태를 쉽게 확인할 수 있다.
    4. 코드의 유지 보수성이 향상된다.
    ```
  - promise 상태
    ```
    1. Pending(대기)    : 비동기 로직 처리의 미완료 상태
    2. Fulfilled(이행)  : 비동기 로직 처리의 완료 상태로, promise 결과값을 반환한 상태. (resolve메소드 호출 완료된 상태)
    3. Rejected(거절)   : 비동기 로직 처리의 실패 또는 오류 상태
    ```
  - promise 사용예시

    ```
    // Pending 상태
    new Promise((resolve, reject) => {});   // Promise 객체 할당

    // Fulfilled & Rejected 상태
    new Promise((resolve, reject) => {
        if(true){
            resolve();  // fulfilled 상태
        }else{
            reject();   // rejected 상태
        }
    }).then((returnValue) => {
        console.log(returnValue);
    }).catch((error) => {
        console.log(error);
    }).finally((value) => {
        console.log(value);
    });
    ```

- async 함수 (ES7)

  - function 키워드 앞에 async 키워드를 붙이면 해당 함수는 항상 promise 객체를 반환한다.
  - promise 가 아닌 값을 return 해도 이행 상태의 promise 객체로 감싸 이행된 promise 객체를 반환한다.
  - await 함수는 async 함수 안에서만 동작한다.

- await 함수 (ES7)

  - Javascript는 await 키워드를 만나면 promise가 처리될 때까지 대기한다.
  - promise가 처리되면 그 결과와 함께 실행이 재게되며 promise가 처리되는 동안에는 엔진이 다른 일(다른 스크립트 실행, 이벤트 처리 등)을 할 수 있으므로, CPU 리소스가 낭비되지 않는다.
  - await는 promise.then보다 좀 더 세련되게 promise의 result 값을 얻을 수 있게 해주는 문법이다.
  - promise.then처럼 await 에도 thenable 객체 (then 메서드가 있는 호출 가능한 객체)를 사용할 수 있다.

  ```
  // async 내 await 사용 예시
  (async () => {
      let response = await fetch('/article/promise-chaining/user.json');
      let user = await response;
  })
  ```

- axios 라이브러리
  - 브라우저, nodeJS를 위한 Promise API를 활용하는 HTTP 비동기 통신 라이브러리
  - BE <-> FE 간 통신을 위해 Ajax와 더불어 사용
  - JS : fetch 메소드 사용 // FW : axios 메소드 사용
  - 운영 환경에 따라 브라우저의 XMLHttpRequest 객체 또는 NodeJS의 HTTP API 사용
  - Promise API를 활용
  - HTTP 요청과 응답을 JSON 형태로 자동 변경
