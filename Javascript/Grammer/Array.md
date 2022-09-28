## 배열 문법 정리

- Array in JS
  - 자바스크립트 배열은 해시 테이블로 구현된 객체이므로 인덱스로 배열 요소에 접근하는 경우, 일반적인 배열보다 성능적인 면에서 느릴 수 밖에 없는 구조적인 단점을 갖는다. 하지만 특정 요소를 탐색하거나 요소를 삽입 또는 삭제하는 경우에는 일반적인 배열보다 빠른 성능을 기대할 수 있다.
  - 자바스크립트 배열은 인덱스를 프로퍼티 키로 갖으며 length 프로퍼티를 갖는 특수한 객체이다.
  - 인덱스로 배열 요소에 접근할 때 일반적인 배열보다 느릴 수 밖에 없는 구조적인 단점을 보완하기 위해 대부분의 모던 자바스크립트 엔진은 배열을 일반 객체와 구별하여 보다 배열처럼 동작하도록 최적화하여 구현하였다.
- Array.prototype.every(function(currentValue, index, array), thisValue))

  - 배열의 각 엘리먼트에 대해서 테스트 함수의 반환 값이 모두 true인지 확인
  - 모든 case가 true일때 true를 반환
  - 기존 배열 값은 변경되지 않음

  ```
  var objArr = [{name: '철수', age: 10}, {name: '영희', age: 10}, {name: '바둑이', age: 2}]

  console.log(objArr.every((item)=> item.age>5)); //false
  console.log(objArr.every((item)=> item.age>1)); //true
  ```

- Array.prototype.some()

  - 배열의 각 엘리먼트에 대해서 테스트 함수의 반환 값이 하나라도 true가 있는지 확인
  - 하나라도 true가 발생하면 true를 반환
  - 기존 배열 값은 변경되지 않음

  ```
  var objArr = [{name: '철수', age: 10},{name: '영희', age: 10}, {name: '바둑이', age: 2}]

  console.log(objArr.some((item)=> item.age>5)); //true
  console.log(objArr.some((item)=> item.age>10)); //false
  ```

- Array.prototype.find((element, index, array) => {})

  - 콜백 함수를 만족하는 첫 요소를 반환

- Array.prototype.findIndex((element, index, array) => {})

  - 콜백 함수를 만족하는 첫 인덱스를 반환
  - 해당하는 값이 없으면 -1 반환

- Array.prototype.indexOf(search, fromIndex)

  - 인자로 받은 값에 해당하는 첫 인덱스를 반환
  - 해당하는 값이 없으면 -1 반환

- Array.prototype.slice(Number startIdx, Number endIdx)

  - 인수로 주어진 시작 인덱스부터 종료 인덱스 전까지 추출하여 새 문자열로 반환한다. 단, 인수로 주어진 인덱스가 음수일 때는 뒤에서부터 인덱스를 세어 위치를 찾고 시작 인덱스가 종료 인덱스보다 크다면 ""을 반환한다.
  - 종료 인덱스가 없다면 문자열의 length를 종료 인덱스로 취급한다.

  ```
  var str = "hello";

  console.log(str.slice(0, 3)); //hel
  console.log(str.slice(1, 0)); //""
  console.log(str.slice(0, -2); //hel
  console.log(str.slice(-4, 2); //e
  ```

- Array.prototype.forEach(callback)

  - 일반적인 for문보다 forEach문이 내장함수 이기 때문에 속도가 더 빠르다.
  - Array 적용가능 (ES6+ : Map, Set 적용 가능)

  ```
  // 1차원 배열
  let arr = [1, 2, 3, 4];

  arr.forEach((v, i) => {
    console.log(v); // value
    console.log(i); // index
  });

  ------------------------------------------------------------------------------------
  // 2차원 배열
  let arr = [[1,1], [2,2,2], [3,3,3,3]];

  arr.forEach((arrObj) => {
    arrObj.forEach((v, i) => {
      console.log('${v} ${i}');
    });
  });

  > 1 0
  > 1 1
  > 2 0
  > 2 1
  > 2 2
  > 3 0
  > 3 1
  > 3 2
  > 3 3
  ```

