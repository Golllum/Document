## [ StreamAPI ]

함수형 프로그래밍 vs 객체지향 프로그래밍

- https://mangkyu.tistory.com/111

Stream API

- Java는 객체지향 언어이기 때문에 기본적으로 함수형 프로그래밍이 불가능하다.
- JDK8부터 Stream API와 람다식, 함수형 인터페이스 등을 지원하면서 Java를 이용해 함수형으로 프로그래밍할 수 있는 API 들을 제공해주고 있다. 그 중 하나가 Stream API이다.
- Stream API는 데이터를 추상화하고, 처리하는데 자주 사용되는 함수들을 정의해두었다. 여기서 데이터를 추상화하였다는 것은 데이터의 종류에 상관 없이 같은 방식으로 데이터를 처리할 수 있다는 것을 의미하며, 그에 따라 재사용성을 높일 수 있다.

  ```
  // Stream 사용 전
  String[] nameArr = {"IronMan", "Captain", "Hulk", "Thor"}
  List<String> nameList = Arrays.asList(nameArr);

  // 원본의 데이터가 직접 정렬됨
  Arrays.sort(nameArr);
  Collections.sort(nameList);

  for (String str: nameArr) {
  System.out.println(str);
  }

  for (String str : nameList) {
  System.out.println(str);
  }
  ```

  ```
  // Stream 사용 후
  String[] nameArr = {"IronMan", "Captain", "Hulk", "Thor"}
  List<String> nameList = Arrays.asList(nameArr);

  // 원본의 데이터가 아닌 별도의 Stream을 생성함
  Stream<String> nameStream = nameList.stream();
  Stream<String> arrayStream = Arrays.stream(nameArr);

  // 복사된 데이터를 정렬하여 출력함
  nameStream.sorted().forEach(System.out::println);
  arrayStream.sorted().forEach(System.out::println);

  // 스트림이 이미 사용되어 닫혔으므로 에러 발생
    int count = userStream.count();

  // IllegalStateException 발생
  java.lang.IllegalStateException: stream has already been operated upon or closed
    at java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:229)
    at java.util.stream.ReferencePipeline.noneMatch(ReferencePipeline.java:459)
  ```

- Stream API 특징

  - 원본의 데이터를 변경하지 않는다.
  - 일회용이다.
  - 내부 반복으로 작업을 처리한다.

  ```
    List<String> myList = Arrays.asList("a1", "a2", "b1", "c2", "c1");

    myList.stream()							// 생성하기
          .filter(s -> s.startsWith("c"))	    // 가공하기
          .map(String::toUpperCase)			// 가공하기
          .sorted()							// 가공하기
          .count();							// 결과만들기
  ```
