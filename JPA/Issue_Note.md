## JPA's N+1 문제

- JPA를 활용한 Join 시 발생하는 N + 1 문제에 대해 설명한다.
- N + 1 문제란, @ManyToOne, @OneToMany 어노테이션의 속성인 fetch의 값이 FetchType.LAZY로 설정된 경우에 발생하는 이슈이다. 지연로딩으로 Fetch 속성 값이 설정된 경우, 쿼리를 1번만 실행했는데 연관 Entity 값을 조회하기 위해 조회 결과값의 갯수(N)만큼 쿼리가 또 실행되는 이슈를 말한다. 초기 쿼리에서 사용자가 수만명이 조회가 되었다면 수만명이 각자 가지고 있는 연관 Entity 값들을 조회하기 위해 또 다시 쿼리를 실행시키면서 서비스 과부하가 걸릴 수 있다.

## FetchType의 LAZY와 EAGER

- LAZY
  - 지연로딩
  - 연관관계가 설정된 테이블에 대해 select를 하지 않는다.
  - 1:N 과 같이 여러가지 데이터가 로딩이 일어날 경우 사용하는 방식
- EAGER
  - 즉시로딩
  - 연관관계가 설정된 모든 테이블에 대해 조인이 이루어진다.
  - 1:1 연관관계와 같이 한 건만 존재할 때 사용하는 방식

## N+1 문제 해결

- 즉시 로딩 전략 (fetch = FetchType.EAGER)
  - Entity 조회시점에 Mapping된 연관 Entity를 join 문으로 함께 가져온다.
- JPQL fetch join 사용 (JPQL의 경우 위 방법으로 해결되지 않음)
  - JPQL은 fetch 속성값을 적용하지 않고 SQL문을 생성한다. 따라서 fetch join을 사용하여 join문으로 Mapping된 연관 Entity를 가져오도록 해야한다.
  - fetch join은 inner join을 통해 연관 Entity 값을 조회한다.
- @EntityGraph 사용
  - 쿼리를 실행하는 메소드에 @EntityGraph를 명시하면, fetch join과 동일하게 1번 쿼리를 조회할 때 join으로 연관 Entity 값들도 조회해온다.
  - @EntityGraph은 left outer join으로 동작한다.
- @BatchSize 사용
  - Mapping된 연관 Entity를 지정한 size 만큼 SQL의 IN 절을 사용해서 가져온다.
- @Fetch(FetchMode.SUBSELECT) 사용
  - Mapping된 연관 Entity를 SQL의 IN 절을 사용해서 가져온다.

## @OneToOne 매핑의 LAZY 전략

- 단방향 매핑의 LAZY 전략은 제대로 동작한다. 연관관계의 주인 객체를 통한 LAZY 전략이 실행되기 때문이다.
- 양방향 매핑의 LAZY 전략은 절반만 동작한다. 연관관계의 주인 객체를 통한 LAZY 전략은 정상동작하지만 주인이 아닌 객체를 통한 LAZY 전략은 동작하지 않는다.
- 기본적으로 프록시 객체는 null을 감쌀 수 없다. 따라서 지연로딩은 프록시 객체 생성이 가능한지 여부를 알기 위해 자신을 참조하는 주인 객체가 null인지 아닌지를 조회해야하므로 즉시로딩으로 동작할 수 밖에 없는 이슈이다.
- 해결방법
- 구조 변경하기
  - 양방향 매핑이 반드시 필요한 상황인지 다시한번 생각해본다.
  - OneToOne -> OneToMany 또는 ManyToOne 관계로 변경이 가능한지 생각해본다.
- 구조를 유지한채 해결하기
  - CART를 조회할때 USER도 함께 조회한다. (Fetch Join)
  - batch fetch size를 사용한다.

## JPA 성능 문제 개선

- Entity가 영속성 컨텍스트에 의해 관리되면 차캐시, 변경감지, 지연로딩 등의 이점도 많지만, 스냅샷 저장, 변경감지 수행 등 서비스가 무거워지는 이슈도 발생할 수 있다.
- 메모리를 과도하게 사용하여 로직 수행시 GC가 함께 동작하여 성능이 느려질 수도 있다.
- Entity 단발성 조회의 경우, 읽기 전용으로 메모리를 할당하여 성능 개선이 가능하다.
- 읽기 전용 쿼리
- 스칼라 타입으로 조회
  > select o.id, o.name, o.price from Order o
- 읽기 전용 트랜잭션 사용
  > @Transactional(readOnly=true)
  > Hibernate session flush 모드가 MANUAL로 설정되어 Tranaction commit 시에 자동 flush()가 발생하지 않는다.
  > flush()가 호출되지 않으니 스냅샷 비교 등 무거운 로직을 수행하지 않는다.
- 읽기 전용 쿼리 힌트 사용
  > query hint를 readOnly=true로 설정
  > Entity를 읽기 전용으로 설정하여 스냅샷을 보관하지 않음
- Tranaction 밖에서 읽기
  > @Transactional(propagation = Propagation.NOT_SUPPORTED)
  > 메소드 실행시 Tranaction을 생성하지 않는다.
  > Tranaction이 없으므로 flush()도 없다.

## @ManyToMany 어노테이션 한계

- @ManyToMany를 사용하면 중간 연결 테이블을 자동으로 관리하고 생성해주므로 편리하다. 하지만 일반적으로 실무에서는 연결 테이블에 외래키가 담지 않고 추가적인 컬럼이 들어간다. 추가적인 컬럼이 들어갈 경우 @ManyToMany는 더이상 사용할 수 없다.
- 직접 새로운 연결 엔티티를 만들어서 일대다 다대일 관계를 직접 만들어줘야한다.
