## [ History of Java ]

JDK 1.0a2

- 1995년 5월 23일 발표. 자바 언어 자체가 정식으로 발표된 날
- 이때의 명칭은 Oak

JDK 1.0

- 1996년 1월 23일 발표
- 1.0.2 버전에서 이름이 Java 로 변경

JDK 1.1

- 1997년 2월 19일 발표
- Inner Class
- JavaBeans
  - Java로 작성된 SW Component
  - 기본 생성자가 필요함.
  - 모든 속성은 private
  - getter, setter 구현
  - Serialization을 구현
- RMI (Remote Method Invocation)
  - 분산 애플리케이션 구축에 사용
  - 한 시스템(JVM)에서 사용되는 객체가 다른 시스템(JVM)에서 사용중인 객체에 접근/호출할 수 있도록 함
- Reflection
- Calendar 유니코드 지원

J2SE 1.2

- 1998년 12월 8일 발표
- Swing GUI
- JIT
- Collection Framework

J2SE 1.3

- HotSpot JVM
  - Sun에서 만든 JIT구현
- JNDI
  - WAS 설정파일 (web.xml, server.xml)에 DB 연결 정보 등을 기재
- JPDA (Java Platform Debugger Architecture)
  - Java 코드를 디버깅하기 위한 API 모음집
- JavaSound

J2SE 1.4

- 2002년 2월 6일 발표
- Java Web Start
  - 웹 브라우저에서 한 번의 클릭으로 모든 기능을 갖춘 응용 프로그램을 실행할 수있는 기능을 제공하는 응용 프로그램 배포 기술
- assert Language
- 정규표현식
- XML API

J2SE 1.5 (대규모 release)

- Generics
- Annotation
- AutoBoxing/UnBoxing
- Enumeration
- 가변 길이 파라미터
- static import
- foreach
- scanner class
- Concurrency API

```
1. JDK 1.5 이전에서는 여러 타입을 사용하는 대부분의 클래스나 메소드에서 인수나 반환값으로 Object 타입을 사용했다.

// 1.5 이전, 컬렉션에 기본 타입을 삽입하는 코드
List list = new ArrayList(10);
list.add(new Integer(10)); // AutoBoxing, UnBoxing 지원 X

// 1.5 이후, 컬렉션에 기본 타입을 삽입하는 코드
List<Integer> list = new ArrayList<>();
list.add(10);

2. Generics 가 등장함으로써, 잘못된 타입이 사용될 경우 컴파일 과정에서 제거할 수 있게 되었다. 또한 불필요한 타입 변환이 필요 없다.

// Generics 사용 이전
List list = new ArrayList();
list.add("JungHo");
String name = (String) list.get(0);

// Generics 사용 이후
List<String> list = new ArrayList<>();
list.add("JungHo");
String name = list.get(0);

```

Java SE 6

- 2004년 9월 30일 발표
- 이때 부터 표기가 J2SE 에서 Java SE 로 변경 되었다.
- 가비지 컬렉터 G1(Garbage First) GC 시범 지원
- Java Compiler API
  - 개발자가 손쉽게 compile을 할 수 있는 환경구축
- Pluggable Annotation
  - Lombok 등에서 사용하고 있는 기술
  - 컴파일 단계에서 Annotation에 정의된 일렬의 프로세스를 동작
    - @Getter의 경우, getter 함수를 구현하여 코드에 삽입
  - 컴파일 단계에서 실행되기 때문에, 빌드 단계에서 에러를 출력하게 할 수 있고, 소스코드 및 바이트 코드를 생성할 수 있음

Java SE 7

- 2011년 7월 7일에 발표
- 일반 자원 : 2015년 4월 지원 종료
- 오라클 연장 : 2022년 7월 지원 종료
- 가비지 컬렉터 G1(Garbage First) GC 정식 지원
- JavaFX가 기본으로 포함
- Switch 문에 String 지원
- try-catch-resources
  - 자동으로 리소스를 close() 해주는 기능
- 이진수 리터럴
- 숫자 리터럴에 \_ 형식 지원

Java SE 8 (대규모 release)

- 2014년 3월 18일에 발표
- 일반 자원 : 2019년 1월 지원 종료
- 오라클 연장 : 2030년
- 폐쇄적인 상업 코드 기반의 Oracle JDK, 오픈 소스 기반의 OpenJDK으로 나뉨.
- Lambda Expression
- Stream API
- Optional API
- Functional Programming
- 새로운 날짜와 시간 API(Ex. JodaTime)
- Interface Default Method 추가
- PermGen 영역 삭제

