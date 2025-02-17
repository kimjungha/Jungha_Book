## Index 생성하는 기준 

1. 검색 속도 향상을 위함
2. 데이터 분포도 고려
3. 정렬, 그룹화에 사용되는 컬럼 

### 1. 검색 속도 향상 위함 
   * 자주 조회(검색) 되는 컬럼으로 인덱스 생성
   * where, join , order by, group by 절에서 사용되는 컬럼이 인덱스 후보
   * ```sql
     select * from orders where customer_id = 100;  //customer_id로 인덱스 생성하면 검색 속도 향상

### 2. 데이터의 분포도 고려
   * 선택도가 높은 컬럼으로 우선적으로 인덱싱해야한다. => customer_id (고유한 값 많음,선택도 높음) => 인덱스 생성 적절
   * 선택도(Selectivity) : 특정 컬럼에서 고유한 값이 많을수록 높아지고, 중복이 많을수록 낮아지는 개념
     *  남/ 여 값만 가지는 컬럼 -> 중복이 많으니 선택도가 낮음
     * customer_id -> 중복도가 낮고,고유한 값이 많아서 선택도가 높음

### 3. 정렬, 그룹화, 조인 에서 사용되는 컬럼 
   * order by, group by 에서 사용되는 컬럼을 인덱스에 추가하면 성능 향상될 수 있습니다. 
   *  ```sql
      select * from sales group by product_id; //product_id 로 인덱스 생성하면 그룹화 속도 향상
      select * from o.order_id, c. name
      from orders o 
      join customer c on o.customer_id = c.customer_id; //o.customer_id 와 c. customer_id 인덱스 생성하면 조인속도향상

## !! 자주 업데이트 되는 컬럼은 주의 !!
   * 인덱스 많아지면 insert,update,delete 성능 저하될 수 있음
   * 데이터 변경될 때, 인덱스 갱신해야하기 때문이다. 
   * 즉, 자주 변경되는 컬럼은 인덱스 생성을 신중하게 생각해야한다. 

### 기본 키(Primary Key)와 유니크 인덱스(Unique Index)
   * 기본키 컬럼, 유니크 제약조건 컬럼은 자동으로 인덱스 생성된다. 

### 복합 인덱스와 커버링 인덱스 
1. 복합 인덱스 
   * 하나 이상 컬럼을 조합하여 생성하는 인덱스
   * WHERE a = ? AND b = ? 같이 두 개 이상의 컬럼을 동시에 검색할 때 유용함.
   * ````sql
     SELECT * FROM orders WHERE customer_id = 100 AND order_date = '2024-02-17';
     /** (customer_id, order_date) 로 복합인덱스 생성하면 조회 속도 개선 가능 */
2. 커버링 인덱스
   * 쿼리를 실행할 때, 테이블을 조회하지 않고 인덱스만으로 데이터를 조회할 수 있는 인덱스
   * 인덱스에 필요한 모든데이터가 있어서, 테이블 접근 필요없음 => 인덱스에서 직접 결과를 반환함
   * ````sql
     CREATE INDEX idx_customer_order ON orders(customer_id, order_date);
     SELECT order_date FROM orders WHERE customer_id = 1001;

## 인덱스가 저장되는 위치는 ? (mysql 기준)
   * 인덱스는 테이블과 같은 물리적 공간에 저장되지 않으며, 별도의 인덱스 테이블에 저장된다. 
   * 인덱스는 특정테이블 데이터를 빠르게 찾기 위해서, 테이블의 데이터를 포인터 형태로 가리킨다. 

📌 MySQL (InnoDB)
   1. 클러스터형 인덱스
      *  기본키 인덱스는 테이블의 실제 데이터와 함께 저장
      *  테이블 자체가 B-Tree 인덱스 구조로 저장
      *  테이블의 물리적 정렬 순서 = 기본 키 순서
   2. 보조 키 인덱스
      * 기본키가 아닌 컬럼 인덱스는 별도 파일에 저장
      * 하지만, 기본키값을 포함하여 저장되어 보조인덱스를 검색 후에 기본키를 이용해 원본 데이터 접근함
      