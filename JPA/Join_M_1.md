## 다대일(M:1) 단방향 관계

- Model 구조
- ```
  @Entity
  public class Member {
        @Id
        @GeneratedValue
        private Long id;

        private String MemberName;

        @ManyToOne
        @JoinColumn(name="TEAM_ID")
        private Team team;
  }

  @Entity
  public class Team {
        @Id
        @GeneratedValue
        private Long id;

        private String teamName;
  }
  ```

- Data 입출력 구현
- ```
  public class TestService {
        private final EntityManager em;

        @Transactional
        public void test() {
            Team team = new Team();
            team.setTeamName("test");
            em.persist(team);

            Member member = new Member();
            member.setMemberName("memberTest");
            //member객체에 team객체를 넣어 관계를 맺는다
            member.setTeam(team);
            em.persist(member);
        }
  }

  public void findTest() {
        Member member = em.find(Member.class, 2L);
        log.info(member.getMemberName());
        log.info(member.getTeam().getTeamName());
  }

  >> console 출력
        TEST : memberTest
        TEST : test
  ```

  - 위 예제는 Member 객체를 찾아 Member가 속한 Team까지 연관관계로 인해 데이터를 가져온다. 하지만 Team을 find했을 때는 단방향 관계로 인해 Member를 찾을 수가 없다.

<br><br/>

## 디대일(M:1) 양방향 관계

- Model 구조
- ```
  @Entity
  public class Team {
        @Id
        @GeneratedValue
        private Long id;

        private String teamName;

        //양방향 매핑을 위해 추가
        @OneToMany(mappedBy = "team")
        private List<Member> members = new ArrayList<>();
  }

  @Entity
  public class Member {
        @Id
        @GeneratedValue
        private Long id;

        private String MemberName;

        @ManyToOne
        @JoinColumn(name="TEAM_ID")
        private Team team;
  }
  ```

  - 위의 코드를 보면 Team에 Member를 저장할 필드가 생성된 것을 볼 수 있고, @OneToMany 어노테이션이 사용됐다. 그리고 속성으로 mappedBy가 사용되었는데 mapppedBy는 양방향 매핑일 때 사용한다.
  - name 속성에는 반대쪽 매핑의 필드 이름값을 넣는다. 위 코드상에서는 Member의 Team객체의 team을 입력한다.
  - 그렇다면 mappedBy는 왜 필요할까? 객체는 서로 다른 단방향 2개로 이루어져 있는 것과 연관이 있다.
  - 양방향 관계를 관리하기 위해서는 2개의 연관관계 ID가 필요하게 된다. 즉, 외래키 2개를 관리하게 될텐데 관계형 데이터베이스는 외래키 1개를 가지고 관리한다.그래서 JPA는 두개의 연관관계중 하나를 고르게 하기 위해 mappedBy를 설정한다. 여기서 관리되는 연관관계를 연관관계의 주인이라 한다. 다시 말해 mappedBy가 없는 엔티티가 연관관계의 주인이다. **위의 코드에서도 mappedBy가 없는 Member 엔티티에 외래키가 생성된다.**

- Data 입출력 구현
- (1) 연관 관계 주인 객체에만 연관 관계 Entity 입력 (정상 동작)
- ```
  public class TestService {
        private final EntityManager em;

        @Transactional
        public void test() {
            Team team = new Team();
            team.setTeamName("test");
            em.persist(team);

            Member member = new Member();
            member.setMemberName("memberTest");
            member.setTeam(team);
            em.persist(member);
        }
  }
  ```

  - 단방향인 경우과 코드가 동일한 이유는 연관 관계 주인 방향에서 데이터를 입력하면 연관관계 주인이 아닌(Team)에 Member 데이터를 넣지 않아도 데이터베이스에는 정상적으로 들어간다.

- (2) 연관 관계 주인이 아닌 객체에만 연관 관계 Entity 입력 (비정상 동작)
- ```
  public class TestService {
        private final EntityManager em;

        @Transactional
        public void test() {
            Team team = new Team();
            team.setTeamName("test");
            em.persist(team);

            Member member = new Member();
            member.setMemberName("memberTest");
            //관계주인인 member에는 team을 설정하지 않음
            //member.setTeam(team);

            //관계주인이 아닌 team에 member를 추가
            team.getMembers().add(member);
            em.persist(member);
        }
  }
  ```

  - 위와 같이 연관관계 주인이 아닌 곳에만 데이터를 넣었을 경우에는 정상적으로 데이터가 삽입되지 않는다.
  - Member 테이블의 TEAM_ID(외래키) 컬럼에 null이 들어간다.

- 혹시 모를 에러를 방지하기 위해 양쪽 객체 모두 연관 관계 Entity 값을 입력해야한다.

<br><br/>

## 문제 해결

아래는 버그가 발생하고 있는 코드이다.

```
public class TestService {
    private final EntityManager em;

    @Transactional
    public void test() {
        //team1 생성
        Team team1 = new Team();
        team1.setTeamName("test");
        em.persist(team1);

        //member 생성
        Member member = new Member();
        member.setMemberName("memberTest");

        //member와 team1 양방향 설정
        member.setTeam(team1);
        team.getMembers().add(member);

        //team2 생성
        Team team2 = new Team();
        team2.setTeamName("test2");
        em.persist(team2);

        //member의 팀을 team2로 양방향 변경
        member.setTeam(team2);
        team2.getMembers().add(member);
        em.persist(member);
    }
}
```

- 문제 파악
  - 초기에 member와 team이 양방향 관계로 설정되었으나 member가 team2와 양방향 관계를 다시 설정한 상태가 되어 team은 member를 바라보지만 member는 team을 바라보지 않는 형태가 되버림.
  - member는 team2에 속해있는데 team1에도 member가 들어있는 버그가 발생한다. 실제로 team1.getMembers()로 member 객체를 가져올 수 있다.
- 해결 방법
  - 연관관계가 변경되면 기존 연관관계도 수정을 해줘야한다. 위의 경우 team1에서 member를 제거해주어야 한다.
  - team1.getMembers().remove(); 코드를 추가하여 해결할 수 있다.
