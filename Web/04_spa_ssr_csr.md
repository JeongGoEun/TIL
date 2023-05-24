SPA
초기에 모든 정적 리소스(html, css, js) 로드
이후엔 필요한 뎅터만 서버로부터 비동기로 로드하여 동적으로 콘텐츠를 업데이트
장점: 사용자 경험 향상, 빠른 전환 속도, 서버 부하 감소

SSR
서버에서 html을 동적으로 생성하는 방식
초기에 완전히 렌더링된 html을 제공하기 때문에 초기 로딩 속도가 빠름
seo 최적화
단점: 서버 부하 큼, 페이지 전환시 서버와의 추가요청 필요


CSR
초기에 정적 리소스 로드 후 클라이언트에서 js를 사용하여 동적으로 콘텐츠 렌더링
페이지 전환시 서버로부터 데이터를 비동기적으로 가져와 렌더링
초기 로딩시간이 길지만, 페이지 전환시 서버 요청 필요 없음 -> 빠른 전환 속도
서버 부하 감소, 클라이언트측에서 ui 업데이트를 자유롭게 처리 가능


GPT 질문 정리하기
