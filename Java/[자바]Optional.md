# Optional
[참고](https://www.daleseo.com/java8-optional-before/)

* NULL   
토니 호어가 1965년에 알골(ALGOL W)이라는 프로그래밍 언어를 설계하면서 처음 등장   
당시에 그는 null 참조라는 개념이 “값이 없는 상황을 가장 단순하게 구현할 수 있는 방법”이라고 생각했다.   
하지만 시간이 흘러 2009년, 그는 자신이 고안한 null 참조를 “10억 달러짜리 실수”라고 표현하며 사과했다.   
단순히 구현하기 쉬웠기 때문에 null 참조를 구상했지만 이로 인해 수많은 오류, 취약성 및 시스템 충돌이 생기고 피해가 막대했기 때문이다.   
문제점은 먼저, 런타임에 NPE(NullPointerException)라는 예외를 발생시킬 수 있습니다. 두번쨰로 NPE 방어를 위해서 들어간 null 체크 로직 때문에 코드 가독성과 유지 보수성이 떨어집니다.   

* Optional ?   
Optional는 “존재할 수도 있지만 안 할 수도 있는 객체”, 즉, “null이 될 수도 있는 객체”을 감싸고 있는 일종의 래퍼 클래스입니다.    
원소가 없거나 최대 하나 밖에 없는 Collection이나 Stream으로 생각하셔도 좋습니다.   
직접 다루기에 위험하고 까다로운 null을 담을 수 있는 특수한 그릇

* Optinal의 장점
1. NPE를 유발할 수 있는 null을 직접 다루지 않아도 됩니다.
2. 수고롭게 null 체크를 직접 하지 않아도 됩니다.
3. 명시적으로 해당 변수가 null일 수도 있다는 가능성을 표현할 수 있습니다. (따라서 불필요한 방어 로직을 줄일 수 있습니다.)

---

## Optional 기본 사용법

* Optional 변수 선언하기   
<b>제네릭</b>을 제공하기 때문에, 변수를 선언할 때 명기한 타입 파라미터에 따라서 감쌀 수 있는 객체의 타입이 결정됩니다.   
~~~
Optional<Order> maybeOrder; // Order 타입의 객체를 감쌀 수 있는 Optional 타입의 변수   
Optional<Member> optMember; // Member 타입의 객체를 감쌀 수 있는 Optional 타입의 변수   
Optional<Address> address; // Address 타입의 객체를 감쌀 수 있는 Optional 타입의 변수   
~~~
변수명은 그냥 클래스 이름을 사용하기도 하지만 “maybe”나 “opt”와 같은 접두어를 붙여서 Optional 타입의 변수라는 것을 좀 더 명확히 나타내기도 합니다.   

* Optional 객체 생성하기
```
Optional.empty()  => null을 담고 있는, 한 마디로 비어있는 Optional 객체를 얻어옵니다. 이 객체는 내부적으로 미리 생성해놓은 싱글턴 인스턴스입니다.   
Optional<Member> mayberMember = Optional.empty();   

Optional.of(value) => null이 아닌 객체를 담고 있는 Optional 객체를 생성합니다. null이 넘어오면 NPE를 던지기 때문에 주의해야합니다.
Optional<Member> mayberMember = Optional.of(aMember);

Optional.ofNullable(value) => null인지 아닌지 확신할 수 없는 객체를 담고 있는 Optional 객체를 생성합니다. 위 두개를 합쳐놓은 메소드. null이 넘어오면 NPE를 던지지 않고
Optional.empty()와 동일하게 비어있는 Optional 객체를 얻어옵니다. 해당 객체가 null인지 아닌지 자신이 없을 경우에는 이 메소드를 사용해야 합니다.
Optional<Member> maybeMember = Optional.ofNullable(aMember);
Optional<Member> maybeNotMember = Optional.ofNullable(null);

```

* Optional이 담고 있는 객체에 접근하기   
null을 담고 있는경우는 다르게 동작하고 객체가 존재할 경우 동일하게 해당 값을 반환합니다.   
~~~
get() => 비어있는 Optional 객체에 대해서, NoSuchElementException 발생시킨다.
orElse(T other) => 비어있는 Optional 객체에 대해서, 넘어온 인자를 반환한다.
orElseGet(Supplier<? extends T> other) => 비어있는 Optional 객체에 대해서, 넘어온 함수형 인자를 통해 생성된 객체를 반환한다
orElseThrow(Supplier<? extends X> exceptionSupplier) => 비어있는 Optional 객체에 대해서, 넘어온 함수형 인자를 통해 생성된 예외를 던진다.
~~~


  
  

