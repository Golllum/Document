## 배열 문법 정리

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
