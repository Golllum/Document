### 정규식 문법 정리

- named capture group

  - 미리 명명된 정규식 캡쳐 드룹 이름 지정
  - named capturing group: (?\<name>x)
  - non-capturing group: (?:x)

  ```
  const re = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/
  const result = re.exec('2015-01-02')

  // result.groups.year === '2015';
  // result.groups.month === '01';
  // result.groups.day === '02';

  --------------------------------------------------------------------------------------------------
  // 이메일 주소를 정규식을 통해 ID와 도메인을 각각 email_id와 domain이란 이름으로 분리한 obj로 가져오기
  const emailAddress = 'bloodguy@gmail.com';

  const result = /(?<email_id>\w+)@(?<domain>\w+\.\w+)/.exec(emailAddress).groups
  // { email_id: "bloodguy", domain: "gmail.com" }

  // 필요한 게 ID만이라면 :?를 통해 그룹핑만 하고 결과값에서는 제외하는 것도 가능
  const result2 = /(?<email_id>\w+)@(?:\w+\.\w+)/.exec(emailAddress).groups
  // { email_id: "bloodguy" }

  ```

- RegExp lookbehind assertions
  - ?= , ?! , ?<= , ?<!
  - 앞에 오는 항목에 따라 문자열 일치
  ```
  // ?= 특정 하위 문자열이 뒤에 오는 문자열을 일치시키는데 사용
  /Roger(?=Waters)/
  /Roger(?= Waters)/.test('Roger is my dog') //false
  /Roger(?= Waters)/.test('Roger is my dog and Roger Waters is a famous musician') //true

  // ?! 문자열 뒤에 특정 하위 문자열이 오지 않는 경우 일치하는 역 연산을 수행
  /Roger(?!Waters)/
  /Roger(?! Waters)/.test('Roger is my dog') //true
  /Roger(?! Waters)/.test('Roger Waters is a famous musician') //false

  // ?<= 새로 추가된 표현식
  /(?<=Roger) Waters/
  /(?<=Roger) Waters/.test('Pink Waters is my dog') //false
  /(?<=Roger) Waters/.test('Roger is my dog and Roger Waters is a famous musician') //true

  // ?<! 새로 추가된 표현식
  /(?<!Roger) Waters/
  /(?<!Roger) Waters/.test('Pink Waters is my dog') //true
  /(?<!Roger) Waters/.test('Roger is my dog and Roger Waters is a famous musician') //false
  ```
