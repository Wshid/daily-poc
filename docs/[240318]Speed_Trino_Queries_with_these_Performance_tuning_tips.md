# Speed Trino Queries with These Performance-Tuning Tips
- https://thenewstack.io/speed-trino-queries-with-these-performance-tuning-tips/

## 1. Performance Bottlenecks for Trino Queries

### Compute Resources
- 데이터 처리를 위해 많은 CPU를 사용
- source, 중간 결과, 최종 출력을 저장하기 위해 memory 소비
- workload, H/W resource를 염두하고
  - 각 노드의 CPU 코어수, memory 균형을 잡는 것이 중요

### I/O Speed
- Storage-independent query enigne
  - local disk에 데이터 저장 x
- 대신 external storage engine에서 데이터를 가져옴
- storage system/network 속도에 크게 영향을 미침

### Table Scans
- Connector에서 데이터를 가져와 다른 작업자가 사용할 데이터를 생성하는 구조
  - 대규모 데이터 세트 사용시 **성능 병목** 발생
- 테이블 분할 방식, Parquet/ORC 등의 선택은 쿼리 속도에 큰 차이 발생

### Joins
- 가장 resource-intensive한 action
- join을 효율적으로 수행할 것

## 2. Process of Optimizing Trino
- ![image](https://github.com/Wshid/daily-poc/assets/10006290/d5fbed30-fba0-4938-bd24-5765feee800d)
- Trino Web UI를 통해 전체 클러스터 속도가 느려지는가
- Trio Web UI가 쿼리에 대기열에 있거나 block 되는가
- `EXPLAIN ANALYZE`를 통해 slow query의 병목현상 식별

### EXPLAIN ANALYZE
```sql
EXPLAIN ANALYZE select * from customers limit 5;
```