# LOCK

- 데이터의 무결성을 보장하기 위한 방법
- `무결성` - 데이터가 정확하고 일관된 상태를 유지하도록 하는 것
- 둘 이상의 사용자가 같은 시간에 같은 데이터를 업데이트 하는 것을 방지하기 위해 존재
- 락이 걸린 데이터는 락이 풀릴 때까지 다른 사용자가 조작할 수 없다
- 오라클과 같이 고가의 DBMS를 사용하는 이유는 데이터의 일관성과 무결성을 유지하기 위함이다

## lock의 종류

### shared lock

- 데이터를 읽을 때 사용한다
- 내가 보고 있는 데이터는 다른 사용자가 볼수 있지만 변경은 할 수 없다
- 다른세션에서 데이터를 읽는 것은 가능하다

### exclusive lock

- 데이터를 변경할 때 사용한다
- 락이 해제되기 전까지는 읽기와 쓰기가 불가하다
- 하나의 트랜잭션이 끝날때 까지 유지되고 exclusive lock 이 끝날때까지 어떠한 접근도 허용되지 않는다

## lock 레벨

### ROW LEVEL

- 락의 설정 대상이 ROW인 곳에만 락을 설정

### PAGE LEVEL

- ROW가 있는 page에만 락을 설정
- 같은 페이지에 존재하는 모든 row는 모두 잠긴다

### TABLE LEVEL

- TABLE과 INDEX 모두 락을 설정

### DATABLASE LEVEL

- 데이터베이스의 복구나 스키마 변경시 락을 설정

### Column Level

- 컬럼 기준으로 Lock이 걸린다.
- Lock 설정 및 해제에 리소스가 많이들어 잘 사용하지 않는다.

## blocking

- 락의 경합으로 인한 상태
- 락들이 경합이 발생하여 특정 세션이 작업을 진행하지 못하고 머춰 선 상태
- 공유락과 exclusive 락 또는 익스클루시브 락과 익스클루시브 락이 경합이 발생할 수 있다
![blocking](https://user-images.githubusercontent.com/42866800/162599886-6f68922e-6a9f-4d29-bbed-a8a6ef2287bd.png)

### 블로킹 발생시 해결방안

- SQL 문 리펙토링 하여 빠르게 실행되도록 한다 (속도 개선)
- 트랜잭션을 짧게 정의한다
- 동일한 데이터를 동시에 변경하는 작업을 진행하지 않는다
- 대용략 작업이 불가피할 경우 작업단위를 쪼갠다
- 락 타임아웃을 설정하여 락의 최대시간을 설정한다

## 데드락

- 트랜잭션간 교착상태를 의미한다

![deadlock1](https://user-images.githubusercontent.com/42866800/162599889-5b1a0cff-7702-4ba7-87e1-cb7d9ee7db43.png)
- 두개의 트랜잭션이 각각의 트랜잭션이 갖고 있는 리소스의 락을 획득하려고 할때 발생한다
- 상대방 Lock이 끝나야 원하는 데이터를 가져오는데 바라보고 있는 서로의 Lock이 같은 상태가 되다보니 영원히 끝나지 않은 상황이 발생하게된다.

![deadlock2](https://user-images.githubusercontent.com/42866800/162599892-3518125e-be54-438e-af7f-474df87d73f3.png)
- 두번째 예는, 1번 트랜젝션이 공유Lock을 설정하고 Sleep에 빠졌습니다.
- 이때 2번 트랜젝션은 배타적Lock을 설정하려고 할때, 무기한 기다리게되는 교착상태에 빠지게 됩니다.

### 데드락 발생시 해결방안

- 둘중 하나의 트랜잭션을 강제 종료한다
- SET LOCK TIMEOUT 명령어를 사용하여 잠금해제 시간 설정
- 락이 걸리는 최대시간을 설정

## 블로킹 vs 데드락

- 블로킹은 트랜잭션이 끝나면 사라진다
- 데드락은 상대의 트랜잭션이 끝나기만을 기다리기 때문에 계속 끝나지 않는다

참고 - 

[https://akasai.space/db/about_lock/](https://akasai.space/db/about_lock/)

[Database Lock 종류 및 기능 (tistory.com)](https://centbin-dev.tistory.com/40)

[[데이터베이스] 트랜잭션과 격리성 (tistory.com)](https://sabarada.tistory.com/117)

[DB의 Lock/DeadLock | devlog.akasai](https://akasai.space/db/about_lock/)

[블로킹(Blocking)과 데드락(Deadlock) 차이 (tistory.com)](https://datacodingschool.tistory.com/100)

[https://cocoon1787.tistory.com/778](https://cocoon1787.tistory.com/778)

[https://chrisjune-13837.medium.com/db-lock-락이란-무엇인가-d908296d0279](https://chrisjune-13837.medium.com/db-lock-%EB%9D%BD%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-d908296d0279)
