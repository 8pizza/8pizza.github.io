### Partitioning

#### Background
  - 서비스가 커지면서 그 만큼 필요한 테이블의 종류와 수가 많아짐
  - VLDB(Very Large DBMS)가 등장하면서 하나의 DBMS가 많은 Table을 관리하게 되고, 이는 성능 이슈를 야기함
  - 이를 해결하기 위한 방법 중의 하나가 Partitioning

#### Partitioning?
  - Database Partitioning
    + 논리 데이터베이스 또는 구성 요소를 별개의 독립 부분으로 나누는 것 --> 분할된 각 부분을 파티션이라고 함
    + 관리 용이성, 성능이나 가용성의 이유, 로드 밸런싱을 위해 수행됨
    + 분산 데이터베이스 관리 시스템에서 주로 사용됨 - 파티션은 멀티 노드로 분산되고 사용자는 각 노드에서 로컬 트랜잭션을 수행함
    + 가용성과 보안을 유지하면서 특정 뷰에 관한 일반 트랜잭션의 성능을 향상 시킴 

#### Partitioning criteria
  - 현재의 고급 관계형 데이터베이스 관리 시스템은 데이터베이스를 분할하기위한 다양한 기준을 제공
  - 파티션 키를 가져와 특정 기준에 따라 파티션을 할당
    + Range Partitioning:
    + List Partitioning: 
    + Composite Partitioning:
    + Round-robin Partitioning:
    + Hash Partitioning


Current high-end relational database management systems provide for different criteria to split the database. They take a partitioning key and assign a partition based on certain criteria. Some common criteria include:

Range partitioning: selects a partition by determining if the partitioning key is within a certain range. An example could be a partition for all rows where the "zipcode" column has a value between 70000 and 79999. It distributes tuples based on the value intervals (ranges) of some attribute. In addition to supporting exact-match queries (as in hashing), it is well-suited for range queries. For instance, a query with a predicate “A between A1 and A2” may be processed by the only node(s) containing tuples.
List partitioning: a partition is assigned a list of values. If the partitioning key has one of these values, the partition is chosen. For example, all rows where the column Country is either Iceland, Norway, Sweden, Finland or Denmark could build a partition for the Nordic countries.
Composite partitioning: allows for certain combinations of the above partitioning schemes, by for example first applying a range partitioning and then a hash partitioning. Consistent hashing could be considered a composite of hash and list partitioning where the hash reduces the key space to a size that can be listed.
Round-robin partitioning: the simplest strategy, it ensures uniform data distribution. With n partitions, the ith tuple in insertion order is assigned to partition (i mod n). This strategy enables the sequential access to a relation to be done in parallel. However, the direct access to individual tuples, based on a predicate, requires accessing the entire relation.
Hash partitioning: applies a hash function to some attribute that yields the partition number. This strategy allows exact-match queries on the selection attribute to be processed by exactly one node and all other queries to be processed by all the nodes in parallel.
