# [Browser event](https://ko.javascript.info/introduction-browser-events)

## 이벤트

브라우저는 event 발생 시 `handelEvent` 함수를 호출하고, 매개변수로 event 객체를 전달한다.

-   `handleEvent` 를 재정의하면 됨

    -   HTML
        `<button onclick="">` 잘쓰이지 않음
    -   DOM 프로퍼티 등록: `elem.onclick = function () {...}`
        하나의 함수를 등록할 수 있음
    -   메소드 등록: `elem.addEventListener(event, handler[, phase])`
        가장 유연한 방법, 객체 형태 이벤트 지원, handleEvent 호출

-   addEventListner, removeEventListener에서 같은 함수를 매개변수를 전달해줄 때 함수를 할당하고 처리해야 함

    ```js
    btn.addEventListener('click', () => alert(1));
    btn.removeEventListener('click', () => alert(1));
    ```

    결과: 1이 두번 나옴
    내용은 같지만 다른 함수이기 때문에!
    같은 함수로 처리하려면 함수에 대한 참조를 전달해야 한다.(객체 형태로 전달)

<br><br><br><br>

## [버블링과 캡처링](https://ko.javascript.info/bubbling-and-capturing)

### 버블링

하위 -> 상위 컴포넌트로 이벤트 호출
선택한 컴포넌트부터 document 객체를 만날때까지 할당된 핸들러 동작
거의 모든 이벤트는 버블링된다.

#### event.target

-   이벤트가 발생한 가장 안쪽의 요소
-   `event.target !== this(event.currenTarget)`
    -   event.target: 실제로 이벤트를 발생시킨 요소 => 버블링이 진행되어도 변화하지 않음
    -   event.currentTarget: 현재 이벤트가 진행중인 요소 => 현재 실행중인 핸들러가 할당된 요소

#### 버블링 중단

`event.stopPropagation()`: 버블링 중단, 같은 레벨에 있는 나머지 핸들러는 동작
`event.stopImmdiatlyPropagation()`: 버블링 중단, 모든 핸들러 동작 중단

**꼭 필요한 경우가 아니라면 버블링을 막지 않는것이 좋다.**

<br><br>

## 캡처링

하위 -> 상위 요소로 이벤트 전파
해당 단계를 이용해야 하는 경우는 흔지 않다.
사용할 경우 `addEventListener`의 `capture`옵션을 `true (default: false)`로 처리

-   `elem.addEventListener(..., { capture: true })`

<br><br>

## 표준 DOM 이벤트 단계

1. 캡처링 단계: 이벤트가 상위요소에서 타겟으로 전파
2. 타겟 단계: 이벤트가 실제 타겟에 전달
3. 버블링 단계: 이벤트가 타겟에서 상위요소로 전파

<br><br>

## 요약

이벤트 실행 순서

1. 이벤트 발생
2. document -> event.target 까지 내려감
    1. 내려가는 과정에서 `addEventListener(..., true)` 로 할당한 핸들러 동작(캡처링)
3. 타깃 요소에 설정된 핸들러 동작
4. event.target -> document 까지 올라감
    1. 올라가는 과정에서 `on<event>`, `addEventListener` 로 할당한 핸들러 동작(버블링)
    2. `addEventListener` 핸들러 중 **세번째 인수가 없거나 false, {capture: false}**인 핸들러만 호출

<br><br><br><br>

# [이벤트 위임](https://ko.javascript.info/event-delegation)

하위 요소에 각각 이벤트를 붙이지 않고 상위 요소에서 하위 요소의 이벤트들을 제어
이벤트 버블링을 통해 하위 컴포넌트의 변경을 신경쓰지 않고 상위 요소에서 처리하도록 위임함

예시

```js
// td에 이벤트 설정 -> td가 새로 생성될때마다 리스너 설정 => 비효율적
// tr에 이벤트 위임 -> 이벤트 버블링을 통해 td -> tr 은 필연적으로 동작하기 때문 => 효율적
<tr onclick='() => {...td handler 처리}'>
    <td>1</td>
    <td>2</td>
    <td>3</td>
</tr>
```

<br><br>

## 이벤트 위임 동작 과정

1. 컨테이너에 하나의 핸들러 할당
2. 핸들러의 `event.target`을 사용해 이벤트 발생 요소 알아냄
3. 원하는 요소라면 이벤트 핸들링 동작

<br><br><br><br>

# [브라우저 기본동작](https://ko.javascript.info/default-browser-action)

거의 모든 이벤트는 발생 즉시 브라우저에 의해 특정 동작을 자동으로 수행한다.
ex) 링크 클릭시 URL이동, 폼 전송, 마우스 드래그 등

<br><br>

## 기본 동작을 막으려면?

`event.preventDefault()` 를 사용하면 된다!

<br><br>

## addEventListener의 `passive` 옵션

`passive` 옵션은 브라우저에게 `preventDefault()`를 호출하지 않겠다고 알리는 역할
