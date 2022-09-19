## [ Optional API ]

- JAva SE 8 에서 등장한 Optional API는 NPE(Null Pointer Exception)를 해결하기 위해 등장했다.
- Optional<T>는 null이 올 수 있는 값을 감싸는 Wrapper 클래스로, 참조하더라도 NPE가 발생하지 않도록 도와준다.
- ```
  // Java8 이전
  List<String> names = getNames();
  List<String> tempNames = list != null ? list : new ArrayList<>();

  // Java8 이후
  List<String> nameList = Optional.ofNullable(getNames())
                                  .orElseGet(() -> new ArrayList<>());
  ```

- ```
    // Java8 이전
    UserVO userVO = getUser();
    if (userVO != null) {
        Address address = user.getAddress();
        if (address != null) {
            String postCode = address.getPostCode();
            if (postCode != null) {
                return postCode;
            }
        }
    }
    return "우편번호 없음";

    // Java8 이후
    // 위의 코드를 Optional로 펼쳐놓으면 아래와 같다.
    Optional<UserVO> userVO = Optional.ofNullable(getUser());
    Optional<Address> address = userVO.map(UserVO::getAddress);
    Optional<String> postCode = address.map(Address::getPostCode);
    String result = postCode.orElse("우편번호 없음");

    // 그리고 위의 코드를 다음과 같이 축약해서 쓸 수 있다.
    String result = user.map(UserVO::getAddress)
                        .map(Address::getPostCode)
                        .orElse("우편번호 없음");
  ```

  orElse() vs orElseGet()

- null 체크 로직이 필요한 경우, orElse() or orElseGet()을 사용하여 default 값을 넣어줄 수 있다.
- 각 메소드의 선언을 살펴보면 아래와 같다.
- ```
    public T orElse(T other) {
        return value != null ? value : other;
    }

    public T orElseGet(Supplier<? extends T> other) {
        return value != null ? value : other.get();
    }
  ```

- orElse 는 T의 모든 매개 변수를 사용하고 orElseGet은 T 유형의 개체를 반환하는 Supplier 유형의 인터페이스를 사용한다.
  > Supplier 은 함수적 인터페이스로서 get을 호출하여 결과를 리턴하는 역할을 함.
- 두 메소드의 사용 경우는 아래와 같다.
  - 매개변수로 함수를 호출하는 경우,
    - orElse() : Optional 객체의 null 여부와 상관없이 매개변수로 넘겨준 함수가 호출됨.
    - orElseGet() : Optional 객체가 null인 경우에만 매개변수로 넘겨준 함수가 호출됨.
  - 매개변수로 값을 넘겨주는 경우,
    - orElse() & orElseGet() : 동작 방식과 반환값이 동일
- 결론
  - orElseGet() : null일 경우 메소드를 호출해야 하는 경우 사용
  - orElse() : null일 경우 값을 넘겨야 하는 경우 사용
  - 값을 넘기는 경우 orElseGet() 함수를 호출하여 굳이 Supplier 인터페이스로 감싸서 값을 넘겨줄 필요가 없음