- Array.prototype.map( callback [ , thisArg ] )

  - 주어진 배열의 값들을 오름차순으로 접근해 callback을 통해 새로운 값을 정의하고 신규 배열을 만들어 반환

  ```
  // for문을 이용한 반복문
  const numbers = [1, 2, 3, 4, 5];
  const result = [];

  for (i = 0; i < numbers.length; i++) {
    result.push(numbers[i] * numbers[i]);
  }


  // map메소드를 이용한 반복문
  const numbers = [1, 2, 3, 4, 5];
  const result = numbers.map(number => number * number);

  console.log(numbers);
  // [1, 2, 3, 4, 5];

  console.log(result);
  // [1, 4, 9, 16, 25]
  ```

  ```
  // 프로그래밍 이름 길이 구하기
  const langs = ["javascript", "java", "c#", "c++", "c"];
  const lengthOfLangs = langs.map(language => language.length);

  console.log(lengthOfLangs);
  // [10, 4, 2, 3, 1];
  ```

  - 고차 함수 사용

  ```
  const numbers = [1, 2, 3, 4, 5];

  // 제곱근 구하기
  const squares = numbers.map(Math.sqrt);

  console.log(squares);
  // [1, 1.4142135623730951, 1.7320508075688772, 2, 2.23606797749979]

  // 곱 구하기
  const double = value => value * 2;
  const doubles = numbers.map(double);

  console.log(doubles);
  // [2, 4, 6, 8, 10]
  ```

  - 새로운 형태 값 생성

  ```
  const users = [
    { name: 'YD', age: 22 },
    { name: 'Bill', age: 32 },
    { name: 'Andy', age: 21 },
    { name: 'Roky', age: 35 },
  ];

  const ages = users.map(user => user.age);

  console.log(ages);
  // [22, 32, 21, 35]

  -------------------------------------------------------------------------------------------------------

  const users = [
    { name: 'YD', age: 22 },
    { name: 'Bill', age: 32 },
    { name: 'Andy', age: 21 },
    { name: 'Roky', age: 35 },
  ];

  const newUsers = users.map(user => {
    if (user.name === 'YD') {
        return { ...user, age: 18 };
    }

    return { ...user };
  });

  console.log(newUsers);
  // [{name: "YD", age: 18}, {name: "Bill", age: 32}, {name: "Andy", age: 21}, {name: "Roky", age: 35}]
  ```

  - 문자열 배열로 전환

  ```
  const message = 'Hello world';
  const newMessage = Array.prototype.map.call(message, char => `${char}`);

  console.log(newMessage);
  // ["H", "e", "l", "l", "o", " ", "w", "o", "r", "l", "d"]
  ```

- Array.prototype.flat()

  - 중첩 배열 삭제 / 빈공간 삭제

  ```
  // 중첩 다차원 배열 평평하게
  const array = [1, [2, 3], [4, 5]];
  array.flat(1);
  > 결과 : [1,2,3,4,5]

  // 데이터 정리도 됨
  const entries = ["bob", "sally", , , , , , , , "cindy"];
  entries.flat();
  > 결과 ['bob', 'sally', 'cindy'];

  ['Dog', ['Sheep', 'Wolf']].flat();
  > 결과 [ 'Dog', 'Sheep', 'Wolf' ]

  let arr1 = ["it's Sunny in", "", "California"];
  arr1.map(x=>x.split(" "));
  > 결과 [["it's","Sunny","in"],[""],["California"]]

  arr1.flatMap(x => x.split(" "));
  > 결과 ["it's","Sunny","in", "", "California"]
  ```

- Array.prototype.at()
  - 양수 및 음수 인덱스를 모두 사용하여 문자열을 인덱싱할 수 있다.
  ```
  const arrays = ['a','b','c','d'];
  console.log(arrays.at(-1));
  > 결과 'd'
  ```
