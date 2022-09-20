## 연산자 문법 정리

- 지수 연산자
  - 곱셈 기호를 두번쓰면 제곱으로 처리
  ```
  2**10 // 1024
  ```
- Numeric separators
  - 숫자의 가독성을 높일 수 있게 언더바(\_)로 단위를 구분
  - 구분자는 임의의 위치에 맘대로 삽입 가능
  ```
  console.log(1_000_000_000 + 10_000); // 1000010000
  console.log(1_00_00_00 + 10_0); // 1000100
  ```
- Shorthand property names

  - 프로퍼티 이름과 value값의 변수이름과 동일할때는 하나로 생략 가능

  ```
  const ellie1 = {
      name: 'Ellie',
      age: '18',
  };
  const name = 'Ellie';
  const age = '18';

  const ellie3 = {
      name,
      age,
  };
  ```

  ```
  let room = {
      number: 23,
      name: "hotel",
      toJSON() {
          return 9999;
      }
  };

  let meetup = {
      room,
      title: "Conference"
  };
  ```

- Destructuring Assignment

  - 객체, 배열안의 원소값들을 바깥 변수로 한번에 빼서 사용하기 위한 기법

  ```
  // object
  const student = {
      name: 'Anna',
      level: 1,
  };

  // 속성값과 변수 이름을 일치시켜 사용
  const { name, level } = student;
  console.log(name, level); // Anna 1

  // 변수 이름 새로 설정
  const { name: studentName, level: studentLevel } = student;
  console.log(studentName, studentLevel); // Anna 1
  ```

  ```
  // array
  const animals = ['Dog', 'Cat'];

  const [first, second] = animals;
  console.log(first, second); // Dog Cat
  ```

- Multi-line strings

  - 템플릿 리터럴을 사용하면 여러 개행 줄의 문자열도 나눠서 작성할 필요가 없이 한번에 작성 가능

  ```
  console.log("string text line 1\n" + "string text line 2");

  //템플릿 리터럴
  console.log(`string text line 1
  string text line 2`);
  ```

- Tagged Template Literal

  - 함수의 실행을 템플릿 리터럴로 구현
  - $와 중괄호{}를 사용하여 표현식을 표기할 수 있습니다.

  ```
  `string text` // 문자열 표현
  `string text line 1
  string text line 2` // 개행된 문자열 표현

  var expression;
  `string text ${expression} string text` // 변수값 문자열 조합

  function tag() { };
  tag `string text ${expression} string text` // 함수 호출 argument
  ```

  ```
  // ASIS 문법
  var a = 20;
  var b = 8;
  var c = "자바스크립트";
  var str = "저는 " + (a + b) + "살이고 " + c + "를 좋아합니다.";
  console.log(str);   //저는 28살이고 자바스크립트를 좋아합니다.

  // TOBE 문법
  let a = 20;
  let b = 8;
  let c = "자바스크립트";
  let str = `저는 ${a+b}살이고 ${c}를 좋아합니다.`;
  console.log(str);   //저는 28살이고 자바스크립트를 좋아합니다.
  ```

  ```
  let person = 'Lee';
  let age = 28;

  let tag = function(strings, personExp, ageExp) {
    console.log(strings); // 첫 인수는 배열이 들어오고
    console.log(personExp); // 나머지 인수는 ${person}값이 들어온다.
    console.log(ageExp); // 나머지 인수는 ${age}값이 들어온다.
  };

  let output = tag`that ${person} is a ${age}`;

  > strings : arr(3) ['that ', ' is a ', '']
  > persionExp : Lee
  > age : 28
  ```

  ```
  const ramenList = [
      {
          brand: '농심',
          items: ['신라면','짜파게티','참치마요','둥지냉면']
      },
      {
          brand: '삼양',
          items: ['삼양라면', '불닭볶음면']
      },
      {
          brand: '오뚜기',
          itmes: []
      }
  ];

  function fn(strings, brand, items) {
      if(undefined === items) {
          return brand + "의 라면은 재고가 없습니다!";
      } else {
          return strings[0] + brand + strings[1] + items;
      }
  }

  console.log(`구매가능한 ${ramenList[0].brand}의 라면 : ${ramenList[0].items}`);
  console.log(`구매가능한 ${ramenList[1].brand}의 라면 : ${ramenList[1].items}`);
  console.log(`구매가능한 ${ramenList[2].brand}의 라면 : ${ramenList[2].items}`);

  > 구매가능한 농심의 라면 : 신라면,짜파게티,참치마요,둥지냉면
  > 구매가능한 삼양의 라면 : 삼양라면,불닭볶음면
  > 구매가능한 오뚜기의 라면 : undefined

  console.log(fn`구매가능한 ${ramenList[0].brand}의 라면 : ${ramenList[0].items}`);
  console.log(fn`구매가능한 ${ramenList[1].brand}의 라면 : ${ramenList[1].items}`);
  console.log(fn`구매가능한 ${ramenList[2].brand}의 라면 : ${ramenList[2].items}`);

  > 구매가능한 농심의 라면 : 신라면,짜파게티,참치마요,둥지냉면
  > 구매가능한 삼양의 라면 : 삼양라면,불닭볶음면
  > 오뚜기의 라면은 재고가 없습니다!

  ```

