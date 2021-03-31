### SQL or NoSQL

* SQL (Structured Query Language) - Relational DataBase
  - RDBMS(Relational DataBase Management System)에서 데이터를 저장, 수정, 삭제 및 검색 가능함
  - 주요 특징
    + 데이터는 정해진(엄격한) 데이터 스키마(=structure)를 따라 데이터베이스 테이블에 저장
    + 데이터는 관계를 통해서 연결된 여러 개의 테이블에 분산
  - 엄격한 스키마 (Schema)
    + 데이터는 테이블(table)에 레코드(record)로 저장
    + 테이블에는 명확하게 정의된 구조(structure)가 존재
    + 구조는 필드(field)의 이름과 데이터 유형으로 정의
 ![table_structure](https://user-images.githubusercontent.com/19465623/113081999-ad559380-9214-11eb-9337-b6c911f222ba.jpg)
    + 스키마를 준수하지 않는 레코드는 추가할 수 없음
  - 관계 (Relation)
    + 데이터들을 여러 개의 테이블에 나누어서, 데이터들의 중복을 피할 수 있음
    + 이는 다른 테이블에서 부정확한 데이터를 다룰 위험이 없음
 ![table_relation](https://user-images.githubusercontent.com/19465623/113089794-5acfa380-9223-11eb-921c-0c657f48eac6.jpg)

* NoSQL (No Structured Query Language) - No Relational DataBase
  - 스키마 없음
  - 관계 없음
  - 레코드 = Documents
    + 다른 구조의 데이터를 같은 컬렉션(SQL에서의 테이블)에 추가할 수 있음
 ![nosql](https://user-images.githubusercontent.com/19465623/113089918-98ccc780-9223-11eb-9c9a-1d6fc79fe82b.jpg)
    + 문서는 JSON 데이터의 형태 (schema는 무시)
    + 일반적으로 관련있는 데이터들은 동일한 컬렉션에 포함 (관계형처럼 여러 테이블로 나누지 않음)
    + 여러 테이블 및 콜렉션에서 조이(join)할 필요없이 필요한 모든 것을 갖춘 문서를 작성
    + NoSQL 데이터베이스는 조인이라는 개념이 없음
    + 컬렉션을 통해 데이터를 복제하여 각 컬렉션 일부분에 속하는 데이터를 가져옴
![nosql_dup](https://user-images.githubusercontent.com/19465623/113096661-91f88180-9230-11eb-8778-3c28a4debbe7.jpg)
    + 이 방식은 데이터가 중복되므로 불안정함 --> 컬렉션 B에서 수정한 데이터를 컬렉션 A에서 업데이트 하지 않으면 데이터 정합성이 맞지 않음
    + 특정 데이터를 같이 사용한다면, 해당 데이터를 사용하는 모든 컬렉션에서 동일한 업데이트가 필요함
    + 그럼에도 불구하고 조인을 사용할 필요가 없다는 것은 큰 장점임
    + 자주 변경되지 않는 데이터의 경우 사용하기 좋음

* 확장(Scaling) - 수직적(Vertical) & 수평적(Horizontal)
  - 수직적 확장
    + 데이터베이스 서버의 성능 향상 (CPU 및 Memory 증설 등)
  - 수평적 확장
    + 서버 추가 및 데이터베이스의 분산을 의미
![scaling](https://user-images.githubusercontent.com/19465623/113097626-37f8bb80-9232-11eb-8435-220d842b514b.jpg)
  - 데이터가 저장되는 방식 때문에 SQL 데이터베이스는 일반적으로 수직적 확장만을 지원
  - 수평적 확장은 NoSQL 데이터베이스에서만 가능함
  - SQL 데이터베이스는 [샤딩(Sharding)](https://newbread.github.io/Sharding/ "Sharding")의 개념을 알고 있지만 특정 제한이 있으며 구현하기가 대체로 어려움
  - NoSQL 데이터베이스는 이를 기본적으로 지원 --> 여러 서버에서 데이터베이스를 쉽게 분리 가능

* 장/단점
  - 데이터의 종류와 데이터를 사용하는 어플리케이션을 고려하여 결정
  - SQL
    + 장점
      * 명확하게 정의된 스키마 - 데이터 무결성 보장
      * Relation - 데이터는 중복없이 한 번만 저장
    + 단점
      * 덜 유연함 - 데이터 스키마는 사전에 계획되고 알려져야 하며, 수정이 어렵거나 불가능함)
      * Relation - Join문으로 인해 복잡한 쿼리가 만들어질 수 있음
      * 수평적 확장이 어려움
    + 적용
      * Relation을 가지고 데이터가 자주 수정되는 어플리케이션의 경우
      * 스키마가 변경될 여지가 없고, 해당 스키마가 사용자와 데이터에게 중요한 형태일 때
  - NoSQL
    + 장점
      * 스키마가 없으므로 유연함 - 언제든지 저장된 데이터를 조정하고 새로운 필드를 추가할 수 있음
      * 데이터는 어플리케이션이 필요로 하는 형식으로 저장 가능 - 데이터를 읽어오는 속도가 빨라짐
      * 수직 및 수평적 확장이 가능
    + 단점
      * 유연함 - 데이터 구조 결정이 어려움
      * 데이터 중복으로 인해 레코드 변경 시 다수의 컬렉션과 문서를 업데이트 해야함
    + 사용
      * 정확한 데이터 구조를 알 수 없거나 변경 또는 확장될 수 있는 경우
      * Read는 자주 하지만, Update를 자주 하지 않는 경우
      * 데이터베이스의 수평적 확장이 필요한 경우 (대량의 데이터 처리가 필요)

* Reference
  - https://siyoon210.tistory.com/130 의 내용을 인용함
