# Vue plugin

-   Vue에 app 레벨로 코드를 직접 포함하도록 도와줌
-   `Vue.use(plugin)` 을 호출하여 플러그인을 설치하고 사용하는 코드이다.
-   플러그인에 정의된 `install()` 메소드를 호출하여 설치한다.
-   Vue 컴포넌트 내부에서 this로 편하게 접근할 수 있다.
-   플러그인을 사용하면 컴포넌트에서 매번 라이브러리를 호출하지 않아도 되는 장점이 있다.

    용량이 큰 라이브러리는 플러그인 형태로 사용하는게 성능면으로 좋다.

-   자주 사용될만한 속성, 함수, 라이브러리등의 사용성을 향상시켜준다.

<br><br>

custom plugin 을 등록하는 예제이다.

해당 파일들의 디렉토리 경로는 `@/plugins/common-plugin`

```js
// index.js
import Vue from 'vue';
import commonPlugin from './common-plugin';

// commonPlugin을 사용하겠다.
Vue.use(commonPlugin);
```

```js
// common-plugin.js
import * as d3 from 'd3'

export default {
    // use가 호출되면 플러그인에 정의된 install함수를 호출하여 설치한다.
    install(Vue, params) {
        // 플러그인 정의(속성, 함수 등 자유롭게 가능하다.)

        // 1. 라이브러리 정의 -> 컴포넌트 내에서 this.d3로 접근 가능
        Vue.prototype.d3 = d3;

        // 2. 커스텀 속성 정의 -> 컴포넌트 내에서 this._$customProperty로 접근 가능
        Vue._$customProperty = Vue.property._$customProperty = {
            ...
        },

        // 3. 메소드 정의 -> this.$printSomething(contents) 으로 접근 가능
        Vue.prototype.$printSomething =  function(param)  {
            console.log(param);
        };
    }
};
```

-   전역으로 사용할 땐 `Vue.추가할요소` 로 정의해준다.
-   인스턴스 메서드나 속성으로 사용할 땐 `Vue.prototype.추가할요소` 로 정의해준다.
