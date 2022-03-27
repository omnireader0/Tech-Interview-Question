# Scheduling

**다중 프로그래밍(multi-prgramming)**

- 여러 프로세스가 시스템에 존재
- 자원을 할당 할 프로세스 선택= 스케줄링
- 자원 관리

**자원 관리**

1. 시간 분할(time sharing) 관리

- 하나의 자원을 여러 스레드들이 번갈아 가며 사용. 예) 프로세서(CPU). CPU에는 한번에 하나의 프로세스
- ex) process scheduling

2. 공간 분할(space sharing) 관리

- 하나의 자원을 분할하여 동시 사용
- ex) memory

**스케줄링의 목적**

- 성능 향상
- 목적에 맞는 지표를 고려하여 스케줄링 기법 선택

**성능의 지표**

- reponse time: 작업 요청으로부터 응답을 받을 때까지의 시간
- throughput(작업 처리량): 단위 시간 동안 완료된 작업의 수
- resource utilization(자원 활용도): 주어진 시간 동안 자원이 활용된 시간

**스케줄링 기준(Criteria)**

- 기준= 스케줄링 기법이 고려하는 항목(지표?)
- 프로세스의 특성: I/O-bounded or compute-bounded
- 시스템 특성: Batch or Interactive system
- 프로세스 긴급성(urgency)
- 프로세스 우선순위(priority)

**CPU burst vs I/O burst**

- burst time은 스케줄링의 중요 기준 중 하나
- CPU burst= CPU 사용 시간
- I/O burst= I/O 대기 시간
- 프로세스 수행=CPU 사용+ I/O 대기
- I/O-bounded= I/O burst > CPU burst. I/O burst가 프로세스 성능 결정
- compute-bounded= CPU burst > I/O burst. CPU burst가 프로세스 성능 결정

![https://blog.kakaocdn.net/dn/Qaz0k/btrszlI3VcS/W0oROd5viBTKrZiGj1D6yk/img.png](https://blog.kakaocdn.net/dn/Qaz0k/btrszlI3VcS/W0oROd5viBTKrZiGj1D6yk/img.png)

---

**CPU 스케줄러란?**

준비 큐에 있는 프로세스에 대해 CPU할당하는 방법

**Scheduling Policy(정책)**

1. 선점 vs 비선점

preemptive scheduling, Non-preemptive scheduling

2. 우선순위

priority

**Non-preemptive scheduling(= 자원을 뺏을 수 X)**

- 할당 받을 자원을 스스로 반납할 때까지 사용.
- 장점: context-switching이 적음
- 단점: 평균 응답 시간 증가, 우선순위 역전 현상(우선순위가 높아도 앞에서 끝날 때까지 대기)

**Preemptive scheduling(= 자원을 뺏을 수 O)**

- 장점: 응답성 높다.
- ex) time-sharing system, real-time system 등에 적합
- 단점: 빈번한 context-switching-> overhead가 큼

**Priority**

프로세스의 중요도

1. static priority(정적 우선순위)

- 프로세스 생성시 우선순위 결정되고 불변
- 구현 쉽고, overhead 적음
- 시스템 환경 변화 대응 어려움

2. dynamic priority(동적 우선순위)

- 프로세스 상태 변화에 따라 우선순위 변경
- 구현이 복잡. 우선순위 재계산-> overhead가 큼
- 시스템 환경 변화 유연 대응

스케줄링 5가지

- FCFS
- SJF
- SRT
- Round Robin
- Priority Scheduling

---

**1. FCFS(First Come First Service)= 선착순 알고리즘**

- Non-preemptive scheduling
- 스케줄링 기준: 도착시간(ready queue 기준). 먼저 도착 프로세스 먼저 처리
- scheduling overhead가 낮다. CPU가 계속 일할 수 있다.
- Batch sysytem(일괄처리)에 적합, interactive system에 부적합
- 단점: . 긴 평균 응답시간
    
    Convoy effect
    

**convoy effect**

하나의 수행시간이 긴 프로세스에 의해 다른 프로세스들이 긴 대기시간을 갖게 되는 현상(대기시간>>실행시간)

![https://blog.kakaocdn.net/dn/ZlUeL/btrsqC0b9ku/LSCdjgbwx9EeqpK47wDuxk/img.png](https://blog.kakaocdn.net/dn/ZlUeL/btrsqC0b9ku/LSCdjgbwx9EeqpK47wDuxk/img.png)

---

**SPN(Shorest Process Next)= burst time이 가장 작은 프로세스 먼저 처리하자!**

- Non-preemptive scheduling. 자원 뺏길 수 X
- 스케줄링 기준: burst time
- burst time이 가장  프로세스 먼저 처리
    
    작은
    
- SJF(Shortest Job First) scheduling
- ex) 소량 상품 전용 계산대