- Spread Syntax

  - 전개연산자
  - 객체나 배열의 안의 요소들을 펼쳐 복사에 이용. 자기 자신 객체, 배열은 영향 안받음
  - 함수의 아규먼트에 쓰이면, 나머지 연산자로 작용. 나머지 인자값들을 모아 배열로 생성

  ```
  const obj1 = { key: 'key1' };
  const obj2 = { key: 'key2' };
  const array = [obj1, obj2];

  // array copy
  const arrayCopy = [...array];
  console.log(arrayCopy);
  > [ { key: 'key1' }, { key: 'key2' } ]

  const arrayCopy2 = [...array, { key: 'key3' }];
  obj1.key = 'newKey';
  console.log(array);
  console.log(arrayCopy2);
  > [ { key: 'newKey' }, { key: 'key2' } ]
  > [ { key: 'newKey' }, { key: 'key2' }, { key: 'key3' } ]

  // object copy
  const obj3 = { ...obj1 };
  console.log(obj3);
  > { key: 'newKey' }

  // array concatenation
  const fruits1 = ['apple', 'strawberry'];
  const fruits2 = ['banana', 'kiwi'];
  const fruits = [...fruits1, ...fruits2];
  console.log(fruits);
  > [ 'apple', 'strawberry', 'banana', 'kiwi' ]

  // object merge
  const dog1 = { dog: 'dog1' };
  const dog2 = { dog: 'dog2' };
  const dog = { ...dog1, ...dog2 };
  console.log(dog);
  > { dog: 'dog2' }
  ```

  ```
  const str = 'hello';

  const arr = [...str];

  console.log(Array.isArray(arr));
  console.log(arr);
  > true
  > [ 'h', 'e', 'l', 'l', 'o' ]
  ```

