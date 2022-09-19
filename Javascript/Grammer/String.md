## 문자열 문법 정리

- Window.prompt()

  - Window.prompt()는 사용자가 텍스트를 입력할 수 있도록 안내하는 선택적 메세지를 갖고 있는 대화 상자를 띄움.

  ```
  // 빈 대화 상자 호출
  sign = window.prompt();
  sign = prompt();

  // "등록하시겠습니까?" 안내 문구가 입력된 대화 상자 호출
  sign = window.prompt("등록하시겠습니까?");

  // "등록하시겠습니까?" 안내 문구가 입력된 대화 상자의 입력 값이 "네."로 설정된 대화 상자 호출
  sign = window.prompt("등록하시겠습니까", "네.");
  ```

- String.prototype.charAt(Number idx)

  - 문자열의 index번째 문자를 유니코드 단일문자로 반환한다.

- String.prototype.startsWith(String str)

  - 특정 문자열로 시작하는지 확인하여 맞으면 true, 틀리면 false를 반환한다.

- String.prototype.endsWith(String str)

  - 특정 문자열로 끝나는지 확인하여 맞으면 true, 틀리면 false를 반환힌다.

- String.prototype.includes(String str)

  - 특정 문자열을 포함하고 있으면 true, 없으면 false를 반환한다.

- String.prototype.repeat(Number cnt)

  - cnt 횟수만큼 반복하여 문자열을 반환한다.

- String.prototype.replaceAll()

  - 일치하는 모든 문자열을 replace 한다.

- String.prototype.concat(String str)

  - 문자열과 인수로 주어진 문자열을 합쳐서 하나의 문자열로 반환한다

- String.prototype.substr(Number index)

  - substring()과 동일한 기능을 하지만 웹 표준에서 제거될 예정이므로 사용하지 않는 것을 권장

- String.prototype.substring(Number startIndex [, Number endIndex])

  - 인수로 주어진 시작 인덱스부터 종료 인덱스 전까지 문자열을 잘라 반환한다. 단, 인수로 주어진 인덱스가 음수일 때는 0으로 취급하고 시작 인덱스가 종료 인덱스보다 크다면 두 인덱스를 바꿔 취급한다. 종료 인덱스가 없다면 문자열의 length를 종료 인덱스로 취급한다.

  ```
  var str = "hello";

  console.log(str.substring(0, 3)); //hel
  console.log(str.substring(1, 0)); //h
  console.log(str.substring(0, -2); //""
  console.log(str.substring(-4, 2); //he
  ```

- String.prototype.slice(Number startIndex [, Number endIndex])

  - 인수로 주어진 시작 인덱스부터 종료 인덱스 전까지 추출하여 새 문자열로 반환한다. 단, 인수로 주어진 인덱스가 음수일 때는 뒤에서부터 인덱스를 세어 위치를 찾고 시작 인덱스가 종료 인덱스보다 크다면 ""을 반환한다. 종료 인덱스가 없다면 문자열의 length를 종료 인덱스로 취급한다.

  ```
  var str = "hello";

  console.log(str.slice(0, 3)); //hel ※시작 인덱스는 포함, 종료 인덱스는 미포함
  console.log(str.slice(1, 0)); //""
  console.log(str.slice(0, -2); //hel
  console.log(str.slice(-4, 2); //e
  ```

- String.prototype.split(String str)

  - 인수로 주어진 문자열을 기준으로 문자열을 분리하여 배열로 반환한다.

  ```
  var words = "cat car cap";
  console.log(words.split(" "));
  > 결과 ['cat', 'car', 'cap']
  ```

- String.prototype.indexOf(String str)

  - 문자열의 앞에서부터 인수로 주어진 문자열과 일치하는 부분이 있는지 검사하고 일치한다면 일치가 시작되는 인덱스를 반환하고, 일치하는 곳이 없다면 -1을 반환한다.

- String.prototype.lastIndexOf(String str)

  - 문자열의 뒤에서부터 인수로 주어진 문자열과 일치하는 부분이 있는지 검사하고 일치한다면 일치가 시작되는 인덱스를 반환하고, 일치하는 곳이 없다면 -1을 반환한다.

- String.prototype.padStart(Number length, String addStr)

  - 문자열의 뒤에 두번째 인수로 주어진 특정 문자열을 붙혀 첫번째 인수로 주어진 길이인 문자열을 반환한다.

- String.prototype.padEnd(Number length, String addStr)

  - 문자열의 앞에 두번째 인수로 주어진 특정 문자열을 붙혀 첫번째 인수로 주어진 길이인 문자열을 반환한다.

  ```
  /* padEnd() */
  console.log(str.padEnd(8, ".")); //hello...

  /* padStart() */
  console.log(str.padStart(8, "!")); //!!!hello

  /* repeat() */
  console.log(str.repeat(2)); //hellohello
  ```

- String.prototype.trim / trimStart / trimEnd

  - 빈공간을 제거하는 trim을 좀더 세부화

  ```
  /* trim() */
  var spaceStr = " my name is earth "; //앞과 뒤에 공백문자가 두개씩 들어있는 문자열
  console.log(spaceStr.trim()); //'my name is earth'

  /* trimEnd() */
  console.log(spaceStr.trimEnd()); //' my name is earth'

  /* trimStart() */
  console.log(spaceStr.trimStart()); //'my name is earth '
  ```

- String.prototype.toLowerCase / toUpperCase

  - 인수로 주어진 Locale에 따라 문자열을 소문자로 변환하여 반환한다.
  - 인수로 주어진 Locale에 따라 문자열을 대문자로 변환하여 반환한다.

- Template Strings

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
  // ES5 문법
  var a = 20;
  var b = 8;
  var c = "자바스크립트";
  var str = "저는 " + (a + b) + "살이고 " + c + "를 좋아합니다.";
  console.log(str);   //저는 28살이고 자바스크립트를 좋아합니다.

  // ES6 문법
  let a = 20;
  let b = 8;
  let c = "자바스크립트";
  let str = `저는 ${a+b}살이고 ${c}를 좋아합니다.`;
  console.log(str);   //저는 28살이고 자바스크립트를 좋아합니다.
  ```
