# Spring Security

### 로그인 기능 구현

```java
formLogin(formLogin -> formLogin
                        .loginPage("/loginForm")
                        **.loginProcessingUrl("/login")** //시큐리티가 대신 로그인 진행
                        .usernameParameter("userID")
//                        .usernameParameter("username이 아닌 다른 변수명으로 username을 입력받았을 경우의 변수명 입력, ex) username2")
                        .defaultSuccessUrl("/"));
        return http.build();
```

 "/login" 요청이 오면 자동으로 **스프링 컨테이너에 등록된** UserDetailsService의 loadUserByUsername 함수를 실행하므로 UserDetailsService을 구현한 PrincipalDetailsService를 만들어줬다.

 UserDetailsService에서는 유저가 입력한 로그인 정보를 토대로 객체를 DB에서 조회해와 PrincipalDetails를 이용하여 시큐리티 session의 Authentication에 저장한다. 

```java
@Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userRepository.findByLoginId(username);

        // *** 검증 로직 구현 ***
        if (user != null) {
            // 시큐리티 session의 Authentication에 저장
            return new PrincipalDetails(user);
        }
        return null;
    }
```

 🤔*PrincipalDetails를 이용하여 시큐리티 session의 Authentication에 저장한다구요?*

알다시피 '/login' 요청이 오면 **스프링 시큐리티**가 낚아채서 로그인을 진행시키는데, 로그인 진행이 완료 되면 session을 만들어준다. 이때 security contextHolder(key)에 세션이 저장된다. 해당 세션에 들어갈 수 있는 정보는 Authentication type object (value) 이다.

Authentication 안에는 User 정보가 있고,  User 객체의 타입은 UserDetails 객체 타입이어야한다.

따라서 UserDetails를 구현한 PrincipalDetails class를 만들어 주어야한다.

```java
@RequiredArgsConstructor
public class PrincipalDetails implements UserDetails {

    // 내가 정의해놓은 user 객체 등록
    private final User user;
    
    // 해당 User의 권한을 리턴하는 곳
    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        Collection<GrantedAuthority> collect = new ArrayList<>();
        collect.add((GrantedAuthority) () -> user.getRole().toString());
        System.out.println(user.getRole().toString());
        return collect;
    }

    @Override
    public String getPassword() {
        return user.getPassword();
    }

    @Override
    public String getUsername() {
        return user.getUsername();
    }

    @Override
    public boolean isAccountNonExpired() {
        return true;
    }

    @Override
    public boolean isAccountNonLocked() {
        return true;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }

    // 계정 활성화 여부 체크
    @Override
    public boolean isEnabled() {
        // *** 1년동안 회원이 로그인을 안했을 경우 휴먼 계정 전환 기능 구현 ***
        // 현재시간 - 로그인 시간 >1년 : return false
        //user.getLoginDate();
        return true;
    }
}
```

🤔*private final User user; //Could not autowire. No beans of 'User' type found.*

User가 bean이 아니라고? 분명히 User class에 @Entity를 달아줬는데…에에 라고 생각했다가 ~~ 멍청함을 알아차렸다.

@Entity는 JPA에서 제공하는 어노테이션으로, 해당 객체를 데이터베이스에 매핑하기위한 어노테이션이며 해당 클래스를 JPA가 관리함을 뜻한다.  스프링에 빈으로 등록하는 행위와는 무관하다!

달아주면 스프링에 빈으로 등록되는 어노테이션은 @Component, @Bean, @Repositoy, @Service, @Controller 등이다. 

**또한, 애초에 스프링 빈으로 User 객체를 등록할 필요도 없다**. 스프링 컨테이너에 스프링 빈으로 객체가 등록되면 제공되는 이점을 떠올려보자. 

1. 싱글톤 보장
2.  의존관계 주입을 통한 DIP 원칙과 SRP 원칙, OCP 원칙 준수

Repository와 Controller, Service는 위의 이점들을 이용해먹기 때문에 스프링 빈으로 등록할 필요성이 추웅분히 있다. User 객체는 아니다.


### OAuth 2.0 개념

OAuth (Open Auth) : 인증 처리를 대신해준다.

![Untitled](https://github.com/mungsil/TIL/assets/107127451/1bd6ae0e-e761-48c9-8029-28b6d1e9da2b)


7️⃣번 과정을 통해서 인증을 완료한다.

9️⃣번 과정을 통해서 리소스 서버에 저장된 user데이터에 접근할 인가를 받게된다.

`reference`

[https://www.inflearn.com/course/스프링부트-시큐리티/dashboard](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%EC%8B%9C%ED%81%90%EB%A6%AC%ED%8B%B0/dashboard)

[https://www.youtube.com/watch?v=JBN5dCnLYnY](https://www.youtube.com/watch?v=JBN5dCnLYnY)
