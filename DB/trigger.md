# 트리거
트리거는 데이터베이스 이벤트에 반응하여 실행되는 프로그램 단위이다.   
자동적으로 수행되는 사용자 정의 프로시저이다.   
트리거는 TABLE과는 별도로 DATABASE에 저장된다. (VIEW에 대해서가 아니라 TABLE에 관해서만 정의될 수 있다.)    
제약조건과 함께 데이터 무결성을 지키는 하나의 방법으로써 특정 이벤트에 대해서 연속적으로 자동 동작하는 특수한 형태의 저장 프로시저   

## 종류

- 문장 트리거   
트리거가 설정된 테이블에 트리거 이벤트가 발생하면 많은 행에 대해 변경 작업이 발생하더라도 오직 한번만 트리거를 발생시키는 방법.   
값이 변화가 생길때마다 스스로 알아서 실행된다. (FOR EACH ROW 옵션 사용안함)   
   
- 행 트리거    
조건을 만족하는 여러개의 행에 대해 트리거를 반복적으로 여러번 수행하는 방법 (FOR EACH ROW WHEN 조건으로 정의)   
칼럼의 데이터 행이 변화가 오면 실행된다.    
   
## 문법
~~~
CREATE [OR REPLACE] TRIGGER trigger_name
BEFORE | AFTER
trigger_event ON table_name
[ FOR EACH ROW ]
[ WHEN (condition) ]
PL/SQL block

OR REPLACE : 생성할 트리거와 같은 이름을 가지고 있어도 무시하고 새로운것으로 갱신하는 것
BEFORE : INSERT, UPDATE, DELETE 문이 실행되기 전에 트리거가 실행된다.
AFTER : INSERT, UPDATE, DELETE 문이 실행된 후 트리거가 실행된다.
trigger_event : INSERT, UPDATE, DELETE 중에서 한 개 이상 올수 있다.
FOR EACH ROW : 이 옵션이 있으면 행 트리거가 된다.
~~~

## 테스트
~~~

1.
CREATE TABLE BONUS_DUPLE AS SELECT * FROM BONUS; (기존 BONUS테이블과 동일한 테이블을 만든다.)

2. 
CREATE OR REPLACE TRIGGER BONUS_TEST
BEFORE INSERT ON BONUS
FOR EACH ROW
BEGIN
IF INSERTING THEN
INSERT INTO BONUS_DUPLE(ENAME,JOB,SAL,COMM)
VALUES(:NEW.ENAME,:NEW.JOB, :NEW.SAL, :NEW.COMM);
END IF;
END BONUS_TEST;
(트리거를 생성한다.)

3. 
INSERT INTO BONUS VALUES('2','2','2','2');
(데이터를 삽입한다)

4.
BONUS 테이블과 BONUS_DUPLE 테이블에 동일한 데이터가 들어갔는지 확인해본다.


~~~
