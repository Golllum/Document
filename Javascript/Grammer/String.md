## 문자열 문법 정리

- String.prototype.replaceAll()
  - 일치하는 모든 문자열을 replace
- String padding
  - 문자열 끝 부분이나 시작 부분을 다른 문자열로 채워 주어진 길이를 만족하는 새로운 문자열을 만들어낼 수 있다.
  ```
  "hello".padStart(6); // " hello"
  "hello".padEnd(6); // "hello "
  "hello".padStart(3); // "hello" // 문자열 길이보다 목표 문자열 길이가 짧다면 채워넣지 않고 그대로 반환
  "hello".padEnd(20, "*"); // "hello***************" // 사용자가 지정한 값으로 채우는 것도 가능
  ```
- String.prototype.trimStart / trimEnd
  - 빈공간을 제거하는 trim을 좀더 세부화
  ```
  // trimStart()
  'Testing'.trimStart() //'Testing'
  ' Testing'.trimStart() //'Testing'
  ' Testing '.trimStart() //'Testing '
  'Testing '.trimStart() //'Testing '

  // trimEnd()
  'Testing'.trimEnd() //'Testing'
  ' Testing'.trimEnd() //' Testing'
  ' Testing '.trimEnd() //' Testing'
  'Testing '.trimEnd() //'Testing'
  ```