![https://blog.kakaocdn.net/dn/c6nkYf/btrsveLhyeX/PLOuE0qXb3YC591ppQCdx1/img.png](https://blog.kakaocdn.net/dn/c6nkYf/btrsveLhyeX/PLOuE0qXb3YC591ppQCdx1/img.png)

**장점:**

- 평균 대기시간(WT) 최소
- 시스템 내 프로세스 수 최소화
- 스케줄링 부하 감소. 메모리 감소-> 효율 향상
- 많은 프로세스 빠른 응답 시간 제공

**단점:**

- starvation(기아) 현상 발생= 무한대기
- BT가 긴 프로세스는 자원을 할당 받지 못 할 수 있음(Aging으로 해결. HRRN)
- 정확한 실행시간 알 수 없음. BT 예측 기법 필요

---

**SRTN(Shortest Remaining Time Next)= 남은 시간 적은 프로세스 먼저!**

- SPN 변형
- preemtive scheduling. 잔여 실행 시간이 더 적은 프로세스가 ready 상태가 되면 선점 됨.
- 장점: SPN 극대화(평균 대기시간 최소화, 시스템 내 프로세스 최소화)
- 단점:

1. 프로세스 생성 시, BT 예측 필요

2. 잔여 실행 시간 추적 필요-> overhead

3. context switching overhead

4. 구현 비현실적

---

**RR(Round-Robin)= 돌려가며 사용**

- preemptive scheduling
- 스케줄링 기준: 도착시간. 먼저 도착한 프로세스 처리(FCFS와 동일)
- 
    
    자원 사용 제한 시간(time quantum)이 존재
    
- 프로세스는 할당 시간이 지나면 자원 반납
- 특점 프로세스의 자원 독점() 방지
    
    monopoly
    
- 단점: context switching overhead가 큼
- interactive system, Time sharing system에 적합

**Time quantum**

- 시스템 성능을 결정하는 핵심
- Very large(infinite)-> FCFS
- Very small-> processor sharing

사용자는 모든 프로세스가 각각의 프로세서 위에서 실행되는 것처럼 느낌. High context switch overhead

![https://blog.kakaocdn.net/dn/sIZEb/btrswXbaAvt/SjVHpNc1msZPEMpYdEOHfk/img.png](https://blog.kakaocdn.net/dn/sIZEb/btrswXbaAvt/SjVHpNc1msZPEMpYdEOHfk/img.png)

---

**MLQ와 MFQ**

이전 SPN, SRTN, HRRN의 단점인 BT예측 overhead를 해결

**MLQ(Multi Level Queue)**

- ready queue가 여러 개 가짐
- 각각의 큐마다 작업 또는 우선순위 배정
- 최초 배정 된 큐는 고정. 큐 이동 못함.
- 각각의 큐 자신만의 스케줄링 기법 사용
- 큐 사이에는 우선순위 기반의 스케줄링 사용(각각 큐가 우선순위가 다르다)

**MLQ의 단점**

- 우선순위 낮은 큐는 여전히 starvation 현상 발생 가능
- 여러 개 큐 관리 등 스케줄링 overhead 발생
- 큐 고정. 시스템 변화 적응 어려움

![https://blog.kakaocdn.net/dn/cXiv2g/btrsA6rpByI/NGB3iIQEo99FYkpnOP0mck/img.png](https://blog.kakaocdn.net/dn/cXiv2g/btrsA6rpByI/NGB3iIQEo99FYkpnOP0mck/img.png)

---

**MFQ(Multi Level Feedback Queue)**

- MLQ와의 차이: 프로세스의 큐간 이동이 허용
- Dynamic priority
- Feedback을 통해 우선순위 조정
- 프로세스에 대한 사전 정보 없이 SPN, SRTN, HRRN 기법 효과

**MFQ 특성**

- Dynamic priority
- Preemptive scheduling

![https://blog.kakaocdn.net/dn/dbzcku/btrsAcd7HUC/Iip8Yjzoq6IJk5ikIKfVs0/img.png](https://blog.kakaocdn.net/dn/dbzcku/btrsAcd7HUC/Iip8Yjzoq6IJk5ikIKfVs0/img.png)

**MFQ 변형**

- **각 ready queue마다 시간 할당량을 다르게 배정 가능**

ex) 중요한 프로세스 time quantum= infinite, 덜 중요 time quantum= 2ms

- **큐 이동 기준이 되는 정책/전략 선택 가능**

ex) 입출력 위주 프로세스(I/O bounded)들은 상위 레벨 큐로 이동(우선순위 높임)

- 프로세스가 block될 때 상위 큐로 진입하게 함.

- 평균 응답 시간 줄임? I/O bounded는 CPU 잠깐 쓰고 나옴. 입출력 작업 분산 시킴

ex) 대기 시간이 지정된 시간 초과한 프로세스들은 상위 레벨 큐로 이동

- aging 기법

**MFQ의 단점**

- 큐 이동, 큐 관리-> 스케줄링 overhead 큼
- 여전한 starvation 문제(낮은 우선순위 큐)