- Short circuit

  - 단축 평가
  - and연산자와 or연산자 특성을 이용해 반환값을 결정하는 기법
  - Falsy : undefined, null, 0, '', NaN
  - || 연산자

    - 왼쪽 값이 Truthy 하면 왼쪽 값을 리턴한다.
    - 왼쪽 값이 Falsy 하면 오른쪽 값을 리턴한다.

    ```
    // || 연산자

    const seaFood = {
        name: "박달대게"
    };

    function getName(fish) {
        return fish || '이름없음' // 만약 fish가 null, undefiend, 빈값, false 라면  '이름없음'을 리턴
    }

    const name = getName(seaFood)
    console.log(name)
    > {name : 박달대게}

    const name2 = getName()
    console.log(name2)
    > '이름없음'

    ------------------------------------------------------------------------------------------------

    console.log(false || 'hello')   // 'hello'
    console.log('' || 'hello')      // 'hello'

    console.log('트루' || 'hello')  // '트루'
    console.log(1 || 'hello')       // 1

    console.log('hello1' || false)  // 'hello1'
    console.log('hello2' || NaN)    // 'hello2'

    console.log(null && false)      // false
    console.log(undefined || null)  // null
    ```

  - && 연산자

    - 왼쪽 값이 Truthy 하면 오른쪽 값이 리턴된다. 만일 오른쪽 값이 없으면 undefined나 null
    - 왼쪽 값이 Falsy 면 왼쪽 값이 리턴된다.

    ```
    // && 연산자 :

    const seaFood = {
        name: "킹크랩"
    }

    function getName(fish) {
        return fish && fish.name // 만약 fish가 참이면, 우측값을 리턴한다.
    }

    const name = getName(seaFood);
    console.log(name);
    > '킹크랩'

    ------------------------------------------------------------------------------------------------

    console.log(true && "hello"); // 'hello'
    console.log(null && undefined); // null
    console.log(undefined && "hello"); // undefined
    console.log("hello" && null); // null
    console.log("hello" && "bye"); // bye
    console.log(null && "hello"); // null
    console.log(undefined && "hello"); // undefined
    ```

- Nullish Coalescing Operator

  - ?? 연산자
  - 값의 유무를 판단

  ```
  var named = 'Ellie';
  var userName = named || 'Guest';
  console.log(userName); // Ellie

  var named = null;
  var userName = named || 'Guest';
  console.log(userName); // Guest

  // 논리값으로 판단
  var named = '';
  var userName = named || 'Guest'; // 논리값은 빈값도 false로 판단
  console.log(userName); // Guest

  var num = 0;
  var message = num || 'Hello'; // 논리값은 0은 false로 판단
  console.log(message); // Hello

  // 값의 유무로 판단
  var named = '';
  var userName = named ?? 'Guest'; // 그냥 심플하게 값이 있고 없고로 판단. 빈칸도 결국 값이 빈칸인 것이다.
  console.log(userName); // ''

  var num = 0;
  var message = num ?? 'Hello'; // 0도 결국 값이 0인것
  console.log(message); // 0

  -------------------------------------------------------------------------------------------------------

  let a = null ?? 'hello';
  let b = '' ?? true;
  let c = false ?? true;
  let d = 0 ?? 1;
  let e = undefined ?? 'world';

  console.log(a); // 'hello'
  console.log(b); // ''
  console.log(c); // false
  console.log(d); // 0
  console.log(e); // 'world'
  ```

- Logical Operators and Assignment Expressions

  - &&=, ||= 연산자
  - 위의 Short circuit 단축평가 ||, && 의 연산자의 += \*= 같은 버젼

  ```
  let oldName = 'oldPerson';
  let newName = 'newPerson';

  // if문을 통한 값 대입
  if(oldName) {
      oldName = newName;
  }

  // && 연산자를 활용한 값 대입
  oldName && (oldName = newName);

  // Logical Operators and Assignment Expressions (&&) 를 통한 값 대입
  oldName &&= newName

  // && 연산자를 활용한 값 대입
  oldName || (oldName = newName);

  // Logical Operators and Assignment Expressions (||) 를 통한 값 대입
  oldName ||= newName
  ```

- Logical nullish assignment

  - ??= 연산자
  - x ??= y 에서 x가 null 이나 undefined 일 경우 y를 대입

  ```
  const a = { duration: 50 };

  // a.duration = a.duration ?? 10; 의 단축 버전
  a.duration ??= 10; // a의 속성에 duration 속성이 있으니 10은 무시
  console.log(a.duration); // expected output: 50

  a.speed ??= 25; // a의 속성에 speed 라는 키가 없으니 25가 들어감
  console.log(a.speed); // expected output: 25
  ```
