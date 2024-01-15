# Spring Data JPA

> EntityManager.persist(entity);
> 

에서의 persist는 entity를 DB에 저장하는게 아니라 영속성 컨텍스트에 저장하는 것이다.

**엔티티 매니저를 통해서 영속성 컨텍스트에 접근할 수 있다.**

### 💥 빌더패턴 사용 시 주의점
List 타입 필드의 NPE에 주의하자.
NullPointerException 방지를 위해 필드를 아래와 같이 초기화시켜도 문제가 발생하기 때문이다. 아래는 Team class의 코드이다.

    @OneToMany(mappedBy = "team")
    private List<Member> members = new ArrayList<>();
위와 같이 필드 초기화를 시켜도 빌더패턴을 이용하여 객체를 생성하면 NPE가 발생한다.

`해결방법`

    @OneToMany(mappedBy = "team")
    @Builder.Default
    private List<Member> members = new ArrayList<>();
