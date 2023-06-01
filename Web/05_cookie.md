쿠키에 대해 전반적으로 알지만, 프로젝트를 하면서 프론트엔드가 쿠키에 대해 가져야할 자세가 어떤것인가에 대해 다시 되새겨보고자 궁금했던거 기록!추후 다시 정리하기

<br><br>
<hr></hr>


## Cookie

- 서버에서 Set Cookie 요청
- 브라우저에서 Cookie 저장
- 브라우저에서 서버 요청 시 헤더에 Cookie 포함해서 호출

일단 기본적인 프로세스는 이러하다.
여기서 도메인에 관련하여 정리 하고자 한다.

<br><br>
<hr></hr>

## Cookie Domain

- 도메인당 최대 20개의 쿠키 값 저장 가능하다.
- Set Cookie 설정 시 도메인 설정 가능
    (cookie_name=cookie_value; domain=example.com)
    - 여기서 궁금한건 domain은 일반적으로 wild domain을 사용해야 서비스 관점에서 편하지 않을까?
- domain간 쿠키 공유가 가능하다.
    - 하지만 다 되는건 아니다!
    - 하위 도메인간 쿠키는 공유하지 않는다.(example.com, sub.example.com 간 공유는 안됨)
    - 브라우저의 SOP(Same Origin Policy)를 따라야 하기 때문에
    - Q. 그럼 하위 도메인까지 커버 할 수 있는 방법은?
    - A. 쿠키의 도메인 설정에 하위 도메인까지 포함하는 방법밖에 없다. 즉, 도메인당 등록 하는건 똑같다.
