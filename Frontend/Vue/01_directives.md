# v-on

-   약어: @
-   argument: event
-   이벤트 리스너에 부착
-   `normal element`인 경우 **native DOM events**만 사용 가능
    -   native인 경우 오로지 native event를(`$event`) 인자로 받는다
    -   ex) `@click="handle('ok', $event)`
-   `custom element`인 경우 **custom events**들 사용 가능

<br><br>

# v-model

-   `input`, `select`, `textarea`, `custom-component` 에 한해서 **양방향 바인딩**을 지원해줌

```js
    <input v-model="text" />

    <input v-bind:"text" @change="this.text = $event.target.value" />
```
