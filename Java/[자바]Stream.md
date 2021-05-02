# Stream

참고한사이트
* [https://jeong-pro.tistory.com/165](https://jeong-pro.tistory.com/165)
* 

Stream은 자바 8부터 추가된 기능으로 "컬렉션, 배열등의 저장 요소를 하나씩 참조하여 함수형 인터페이스(람다식)을 적용하며 반복적으로 처리할 수 있도록 해주는 기능. (InputStream, OutputStream 같은 I/O Stream이 아니다.

~~~
List<String> names = Arrays.asList("jeong", "pro", "jdk", "java");
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


