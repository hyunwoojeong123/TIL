# Statement vs PreaparedStatement

- 속도는 `PreparedStatement` 가 빠름. 쿼리를 수행하기 전에 이미 쿼리가 컴파일 되어 있고, 반복 수행시 이 것을 사용해 수행하기 때문이다.

- `PreparedStatement` 에는 보통 변수를 설정하고 바인딩하는 `static sql` 사용

- `Statement` 에서는 쿼리 자체에 조건이 들어가는 `dynamic sql` 사용

- `PreparedStatement`가 파싱 타임을 줄여주지만 `static sql`을 사용하기에 성능 저하가 있을 수 있다.
- 하지만 성능에서 시간 부분의 가장 중요한 것은 테이블에서 레코드를 가져오는 과정이고, SQL 문을 파싱하는 시간은 이에 비하면 10분의 1에 불과하다. 그렇기 때문에 `SQL Injection` 등의 문제를 보완해주는
- `PreparedStatement`를 사용하는게 맞다.