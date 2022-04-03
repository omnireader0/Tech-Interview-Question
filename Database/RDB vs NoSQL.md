# RDB

- 관계형 데이터 모델에 기초를 둔 데이터베이스
- 데이터를 2차원 테이블 형태로 표현
- key와 value의 관계를 테이블화 시켰다

![RDB구조](https://user-images.githubusercontent.com/42866800/161411255-a7c32567-4bac-4e96-af05-b2e5d39a622f.png)

# RDBMS

- 관계형 데이터베이스를 생성하고 관리할 수 있는 소프트웨어
- 개체(entity) , 관계(relationship)를 테이블로 표현
- 개체 - 독립적으로 존재하는 대상
- 테이블은 row와 column으로 구성된 데이터 저장 단위
- `R`
- 개체 또는 속성들의 관계
- 여러개의 테이블을 조합해 원하는 데이터를 찾아올 수 있게 한다
- 테이블 한 개로 데이터를 얻을 수 없는 경우 관계성을 이용해 더 복잡한 연산 수행
- `MS`
- 테이블에 데이터를 삽입 조회 수정 삭제 할 수 있도록 도와주는 소프트웨어
- DBMS가 SQL을 통해 가능하다

## ER(Entity Relation) 모델

- 세상의 사물을 개체(Entity)와 개체의 관계로 표현함
- 개체 : 독립적인 의미를 지니고 있는 유무형의 사람 또는 사물. 개체의 특성을 나타내는 속성(attribute)에 의해 식별됨.
- 개체끼리 서로 관계를 가짐.

![er모델링](https://user-images.githubusercontent.com/42866800/161411260-bb2a5b1b-8db9-4cb3-b701-dafa4a4e55c1.png)

## 관계형 데이터베이스 구조

- 모든 데이터를 2차원 테이블로 표현
- 테이블은 유일한 이름을 가짐
    - 열은 필드 , 아이템 , 컬럼
    - 행은 레코드 , 튜플 , 로우
- `key` - 테이블에서 레코드를 유일하게 식별할 수 있는 속성의 집합
    - 기본키 - 레코드를 유일하게 식별할 수 있는 속성의 집합
    - 외래키 - 어떤 테이블의 기본 키를 다른 테이블에서 사용할때 지정할수 있는 키
    

![관계형 데이터베이스](https://user-images.githubusercontent.com/42866800/161411262-fd72426c-d571-4290-accb-98a5945d1856.png)

## 조인 연산

- 두개 이상의 테이블을 연결시켜 필요한 데이터를 선택
- 고객이 어떤 상품을 언제 가장 많이 팔았는지 알고싶을때
- **이런 경우에는 상품 테이블과 고객 테이블을 같이 이용해야 하는데 이 때 조인(join) 연산 이용**

![rdb조인](https://user-images.githubusercontent.com/42866800/161411302-279d60ba-8db9-4661-851d-6a9310e99a31.png)
-42fb-9d25-4326737d18ff.png)
# NoSQL

- 기존 관계형 DBMS가 갖고 있는 특성 + 다른 부가적인 특성을 지원
- 데이터 저장및 검색을 위한 특화된 메커니즘
- 최적화된 키 값 저장 기법 → 응답속도 , 처리 효율성 높음

![mongodb vs rdb](https://user-images.githubusercontent.com/42866800/161411270-079f2677-3cd7-4273-a75c-36ba0a552494.png)
- mongoDB의 경우 도큐먼트에 접근하여 JSON 형식으로 CRUD 작업 진행

![rdb nosql _ 쿼리 질의방법](https://user-images.githubusercontent.com/42866800/161411272-07fc159f-c250-46c1-9916-1792ab694fe6.png)
## NoSQL- mongodb

- key - value 쌍으로 데이터 저장
- JSON 형식으로 데이터를 관리

![NoSQL 임베디드 방식 vs 레퍼런스 방식](https://user-images.githubusercontent.com/42866800/161411274-0d7b87f7-3d78-4291-84e4-9736b620ed1d.png)

# RDB vs NoSQL

- 테이블을 연결해서 조회하는 조인 기능이 없다
- 데이터 조회 하기위해 직접 SQL을 작성하지 않아도 된다
- 데이터의 속성값이 다양한 타입을 갖는다
- 비 관계형 데이터베이스
- 조인을 지원하지 않음

--------------------------------------------------------------------------------------------

# RDBMS Master 와 Slave

- 이중화 구성 -Replication
- 데이터가 날아가는 것 방지
- `Master`
    - 등록 / 수정 / 삭제 쿼리 요청시 BinaryLog를 생성하여 slave로 전달
- `Slave`
    - Master 정보 복제
    - 조회 쿼리 요청 처리
    - 디비 부하 분산

![master와 slave](https://user-images.githubusercontent.com/42866800/161411363-cc0088d7-ed0c-4925-8959-ecac67646aa6.png)

- (1) Client가 쓰기 쿼리 작업을 요청합니다. 쓰기 쿼리요청은 Master DB가 받는다
- (2) Master는 변경사항을 Binary log 파일에 기록합니다. 이후 DB에 반영(commit)한다.
- (3) Slave는 현재까지 기록한 이벤트 정보 (GTID=2)를 가지고 다음 이벤트 정보를 Master에게 요청한다.
- (4) Master는 Binary log 파일에서 최신 이벤트 정보(GTID=3)를 읽어
- (5) Slave에게 전송한다.
- (6) Slave는 Master에게 받은 이벤트 정보(GTID=3)를 Relay log 파일에 기록한다.
- (7) Slave는 최종 변경사항을 DB에 반영(commit)한다.
- (4)(5) 과정에서는 Master 쓰레드, (3)(6) 과정에서는 Slave I/O 쓰레드, (7) 과정에서는 Slave SQL 쓰레드가 동작합니다.

`MasterThread`

- Binary Log를 읽어 Slave 쪽으로 데이터 전송
- Slave가 클라이언트 , Master가 서버입장에서 응답을 하는 구조

`Slave I/O Thread`

- Master로 부터 Binary Log 데이터를 받아 Relay 로그 파일에 기록

`Slave SQL Thread`

- relay log에 반영된 내용을 읽어 DB에 반영 (커밋)

참고 - 

[https://jwprogramming.tistory.com/52](https://jwprogramming.tistory.com/52)

[http://thecoding.kr/관계형-데이터베이스rdb/](http://thecoding.kr/%EA%B4%80%EA%B3%84%ED%98%95-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4rdb/)

[https://jwprogramming.tistory.com/70](https://jwprogramming.tistory.com/70)

[https://meetup.toast.com/posts/275](https://meetup.toast.com/posts/275)

[https://it-sunny-333.tistory.com/148](https://it-sunny-333.tistory.com/148)

[https://intrepidgeeks.com/tutorial/02rdb](https://intrepidgeeks.com/tutorial/02rdb)

[https://ko.wikipedia.org/wiki/관계형_데이터베이스](https://ko.wikipedia.org/wiki/%EA%B4%80%EA%B3%84%ED%98%95_%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4)
