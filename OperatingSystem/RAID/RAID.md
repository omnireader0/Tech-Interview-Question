# RAID

**RAID Architecture란?**

- Redundant Array of Independent Disks: 복수 배열 독립 디스크
- 여러 개 물리 disk를 하나의 논리 disk로 사용

![Untitled](RAID%20be8c1/Untitled.png)

**RAID를 사용하는 이유**

- 성능 향상
    - Access speed(접근 속도)
    - Reliability(안전성)

---

**RAID0**

- 접근 속도에 초점
- Disk striping
    - block을 일정한 크기로 나누어 각 disk에 나누어 저장
- 모든 disk에 입출력 부하 균등 분배
    - 병렬 접근(parallel access)
    - 접근 속도 향상
- 단점
    - 한 disk 장애 시, 데이터 손실 발생(Low Reliability, 안전성 낮다)

![Untitled](RAID%20be8c1/Untitled%201.png)

---

**RAID1**

- 안전성에 초점
- Disk mirroring
    - 동일한 데이터를 mirroring disk에 중복 저장
- 최소 2개의 disk로 구성
- 단점
    - 한 disk 장애 생겨도 데이터 손실 X
    - 가용량: (전체 disk 용량)/2

![Untitled](RAID%20be8c1/Untitled%202.png)

---

**RAID3**

- RAID0+ parity disk
    - Byte 단위로 분할 저장
    - 모든 disk에 입출력 부하 균등 분배(block A를 읽으려면 A0, A1, A2, A3 동시 접근)
- 한 disk에 장애 발생 시, parity 정보를 이용하여 복구
- write 시 parity 계산이 필요
- 단점
    - disk에 write 할 때마다 parity 정보도 parity disk에 저장→ overhead가 발생
    - write 몰리면 병목현상 발생 가능
    - parity disk에 장애가 발생하면?

![Untitled](RAID%20be8c1/Untitled%203.png)

**parity란?**

- 디스크 장애 시 데이터를 재 구축하는데 사용할 수 있는 사전에 계산된 값
- 디스크 하나가 장애가 날 경우 Parity 영역를 이용해서 장애 난 디스크의 데이터를 복구한다.

---

**RAID4**

- RAID3와 유사, 단 Block 단위로 분산 저장
- 각 Block을 독립적으로 접근 할 수 있다. 단, Disk 간 균등 분배가 안될 수 있음.
- 한 disk에 장애 발생 시, parity 정보를 이용하여 복구
- write 시 parity 계산이 필요

![Untitled](RAID%20be8c1/Untitled%204.png)

---

**RAID5**

- RAID3, RAID4의 parity disk 장애 발생 문제 해결
- 접근 속도+ 안전성에 초점. 두마리 토끼!
- RAID4와 유사, 단 parity도 나눠서 저장하겠다!
    - 디스크의 5개 블록 중 4개는 데이터를 저장하는데 쓰고 나머지 하나는 Parity 영역으로 둔다.
    - parity disk의 병목현상 문제 해결
- 단 디스크 2개 이상 고장나면 복구할 수 없다.

![Untitled](RAID%20be8c1/Untitled%205.png)

---

**참고**

[https://www.youtube.com/watch?v=omDkxSyol98](https://www.youtube.com/watch?v=omDkxSyol98)

[https://anmj.tistory.com/12#--%--�%-A%A-�%-A%B-�%-D��%-D%B-�%--%--](https://anmj.tistory.com/12#--%25--%EC%25-A%25A-%ED%25-A%25B-%EB%25-D%BC%EC%25-D%25B-%ED%25--%25--)

[https://hihighlinux.tistory.com/64](https://hihighlinux.tistory.com/64)