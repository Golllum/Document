### 클래스 문법 정리

- Class Field Declarations

  - 처음에 클래스 인스턴스를 정의하기 위해선, 자바 같이 그냥 변수 선언으로 하면 에러가 나고 무조건 생성자(constructor) 내에서만 this를 통해 클래스 필드를 선언해야 했지만, 이제는 바로 선언이 가능해 졌다.

  ```
  class Hello {
      fields = 0;
      title;
  }
  ```

- static 키워드

  - static 키워드를 사용하여 정적 클래스 필드와 개인 정적 메서드를 제공

  ```
  class Hello {
      name = 'world';
      static title = 'here';
      static get title() { return title; }
  }

  new Hello().name // 'world'
  Hello.title // 'here'
  ```

- private 키워드

  - 자바의 private 기능을 추가
  - 메서드와 필드명 앞에 "#"을 붙여서 프라이빗 메서드와 필드 정의가 가능.
  - "#"이 붙은 메서드와 필드는 프라이빗으로 동작하면 클래스 외부에서 접근이 되지 않는다.

  ```
  class ClassWithPrivateField {
      #privateField;

      constructor() {
          this.#privateField = 42;
      }
  }

  class SubClass extends ClassWithPrivateField {
      #subPrivateField;

      constructor() {
          super();
          this.#subPrivateField = 23;
      }
  }

  new SubClass(); // SubClass {#privateField: 42, #subPrivateField: 23}

  --------------------------------------------------------------------------------------------------------

  class myClass {
      #privMethod(){
          return "프라이빗 메서드";
      }
      publicMethod(){
          return "퍼블릭 메서드";
      }
  }

  let newClass = new myClass();
  console.log(newClass.privMethod()); // ERROR
  ```

- Ergonomic Brand Checks for Private Fields
  - private 속성/메소드를 체크
  - public 필드에 대해, 클래스의 존재하지 않는 필드에 접근을 시도하면 undefined가 반환되는 반면에, private 필드는 undefined대신 예외를 발생시키게 된다.
  - 따라서 in 키워드를 사용해 private 속성/메소드를 체크할 수 있다.
  ```
  class VeryPrivate {
      constructor() {
          super()
      }

      #variable
      #method() {}
      get #getter() {}
      set #setter(text) {
          this.#variable = text
      }

      static isPrivate(obj) {
          return (
              #variable in obj && #method in obj && #getter in obj && #setter in obj
          )
      }
  }
  ```
