# Tech-Interview-Question

## ✅ 요약 및 질문 정리

### **네트워크**

#### 🔗 [질문 노트 바로 가기](https://github.com/omnireader0/Tech-Interview-Question/blob/main/Question/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC_%EC%A7%88%EB%AC%B8%EC%A0%95%EB%A6%AC.md)

#### ✍ 요약

- 쿠키, 세션, JWT 토큰
  - Cookie / Session
  - 세션 기반 인증 / 토큰 기반 인증
  - JWT
- 네트워크 시스템의 Layered Architecture
  - 웹의 동작 방식
  - TCP/IP 5 Layer
  - OSI 7 Layer
  - TCP, UDP, IP, PORT
- HTTP 와 HTTPS
  - HTTP/HTTPS
  - HTTP 2.0
- 로드 밸런서(Load Balancer)
  - 로드밸런싱
  - Scale out, Scale up
- 프록시(Proxy)
  - 포워드 프록시, 리버스 프록시
  - DMZ
- 네트워크 보안(Network Security)
  - 보안 3대요소, 웹 해킹, 방화벽
  - IPSec, SSL 과 TLS
  - SQL Injection, OS Command Injection, XSS, CSRF
- 웹 소켓(Web Socket)
  - HTTP Polling, HTTP Long Polling
  - HTTP vs 웹 소켓
- CORS(Cross Origin Resource Sharing)
  - CORS
  - SOP
  - 스프링 부트에서 CORS 해결 하는 방법
- REST and RESTful
  - REST 구성요소와 기본 원칙
  - REST API 디자인 가이드
- OAuth(Open Authorization)
  - OAuth1.0, OAuth2.0
  - 일반로그인과 OAuth로그인 차이
  - 인증 절차 종류

### **운영체제**

#### 🔗 [질문 노트 바로 가기](https://github.com/omnireader0/Tech-Interview-Question/blob/main/Question/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C_%EC%A7%88%EB%AC%B8%EC%A0%95%EB%A6%AC.md)

#### ✍ 요약

- 운영체제와 컴퓨터 시스템 구조
- 캐시의 지역성
  - 캐시의 종류와 쓰기
  - 캐시의 지역성
  - Mapping Function 개념 (MMU와 관련하여 설명) (Mapping Function 종류는 조사X)
- 메모리 구성
  - 스택 동작 과정
  - Stack 과 Heap
  - 프로세스/스레드에서의 스택
- 프로세스와 스레드 1 - 동일인
  - Multi Process, Multi Thread, PCB, 프로세스 상태 전이
  - Interrupt, Context Switching
- 프로세스와 스레드 2 - 동일인
  - WAS, ThreadPool
  - 동시성 이슈란?, 동시성 이슈를 피하는 방법 (스프링에서)
  - Thread Safe 하게 설계하는 방법
- 프로세스 동기화
  - 경쟁 상태(race condition)
  - 임계 구역(ciritical section)
  - 뮤텍스 락(Mutex Locks)
  - 세마포(semaphore)
- 교착상태와 기아상태
  - 교착상태
  - 교착상태 해결 방법
  - 기아상태, Livelock
- CPU 스케줄링 기법
  - 선점, 비선점
  - FIFO, SJF, STCF
  - Round Robin
  - Busy Waiting
  - Multi-Level Feedback Queue
- 블락킹과 논블락킹, 동기식과 비동기식
  - 동기식과 비동기식
  - 블락킹과 논블락킹
- System Call
  - 커널 모드와 유저 모드
  - 인터럽트 vs 시스템콜
- 파일 시스템
  - 파일의 기본 구성
  - 파일 시스템이 필요한 이유
  - 트리 구조 디렉토리
  - 파일 시스템 대신 데이터베이스를 사용하는 이유
- 주소 바인딩과 스와핑
  - 논리 주소 vs 물리 주소
  - 컴파일 타임 바인딩, 적재 타임 바인딩, 실행 타임 바인딩
  - 스와핑
- 메모리 할당과 단편화
  - 고정 분할, 가변 분할
  - 메모리 할당 알고리즘(최초 적합, 최적 적합, 최악 적합)
  - 외부 단편화, 내부 단편화
- 페이징과 세그멘테이션
  - 페이징, 세그멘테이션
  - 페이징 스와핑
- 페이지 교체 알고리즘
  - OPT, FIFO
  - LRU, NUR
  - LFU, MFU, SCR
- RAID
  - RAID 사용 이유
  - RAID 에서 쓰이는 3가지 기술
  - RAID 종류와 특징
- 가상 머신, 가상 메모리
  - 가상 머신과 가상머신을 사용하는 이유
  - 가상 메모리 이점, 원리
  - 요구 페이징

### **데이터베이스**

#### 🔗 [질문 노드 바로 가기](https://github.com/omnireader0/Tech-Interview-Question/blob/main/Question/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EC%A7%88%EB%AC%B8%EC%A0%95%EB%A6%AC.md)

#### ✍ 요약

- RDBMS vs NoSQL
  - RDBMS 와 NoSQL 차이
  - RDBMS 에서 서버 확장하는 방법(Master and Slave)
- ElasticSearch
  - 검색엔진, 검색시스템, 검색서비스
  - 검색시스템 구성요소
  - 색인과 역색인
  - 검색기 품질
  - 관계형 데이터베이스와의 차이점
  - 엘라스틱서치 주요 API
- Transaction
  - 트랜잭션을 사용하는 이유
  - ACID
  - 트랜잭션 격리 수준
  - 트랜잭션 격리 수준을 설정할 때 발생 하는 문제점들
- Redis
  - Redis
  - Look Aside Cache, Write Back
  - CAP
- DB Lock
  - Lock 의 종류와 단위
  - 블로킹(Blocking)
  - 데드락(Deadlock)
- 정규화, 반정규화
  - 이상 현상
  - 정규화와 반정규화
- MySQL Architecture
  - MySQL 엔진
  - 스토리지 엔진
  - 핸들러 API
  - MySQL 스레딩 구조
  - 메모리 할당 및 사용 구조
  - 쿼리파서, 전처리기, 옵티마이저, 실행엔진
  - 스레드풀, 트랜잭션 지원 메타데이터
- Index, Hint
  - 순차 I/O, 랜덤 I/O
  - 쿼리 튜닝의 목적
  - B-Tree Index, Hash Index
  - MySQL 에서 B-tree 를 사용하는 이유
  - 인덱스 레인지 스캔, 인덱스 풀 스캔
  - 클러스터링 인덱스, 논 클러스터링 인덱스
  - MySQL 에서 PK 를 인조키로 사용하고 Auto_Increment 를 사용하는 이유
- 동시성 제어
  - 동시성 제어를 하지 않을 시 발생하는 문제점
  - 동시성 제어 방법
- 스키마(Schema)
  - 스키마 3계층과 3계층으로 나누어 사용하는 이유
  - 테이블 vs 스키마
- DB 클러스터링, 리플리케이션
  - 클러스터 사용 장점과 구현 방법
  - 리플리케이션, 리플리케이션 래그
  - 파티셔닝
  - 샤딩
- ConnectionPool
  - 커넥션 풀 개수 설정 방법
  - 커넥션 풀 동작원리(HikariCP)
  - 커넥션 풀의 장점