Java SE 9

- 2017년 9월 21일 발표
- 일반 자원 : 2018년 3월 지원 종료
- JShell 추가
  - 인터프리터 언어의 쉘처럼 Java를 사용 가능하도록 지원
- 선행 컴파일 추가
- Modular System (Jigsaw)지원
- Reactive Stream API 추가
- Optional To Stream

Java SE 10

- 2018년 3월 20일 발표
- 일반 자원 : 2018년 9월 지원 종료
- var 키워드를 이용한 지역 변수 타입 추론
- Stop-The-World를 개별 Thread로 분리 (병렬 처리 GC)
  > 기존에는 Stop-The-World 가 발생하면 GC 를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춘다. GC 작업을 완료한 이후에야 중단했던 작업을 다시 시작한다. GC의 병렬처리 기능을 추가하여 해당 동작을 개별 쓰레드로 분리하여 처리. Stop-The-World 시간 개선
- JVM 힙 영역을 시스템 메모리가 아닌 다른 종류의 메모리에도 할당할 수 있도록 지원
- JDK에서 루트 인증 기관(CA) 인증서의 기본 세트를 제공 (https)
- Enhanced for Loop 를 위한 바이트코드 생성

Java SE 11

- 2018년 9월 25일 발표
- 이클립스 재단으로 넘어간 Java EE가 JDK 에서 삭제되고, JavaFX 도 JDK 에서 분리되어 별도의 모듈로 제공
- Java SE 11 부터 Oracle JDK 의 독점 기능이 오픈 소스 버전인 OpenJDK 에 이식됨
  > Oracle JDK 와 OpenJDK가 완전히 동일해진다는 뜻이다.  
  > 2019년 1월부터 오라클이 제공하는 모든 Oracle JDK는 유료화되며, 구독권을 구입하지 않으면 Oracle JDK에 접근 자체가 금지된다. 따라서, OpenJDK 를 기반으로 한 다른 서드파티 JDK 가 대안으로 떠오르고 있다.  
  > Ex. Zulu JDK, AdoptOpenJDK 등이 있다.
- hotspot/jvmti 기능 추가

Java SE 12

- 2019년 3월 19일 발표
- Switch 문법 확장
- ```
  // 예전 Switch 문법
  switch (day) {
    case MONDAY:
    case FRIDAY:
    case SUNDAY:
        System.out.println(6);
        break;
    case TUESDAY:
        System.out.println(7);
        break;
    case THURSDAY:
    case SATURDAY:
        System.out.println(8);
        break;
    case WEDNESDAY:
        System.out.println(9);
        break;
  }

  // 확장 Switch 문법
  // 1. -> 표현 가능
  // 2. 반환값을 넘겨줌
  switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> System.out.println(6);
    case TUESDAY                -> System.out.println(7);
    case THURSDAY, SATURDAY     -> System.out.println(8);
    case WEDNESDAY              -> System.out.println(9);
  }


  System.out.println(
    switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> 6;
    case TUESDAY                -> 7;
    case THURSDAY, SATURDAY     -> 8;
    case WEDNESDAY              -> 9;
  });

  int cnt = switch(day) {
    case MONDAY, FRIDAY, SUNDAY -> 6;
    case TUESDAY                -> 7;
    case THURSDAY, SATURDAY     -> 8;
    case WEDNESDAY              -> 9;
  };

  ```

Java SE 13

- 2019년 9월 17일 발표
- Switch 문 내에서만 사용하는 yield 예약어 추가
- ```
  int cnt = switch (day) {
    case MONDAY -> 0;
    case TUESDAY -> 1;
    case WEDNESDAY -> {
        int k = day.toString().length();
        int result = k+5;
  	    yield result;   //return과 같은 기능
    }
    default -> 0;
  };
  ```
- yield 예약어는 변수명으로 사용할 수 있다. (Switch문 내에서만 예약어임)

Java SE 14

- 2020년 3월 18일 발표
- record 라는 데이터 오브젝트 선언 기능이 추가

Java SE 15

- 2020년 9월 15일 발표
- sealed class(봉인 클래스)가 추가

Java SE 16

- OpenJDK 의 버전 관리가 Mercurial 에서 Git으로 변경
- GitHub 에서 OpenJDK 소스를 볼 수 있음

JAva SE 17

- 2021년 9월 15일 발표
- 의사난수 생성기 API 정식 추가
  - 예측하기 어려운 난수를 생성하는 API
- Java Applet Deprecate 처리
