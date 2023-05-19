# script의 위치에 따라 왜 다른가?

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        ...
        <style>
            .supportWrap {
                display: none;
            }
            @media all and (-ms-high-contrast: none), (-ms-high-contrast: active) {
                .supportWrap {
                    display: block;
                    width: 100%;
                    height: 100%;
                }
                .supportWrap .supportCon {
                    position: absolute;
                    top: 50%;
                    left: 0;
                    width: 100%;
                    -webkit-transform: translateY(-50%);
                    transform: translateY(-50%);
                    text-align: center;
                    font-size: 20px;
                }
            }
        </style>
        <!-- 안내문구 div 안나옴 -->
        <script type="text/javascript">
            const isIE = window.navigator.userAgent.search(/(?:MSIE |Trident\/.*; rv:)(\d+)/g) !== -1;
            if (isIE) {
                window.location = 'microsoft-edge:' + window.location.origin;
                window.close();
            }
        </script>
        ...
    </head>
    <body>
        ...
        <div id="supportWrap" class="supportWrap">IE 접속 시 안내문구</div>
        <div id="app"></div>
        <!-- 안내문구 div 나옴 -->
        <script type="text/javascript">
            const isIE = window.navigator.userAgent.search(/(?:MSIE |Trident\/.*; rv:)(\d+)/g) !== -1;
            if (isIE) {
                window.location = 'microsoft-edge:' + window.location.origin;
                window.close();
            }
        </script>
        <!-- Convert IE -> Edge -->
        ...
    </body>
</html>
```

-   프로젝트 하다가, IE로 넘어갈 때 div 하나를 띄워줘야 함
-   case1) <head>에 있는 경우
    -   <div>표시 안됨
-   case2) <body>에 있는 경우
    -   <div>표시 됨

# 이유

-   window 객체를 다루어야 하는데, window 객체가 생성되는 시점은 html의 모든 태그가 화면에 올라가는 순간이기 때문에
-   script는 dom이 다 구성되고 나서 body의 최하단에 추가하는것이 효율적
    -   html파싱 도중 js를 만나면 멈추고 js 먼저 수행하기 때문
