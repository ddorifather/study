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
