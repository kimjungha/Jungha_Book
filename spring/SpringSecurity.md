# Spring Security 개념

* 스프링 프레임워크에서 보안을 담당하며 인증, 인가를 제공한다. 

* 인증 Authentication : 사용자가 누구인지 확인 
* 인가 Authorization : 인증된 사용자가 특정 리소스에 접근이 가능한가 확인
  * 사용자 역할 role , 권한에 따라 접근 제한 

## 제공하는 기능
    * 다양한 인증 방식 제공 (FORM 기반 로그인, OAuth2.0, JWT)
    * 비밀번호 암호화 
    * 세션관리
    * CSRF (Cross site Request Forgery) 방어
        * 사이트간 요청 위조 : 공격자가 사용자의 세션을 가로채어서 의도치 않은 요청을 서버로 보내는 공격
        * 사용자가 원하지 않는 요청이 정상적인 인증을 통해서 서버에 전달되는것 
        * Html form 형태에선 필요, jwt token 방식 경우 세션을 사용하지 않아서 csrf 공격이 불가능하다 => 즉 jwt 방식에서는 csrf 공격이 불가능하다 
    * CORS (Cross Origin Resource Sharing) 지원
        * 교차 출처 리소스 공유  => 브라우저 보안 정책을 우회하여서 다른 출처의 요청을 허용하는 방법
        * 프론트엔드에서 백엔드 API 호출할때 CORS 정책을 허용해야 한다. 
        * SecurityFilter에 CORS 설정을 추가해야 한다.



