# Stream

참고한사이트
* [https://jeong-pro.tistory.com/165](https://jeong-pro.tistory.com/165)
* 

Stream은 자바 8부터 추가된 기능으로 "컬렉션, 배열등의 저장 요소를 하나씩 참조하여 함수형 인터페이스(람다식)을 적용하며 반복적으로 처리할 수 있도록 해주는 기능. (InputStream, OutputStream 같은 I/O Stream이 아니다.

~~~
List<String> names = Arrays.asList("ddori", "oracle", "jdk", "java");
// 기존의 코딩 방식
long count = 0;
for (String name : names) {
    if (name.contains("o")) {
        count++;
    }
}
System.out.println("Count : " + count); // 2
 
// 스트림 이용한 방식
count = 0;
count = names.stream().filter(x -> x.contains("o")).count();
System.out.println("Count : " + count); // 2

기존에는 어떠한 컬렉션의 요소를 순회하면서 요소의 개수를 구한다고 가정한다면 
스트림을 이용하면 한 줄의 코딩만으로도 count값을 구할 수 있다. 
즉, 불필요한 코딩(for,if)을 걷어낼 수 있고 직관적이기 때문에 가독성이 좋아진다.
이 점이 Stream의 장점이자 목적이다.
~~~

- Stream은 어떤 것들에 적용할 수 있을까?   
Stream은 주로 Collection, Arrays에서 쓰인다.    
~~~
List<String> names = Arrays.asList("ddori", "oracle", "jdk", "java");
names.stream(); //Collection에서 스트림 생성
 
Double[] dArray = {3.1, 3.2, 3.3};
Arrays.stream(dArray);//배열로 스트림 생성
 
Stream<Integer> str = Stream.of(1,2); // 스트림 직접 생성

~~~

- Stream 사용법과 주의사항

스트림의 구조는 크게 3가지이다. 1 스트림생성 2 중개연산 3 최종연산   
=> "Collections 같은 객체집합.스트림생성().중개연산().최종연산();" 이런식이다   

- 중개연산
1. Filter   
~~~


List<String> names = Arrays.asList("ddori", "oracle", "jdk", "java");
Stream<String> a = names.stream().filter(x -> x.contains("o"));

filter는 말 그대로 필터링, 즉 조건에 맞는 것만 거른다는 것이다.
위의 코드에서 람다식을 이용해서 x로 스트림의 요소를 받고 각 요소에 "o"라는 알파벳이 있는 것들만 거른다. 
즉 "ddori" , "oracle"만 가지고 있는 스트림을 반환한다. 

~~~

2. Map
~~~
List<String> names = Arrays.asList("ddori","oracle","jdk","java");
names.parallelStream()
     .map(x -> x.concat("s"))
     .forEach(x -> System.out.println(x));

ParallelStream은 Java에서 제공하고 있는 Stream중 하나로 Collection속의 데이터를 병렬 처리하기 위해서 사용됨.
map은 스트림의 각 요소를 연산하는데 쓰인다. 
~~~
3. Peek
peek()도 Map과 유사하게 각 요소에 어떤 연산을 적용할 때 사용한다.

4. Sorted
말 그대로 스트림의 요소들을 정렬해준다.

5. Limit
~~~
List<Integer> ages = Arrays.asList(1,2,3,4,5,6,7,8,9);
ages.stream()
    .filter(x -> x > 3)
    .limit(3);
//4,5,6

스트림의 개수를 .limit(3) 으로 지정하면 3개로 제한한다. (물론 중개연산이라 스트림 반환)

~~~

6. Distinct

스트림의 요소가 예를들어 1,2,1,2,1,2,일 때 .distinct()를 적용하면 1,2로 중복을 제거한다.

7. Skip

.skip(3)이라고 하면 처음 3개의 요소는 제외하고 나머지 요소들로 새로운 stream을 만든다.

8. MapToInt, MapToLong, MapToDouble

mapTo 함수들은 해당 타입의 스트림으로 바꿔준다. "1","2","3"을 가진 스트림이 있다면 MapToInt 하면 1,2,3 스트림으로 변환.   


- 최종연산
1. count(), min(), max(), sum(), average()

최종연산이기 때문에 앞서 함수를 적용했던 스트림에 있는 요소들에 대해 count를 세거나 최소값, 최대값, 합계, 평균 값을 얻을 수 있는 함수다.

2. reduce
~~~
List<Integer> ages = new ArrayList<Integer>();
ages.add(1);
ages.add(2);
ages.add(3);//1,2,3
System.out.println(ages.stream().reduce((x,y) -> x+y).get());//1+2+3=6

누적된 값을 계산하는 함수다.
x+y된 값이 다시 x가되고 다음 스트림의 요소가 y가 되어서 계속 누적된다.
~~~

3.forEach
~~~
List<Integer> ages = new ArrayList<Integer>();
ages.add(1);
ages.add(2);
ages.add(3);//1,2,3
Set<Integer> set = ages.stream().collect(Collectors.toSet());
set.forEach(x-> System.out.println(x));//1,2,3
forEach는 map이나 peek의 최종연산 버전이다. 각 요소를 돌면서 처리할 수 있도록 되어있다
~~~

4. collect
collect는 스트림의 값들을 모아주는 기능을 한다. toMap, toSet, toList로 해당 스트림을 다시 컬렉션으로 바꿔준다.

5. iterator
~~~
List<String> names = Arrays.asList("oracle", "ddori", "jdk", "java");
Iterator<String> iter = names.stream().iterator();
while(iter.hasNext()) {
    System.out.println(iter.next());//oracle, ddori, jdk, java
}
iterator는 Iterator<T>를 반환한다.
~~~

6. noneMatch, anyMatch, allMatch
~~~
List<Integer> ages = new ArrayList<Integer>();
ages.add(1);ages.add(2);ages.add(3);//1,2,3
System.out.println(ages.stream().filter(x -> x>1).noneMatch(x->x>2));//false

noneMatch는 최종적으로 얻은 스트림의 "모든" 요소들이 조건을 만족하지 "않는"지를 판단해서 boolean값을 리턴한다.

anyMatch는 스트림의 요소들 중에 하나라도 조건을 만족하는지 판단해서 boolean값을 리턴하고,

allMatch는 스트림의 "모든" 요소들이 조건을 만족하는지를 판단해서 boolean값을 리턴한다.



~~~
- 알아둘 것

1. stream은 재사용이 불가능하다.

2. 병렬 스트림은 여러 쓰레드가 작업한다.
stream()으로 스트림을 생성하지 않고 parallelStream()으로 병렬 스트림을 만들 수 있다. 이렇게 하면   
여러 쓰레드가 스트림에서 요소를 필터링하고 나온 요소 수를 계산하고 쓰레드끼리 다시 한 번 각자 계산하고 리턴해준다.   
단순하게 생각해서 여러 쓰레드가 처리해주니 병렬 스트림이 항상 성능면에서 유리해보일 수 있지만 어플리케이션에서 사용하는 쓰레드가 많거나   
스트림의 요소 수가 많지 않다면 오히려 쓰레드를 사용하는데 드는 오버헤드가 더 클 수도 있다.

3. 중개 연산은 미리하지 않는다 지연 연산을 한다.
~~~
Stream<String> a = names.stream().filter(x -> x.contains("o")).map(x-> x.concat("s"));
a.forEach(x -> System.out.println(x));

위와 같은 코드가 있으면 위에 filter와 map 함수는 미리 계산하고 있지 않고 있다가 forEach와 같은 최종연산이 적용될 때 중개 연산도 실행된다.

이로써 얻는 장점은 미리 계산하면서 두 번 순회하는 짓을 안할 수 있게 된다는 점이다.



~~~


