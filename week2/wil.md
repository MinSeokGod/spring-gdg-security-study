## 세션 방식 인증에 대한 내용을 요약
- 사용자는 세션 ID를 가지고 있다.
- 세션 저장소에 사용자의 ID가 저장되어 있다.
  - 인가 여부 확인
  - 접근 허용 또는 거부
- 참고로 서버가 사용자의 상태를 저장한다는 뜻으로 "Stateful" 하다고 한다.
- 모든 SecurityFilterChain 간에 동일한 http 설정이 공유되지 않도록 prototype scope 빈으로 HttpSecurity를 생성한다.

- 로그인 플로우 (우리가 구현해야 하는 목표)
  - 로그인 요청을 authToken으로 변환
    - 여기서 Token은 AuthenticationManager가 다룰 수 있는 객체를 의미한다.
  - AuthenticationManager가 인증 시도
  - 정보를 저장
    - SecurityContext가 담당
  - 세션 생성 및 JSESSIONID를 발급하고 저장

## 왜 MemberRole의 value로 ROLE_ 접두사를 붙이는지
- Spring Security의 hasRole() 메서드는 내부적으로 전달된 권한 문자열 앞에 ROLE_ 이라는 접두사가 붙어있다고 가정하고 검사를 수행
  - EX) hasRole("ADMIN")이라고 코드를 작성하면, Spring Security는 실제로 ROLE_ADMIN이라는 문자열을 찾음.
- 명시적 약속 (권한과 역할의 구분) NOT Authority, Role
  - Role 없이 정의된다면 "권한"으로 취급된다.