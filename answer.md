### 1. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)의 장단점 비교
* **관계형 데이터베이스란?**  
하나 이상의 열과 행으로 이루어진 테이블에 저장된 정보를 구조화하는 방식이다. 테이블을 조인하여 정보 간 관계 또는 링크를 설정하는 기능이 있어, 여러 데이터(테이블)간의 관계를 쉽게 이해하고 정보를 얻을 수 있다. 관계형 데이터베이스의 데이터는 정해진 데이터 스키마를 따라 데이터베이스 테이블에 저장되고, 관계를 통해서 연결된 여러개의 테이블에 분산되는 특징을 가지고있다.
* **비관계형 데이터베이스란?**  
관계형 데이터베이스와 달리 스키마에 대한 정의나 PK, FK, Join 등으 관계를 정의하지 않는다. 대신 데이터를 연결되지 않은 개별 파일(컬렉션)로 저장한다. 
* **장단점 비교**  
**관계형 데이터베이스**의 장점은 명확하게 정의 된 스키마로 인해 데이터 무결성이 보장된다. 또한 데이터를 중복없이 한 번만 저장된다. 단점은 상대적으로 덜 유연하기 때문에 나중에 데이터 스키마를 수정하기 번거롭거나 불가능 할 수 있다. 테이블끼리 관계를 맺고 있기 때문에 Join문이 많은 매우 복잡한 쿼리가 만들어 질 수 있다. 또한 수평정 확장이 어렵고 대첼 수직적 확장만 가능하다.   
**비관계형 데이터베이스**의 장점은 스키마가 없기 때문에 훨씬 유연해 언제든지 새로운 필드를 추가할 수 있다. 또한 데이터를 읽어오는 속도가 빠르고 수평 확장이 용이하다. 단점은 데이터 중복으로인해 여러 컬렉션과 문서가 변경된 경우 모든 컬렉센에서 수정(update)을 해야한다.  
```위와 같은 특성을 고려하여 관계형 데이터베이스는 데이터가 자주 수정되고 스키마가 변경될 여지 없이 명확한 경우 사용하는 것이 좋고, 비관계형 데이터베이스는 정확한 데이터 구조를 알 수 없건 변경 / 확장 될 수 있는 경우와 읽기(read)처리를 주로 하고 데이터를 자주 변경(update)하지 않는 경우에 사용하면 좋다.```


### 2. 트랜잭션(transaction)이란 무엇인가요?
* **트랜잭션이란?**  
데이터베이스의 상태를 변화시키기 위해 수행하는 작업의 단위를 뜻한다. 즉 SELECT, INSERT, DELETE, UPDATE 와 같은 SQL문을 사용하여 데이터 베이스에 접근하여 수행하는 작업단위를 말한다. 유의할점은, 작업의 단위는 SQL 한 문장이 아니라는 점이다. 예를들어 게시판에 새 글을 작성할 때 INSERT문을 사용해 사용자가 입력한 글의 데이터를 등록한 후, SELECT를 사용해 방금 등록한 글과 기존 글들을 조회한다. 여기서 작업단위는 INSERT문과 SELECT문을 합친 것이다. 이러한 작업단위를 하나의 트랜잭션이라 한다.
* **트랜잭션의 특징**  
트랜잭션의 특징은 크게 4가지로 **원자성(Atomicity), 일관성(Consistency), 독립성(Isolation), 지속성(Durability)** 로 구분된다. 원자성은 **트랜잭션이 데이터베이스에 모두 반영되거나, 전혀 반영되지 않아야 한다**는 것이다. 일관성은 **트랜잭션의 작업 처리 결과가 항상 일관성 있어야 한다**는 것이다. 독립성은 둘 이상의 트랜잭션이 동시에 실행되고 있는 경우 **어떤 트랜잭션이라도 다른 트랜잭션의 연산에 끼어들 수 없다**는 것이다. 지속성은 **트랜잭션이 성공적으로 완료됐을 경우, 결과는 영구적으로 반영되어야 한다**는 것이다. 


### 3. MySQL에서 조인(join)의 역할은 무엇인가요? 다양한 join의 방식에 대해 설명해주세요.
* **Join이란?**  
한 데이터베이스 내의 여러 테이블의 레코드를 조합하여 하나의 열로 표현한 것이다.
* **Join의 종류**  
  <img width="600" alt="SQL_Joins" src="https://user-images.githubusercontent.com/96585009/216287913-23f4ab6d-b998-4216-90a9-ac168c0c37ad.png">
  1) **Inner Join** : 두 테이블 간의 교집합, 즉 겹치는 컬럼이 존재하는 경우 조건이 부합하는 행만을 가지고 오는 방법
  2) **Outer Join** : 두 테이블 간의 교집합이 되는 데이터 뿐만 아니라, **해당되지 않는 값**까지 가져오는 방법.  
  ```Outer Join은 Inner Join 고 다르게 처음으로 가져오는 기준이 되는 드라이빙 테이블 필요하다. 기준이 되는 테이블의 모든 정보는 가지고 오고, 대상이 되는 테이블은 Join 조건이 일치하지 않아도 가지고 온다. 때문에 쿼리 성능을 위해 올바른 드라이빙 테이블을 선택하는것이 중요하다.```
      - **Left (Outer) Join** : 기준 테이블을 왼쪽에 두고 Outer Join을 수행하는 방법. 대상이 되는 테이블에 데이터가 없을 경우 Null로 저장.
      - **Right (Outer) Join** : 기준 테이블을 오른쪽에 두고 Outer Join을 수행하는 방법. 대상이 되는 테이블에 데이터가 없을 경우 Null로 저장.
      - **Full (Outer) Join** : 왼쪽 오른쪽 모든 데이터를 읽어 결과를 생성. 즉, Left Join과 Right Join의 결과를 합한 결과라고 볼 수 있음.


### 4. MySQL에서 인덱스(index)란 무엇인가요?
* **인덱스란?**  
말 그대로 책의 맨 처음이나 마지막에 나오는 색인이라고 할 수 있다. 
* **인덱스의 장점**  
검색 속도가 무척 빨라질 수 있고, 해당 쿼리의 부하가 줄어 결과적으로 시스템 전체의 성능을 향상시킬 수 있다.
* **인덱스의 단점**  
처음 인덱스 생성시 시간이 많이 소요될 수 있고 데이터 베이스 공간을 대략 10%정도 차지한다. 무엇보다 데이터의 변경 작업이 자주 일어나는 경우 오히려 성능을 저하시킬 수 있어 올바르게 사용해야 한다.
* **효율적인 인덱스 사용**  
```인덱스는 저장공간, CUD속도를 희생하여 SELECT의 속도를 높이는 것이라 볼 수 있다.```
	- WHERE 절에 자주 등장하는 컬럼을 인덱스로 설정
	- ORDER BY 절에 자주 등장하는 컬럼을 인덱스로 설정
	- SELECT 절에 자주 등장하는 컬럼들을 잘 조합해서 인덱스로 설정
	- JOIN이 자주 사용되는 열에 인덱스를 생성
