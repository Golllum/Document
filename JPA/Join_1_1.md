## 일대일(1:1) 단방향 관계

- Model 구조
- ```
  @Entity
  public class Locker {
        @Id
        @GeneratedValue
        private Long id;

        private String name;
  }

  @Entity
  public class Member {
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;

        private String memberName;

        @OneToOne
        @JoinColumn(name = "LOCKER_ID")
        private Locker locker;
  }
  ```

  - 일대일 관계는 양쪽이 서로 하나의 관계만 가지는 관계이다.
  - 일대일 관계에서는 외래키가 어디에 있든 상관이 없다.
  - 위의 코드는 Member를 연관관계 주인으로 설정한 코드이다.

<br><br/>

## 일대일(1:1) 양방향 관계

- Model 구조
- ```
  @Entity
  public class Member {
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;
        private String memberName;

        @OneToOne(mappedBy = "member")
        private Locker locker;
  }

  @Entity
  public class Locker {
        @Id
        @GeneratedValue
        private Long id;

        private String lockerName;

        @OneToOne
        @JoinColumn(name = "MEMBER_ID")
        private Member member;
  }
  ```

  - 일대일 양방향 관계도 다대일 양방향 관계랑 비슷하다.
  - 위 코드는 Locker를 연관관계 주인으로 한 일대일 관계 매핑이다.
  - Member를 연관관계 주인으로 하고 싶다면 mappedBy, @joinColumn위치를 서로 바꿔주면 된다.
