# 문자열을 다루는 String 클래스

## String VS StringBuffer VS StringBuilder 
자바에서 3개의 클래스모두 문자열을 저장하고 관리하는 클래스이다.   
String은 immutable(불변)하고 StringBuilder과 StringBuffer는 mutable(가변)하다.   
String은 불변하기 때문에 문자열을 수정하는 시점에는 새로운 String 인스턴스가 생성되고 기존 인스턴스는 GC제거 대상으로 제거된다.   

## StringBuffer VS StringBuilder
2개의 클래스 모두 가변한 클래스이지만 가장 큰 차이점은 동기화의 유무이다.   
StringBuffer는 동기화 키워드를 지원하여 멀티쓰레드 환경에서 안전하다. (String 클래스도 불변성을 가지기 때문에 멀티쓰레드 환경에서 안정성을 가진다.)   
StringBuilder는 동기화를 지원하지 않기 때문에 멀티쓰레드 환경에서는 적합하지 않지만 동기화를 고려하지 않는 만큼 단일쓰레드에서의 성능은 StringBuffer보다 뛰어나다.   

## 결론
String 클래스는 문자열 연산이 적고, 자주 참조하는 경우에 사용하면 좋다. 
멀티쓰레드 환경에서는 StringBuffer를 사용하면 좋고, 싱글 쓰레드환경이거나 동기화가 필요없는 경우에는 StringBuilder를 사용하는 것이 좋다.    
JDK 1.5이상부터는 String에서 + 연산으로 작성하더라도 StringBuilder로 컴파일하게 만들어 놨다.
