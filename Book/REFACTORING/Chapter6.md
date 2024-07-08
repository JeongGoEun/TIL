# 기본적인 리팩터링

## 함수 추출하기

### p.159
코드를 보고 무슨 일을 하는지 파악하는 데 오랜 시간이 걸린다면?
- 그 부분을 함수로 추출한 뒤 '무슨 일'에 걸맞는 이름을 짓는다.

함수의 길이는 그리 중요하지않다. 목적이 명확하면 그게 잘 짜여진 함수이다.

함수 호출이 많아져서 성능이 느려질까 걱정하지 않아도 된다. 요즘은 그럴 일이 거의 없다. <br>
오히려 캐싱하기 쉽기 때문에 컴파일러가 최적화하는 데 유리할 때도 많다.

<br><br><hr>

## 변수 추출하기

### p.173
변수 추출을 하고싶다면, 표현식에 이름을 붙이고 싶다는 것이다. <br>

현재 함수 안에서만 의미가 있다면 변수로 추출하는 것이 좋다. <br>
범위가 보다 넓어졌다면, 변수가 아닌 함수로 추출하는 것이 낫다.

<br><br><hr>

## 함수 선언 바꾸기

### p.179

함수명은 고작 이름일 뿐이지만, 혼란을 막아준다. <br>
이런 혼란을 막아야 나중에 그 코드를 다시 볼 때 '또' 고민하지 않는다.

좋은 이름이 떠오르지 않다면, 주석을 이용해 함수의 목적을 설명해보자. <br>
그렇다면, 주석이 멋진 이름으로 되돌아올 때가 있다.


<br><br><hr>

## 변수 캡슐화하기

### p.179

접근할 수 있는 범위가 넓은 데터를 옮길 때엔, 해당 데이터의 접근을 독점하는 함수를 만들어 캡슐화한다.
- 데이터를 변경하고 사용하는 코드를 감시할 수 있는 확실한 통로가 된다.
- 데이터 변경 전 검증이나, 변경 후 추 로직을 쉽게 끼워넣을 수 있다.

데이터 캡슐화는 유용하지만, 그 과정은 간단하지 않다.<br>
분명한 사실은 데이터의 사용 범위가 넓을수록 적절히 캡슐화하는게 더 좋다.

<br><br><hr>

## 매개변수 객체 만들기

### p.197

데이터 뭉치를 데이터 구조로 묶으면 데이터 사이의 관계가 명확해진다.
매개변수 수가 줄어들고, 같은 데이터 구조를 사용하는 모든 함수는 같은 이름을 사용하기 때문에 일관성도 높여준다.

=> 코드를 더 근본적으로 바꿔준다.