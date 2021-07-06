# view 

## view ? 
뷰(View)는 하나 이상의 테이블이나 다른 뷰의 데이터를 볼 수 있게 하는 데이터베이스 객체이다.   
실제 데이터는 뷰를 구성하는 테이블에 담겨 있지만 마치 테이블처럼 사용할 수 있다.   
테이블 뿐만 아니라 다른 뷰를 참고하여 새로운 뷰를 만들어서 사용할 수도 있다.

## view의 사용목적 ?
뷰는 복잡한 쿼리를 단순화 시킬수 있다. (여러테이블의 JOIN과 Group BY 같은 복잡한 쿼리를 view로 저장시킴)   
뷰는 사용자에게 필요한 정보만 접근하도록 접근을 제한할 수 있다.   
데이터보안측면에서 유리하다.

## view 문법
~~~
생성
CREATE OR REPLACE VIEW [스키마.][뷰 NAME] AS
SELECT 구절;


수정
CREATE OR REPLACE VIEW [스키마.][뷰 NAME] AS
SELECT 구절;

삭제
DROP VIEW [스키마.][뷰 NAME]

구조확인
DESC [스키마.][뷰 NAME];
~~~
