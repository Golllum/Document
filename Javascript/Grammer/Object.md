## 객체 문법 정리

- Optional chaining

  - ?. 문법
  - 프로퍼티가 없는 중첩 객체를 에러 없이 안전하게 접근
  - ?.은 ?. 왼쪽 대상이 undefined나 null이면 평가를 멈추고 undefined를 반환.

  ```
  const person1 = {
      name: 'Ellie',
      job: {
          title: 'S/W Engineer',
          manager: {
          name: 'Bob',
          },
      },
  };

  const person2 = {

  };


  // Error 발생
  function printManager(person) { // 중첩 객체의 값을 불러오는 함수
      console.log(person.job.manager.name);
  }
  printManager(person1); // Bob
  printManager(person2); // TypeError: Cannot read property 'job' of undefined


  // && 연산자 : 왼쪽 값이 Falsy 값이면 왼쪽값 반환
  function printManager(person) {
      // person.job : undefined
      console.log(person.job && person.job.manager && person.job.manager.name);
  }
  printManager(person1); // Bob
  printManager(person2); // undefined

  // ?. 연산자 : 왼쪽 값이 undefined나 null이면 undefined를 반환
  function printManager(person) {
      console.log(person?.job?.manager?.name);
  }
  printManager(person1); // Bob
  printManager(person2); // undefined
  ```

  - ?.() 문법

  ```
  let user1 = {
    admin() {
      alert("관리자 계정입니다.");
    }
  }

  let user2 = {};

  user1.admin?.(); // 관리자 계정입니다.
  user2.admin?.(); // undefined
  ```

  - ?.[] key 접근

  ```
  let user1 = {
    firstName: "Violet"
  };

  let user2 = null; // user2는 권한이 없는 사용자라고 가정해봅시다.

  let key = "firstName";

  alert( user1?.[key] ); // Violet
  alert( user2?.[key] ); // undefined

  alert( user1?.[key]?.something?.not?.existing); // undefined
  ```

- globalThis
  - globalThis는 환경에 관계없이 전역객체를 통일된 방법으로 참조할 수 있는 방법이다.
  - 기존에는 브라우저에서의 전역(window)과 노드에서의 전역(global)이 달랐는데 이를 통일한 것으로 보면 된다.
  ```
  // browser environment
  console.log(globalThis);    // => Window {...}

  // node.js environment
  console.log(globalThis);    // => Object [global] {...}

  // web worker environment
  console.log(globalThis);    // => DedicatedWorkerGlobalScope {...}
  ```
