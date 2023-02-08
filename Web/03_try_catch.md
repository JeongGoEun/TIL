# webstorm throw warning

### 상황

1. 카카오 로그인 구현 중, 해당 sdk를 lazyLoading하여 가져온다.
2. lazyLoading이 완료되면 window에 Kakao 전역 객체가 생성한다.
3. 이후 콜백에서 Kakao 전역 객체가 생성되었는지 확인하는 작업이 필요했다.
4. try-catch 를 사용하기 때문에 아예 에러를 던져서 예외 상황에 대해 모두 catch에서 처리하고 싶었다.

### as-is 코드

```js
try {
    if (!window.Kakao) {
        alert('카카오톡 연동 장애로 인해 일부 서비스 이용이 원활하지 않습니다. ');
        return;
    }

    if (!Kakao.isInitialized()) Kakao.init(KAKAO_CLIENT_ID);
} catch (e) {
    alert('카카오톡 연동 장애로 인해 일부 서비스 이용이 원활하지 않습니다. ');
}
```

### to-be 코드

```js
try {
    if (!window.Kakao) throw new Error(); // warn: 'throw' of exception caught locally
    if (!Kakao.isInitialized()) Kakao.init(KAKAO_CLIENT_ID);
} catch (e) {
    alert('카카오톡 연동 장애로 인해 일부 서비스 이용이 원활하지 않습니다. ');
}
```

이유

-   exception은 **개발자가 예상하지 못한 에러**들을 처리할 때 쓰는 것
-   if문으로 예상 가능한 에러이기 대문에 로컬 블록 내에서 처리하는 것이 좋다.

[참고문서](https://velog.io/@milkcoke/Node.js-Throw-of-exception-caught-locally)
