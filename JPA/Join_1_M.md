## 일대다(1:M) 단방향 관계

- Model 구조
- ```
  @Entity
  public class Team {
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;

        private String teamName;

        @OneToMany
        @JoinColumn(name = "TEAM_ID")
        private List<Member> members = new ArrayList<>();
  }
  ```

- 다대일 관계에서는 @JoinColumn을 둔 엔티티에 외래키가 생성되고 관리한다. 하지만 일대다 단방향 관계에서는 Team 엔티티의 반대편인 Member엔티티에 외래키가 생성되고 관리된다.
- 일반적으로 일대다 단방향 관계 매핑은 권장되지 않는다. 연관관계 주인 엔티티에서 외래키를 관리하지 않고 반대편 엔티티에서 외래키를 관리하기 때문에(데이터베이스 설계에서 1:M관계에서 외래키는 M에 존재하기 때문에) 관리가 부담스럽다.
- 또한 이로 인해 성능 이슈도 발생한다. 예를 들어 Member 객체를 저장한다 해보자.  
  Member 엔티티에는 Team엔티티에 대한 정보가 없다. 즉 Member 객체를 저장하면 INSERT 구문에서 외래키는 저장이 되지 않고 데이터베이스에 들어갈 것이다. Team객체가 저장될 때 Team객체에 있는 연관 관계 정보를 보고 Member객체에 UPDATE구문으로 외래키가 저장될 것이다. 즉 한번 저장하는데 UPDATE도 항상 같이 호출된다. 그러므로 단방향 관계를 할 때는 일대다 보다는 다대일 단방향으로 하는 것이 좋다.

<br><br/>

## 일대다(1:M) 양방향 관계

- 1:M관계의 주인은 항상 다(M)이기 때문에 일대다 양방향이나 다대일 양방향은 같은 말이다.
