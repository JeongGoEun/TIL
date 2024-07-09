>mounted일 때 로깅을 했는데 두번 출력됨 > strict mode 활성화로 인해

### [react strict](https://ko.react.dev/reference/react/StrictMode) 모드란?

개발 과정에서 디버깅을 더욱 효율적이게 하도록 도와주는 도구

1. 안전하지 않은 생명주기 메서드 식별
2. 레거시 문자열 사용 경고
3. 일부 생명주기 두 번 호출하여 부작용 감지
    - 해당 내용으로 보임
4. 렌더링 시 상태 변경 부작용 감지
5. 메모리 누수 감지

<br><br>
<hr>

### 목적

부작용의 일관성을 검사하고, cleanup 함수가 제대로 구현되었는지 확인하기 위함

상태 업데이트 함수는 두 번 호출되지 않음(`useState`의 `setter`)

<br><br>
<hr>

### 요약

개발 모드에서만 작동, 프로덕션 빌드에는 영향 없음

일부 effect 의도적으로 두 번 실행하여 버그 찾아냄

- `userEffect`
    - 의존성 배열이 비어있는 경우
    - 의존성 배열이 있는 경우에도 해당 의존성이 변경될 때

- 클래스 컴포넌트 생명주기 메서드
    - componentDidMount
    - componentDidUpdate
    - componentWillUnmount

- 기타 hooks
    - useMemo
    - useCallback
    - useImperativeHandle
    - useInsertionEffect

