# React Query
React에서 비동기 데이터를 관리하기 위한 라이브러리
다양한 api 상태를 지원한다.


## Questions

1. useQueryClient()의 역할
mutation 성공 후 서버 상태를 다시 불러오기 위해 사용
cache 초기화를 위해 사용된다고 함
- queryClient.invalidQueries(`${QUERY_KEY}`);

2. queryKey
- 데이터 캐싱과 재사용 > 동일 키로 데이터를 요청하면, 캐시된 데이터 반환(네트워크 요청 생략)
- 배열이나 객체 형태를 통해 다양한 키 유형 지원
- queryKey에 의존된 값이 변경되면 자동으로 해당 쿼리 실행