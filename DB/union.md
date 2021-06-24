# UNION

UNION과 UNION ALL의 차이는 정렬작업의 수행 여부이다.   
UNION은 중복을 제거해야 하기 때문에 정렬작업을 수행하므로 성능이 저하된다.   
UNION, MINUS, INTERSECT는 전체범위를 모두 액세스 하는 정렬작업을 수행하기 때문에 부분범위처리가 불가능하다.   

