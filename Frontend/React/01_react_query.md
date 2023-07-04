# React Query
React에서 비동기 데이터를 관리하기 위한 라이브러리
다양한 api 상태를 지원한다.


## Questions

1. useQueryClient()의 역할
mutation 성공 후 서버 상태를 다시 불러오기 위해 사용
cache 초기화를 위해 사용된다고 함
- queryClient.invalidQueries(`${QUERY_KEY}`);