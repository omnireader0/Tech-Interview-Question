## 파일

- 논리적인 저장 단위
- 레코드 혹은 블록 단위로 비휘발성 보조기억장치에 저장된다

(전원이 끊어진 상황에서도 정보들을 영구히 보존할 수 있다

프로그램과 자료로 나누어진다)

`프로그램` : 소스 프로그램 , 목적 프로그램으로 나누어 진다

`자료` : 숫자 문자 이진수 등 저장할 수 있는 모든 것이 자료가 된다

### 파일의 속성

- 이름
- 식별자
- 타입
- 위치
- 크기
- 보호 여부
- 시간 , 날짜

### 파일의 구조

`필드` : 데이터 항목

`레코드` : 대상과 관련된 필드들의 집합

## 파일 시스템

![파일시스템](https://user-images.githubusercontent.com/42866800/160276136-aa3af75e-0aeb-423b-ba94-149f97c4f8b3.png)

- 파일 , 파일의 메타데이터 , 디렉터리 정보를 관리한다
- 운영체제 , 데이터 , 프로그램이 파일을 저장하고 접근하기 위한 기법을 제공하는 시스템
- 데이터나 프로그램을 디스크에 쓰고 읽을 수 있게 해주는 프로그램
- 파일과 디스크 블록간 연결작업 처리
    - 메모리는 바이트 단위로 읽어들일수 있지만 디스크는 바이트 단위로 읽어 들일수 없는 구조이다

### 파티션

- 저장공간을 독립적인 영역으로 나누어 사용할 수 있도록 정의한 규약
- 하나의 물리적 디스크 안에 여러 파티션을 두는 경우가 일반적
- 여러 물리적 디스크를 하나의 파티션으로 구성하기도 한다

![디렉토리와 파티션](https://user-images.githubusercontent.com/42866800/160276152-988ad836-a3b0-4cd9-8910-39edb483a6f1.png)

## 디렉토리

- 하나의 파일시스템에서 서로 연관된 파일들을 한곳에 체계적으로 저장될 수 있도록 한다
- 디스크에 저장되어 있는 파일들을 보다 효율적으로 관리하기 위해 사용

### 트리 구조 디렉터리

![트리 구조 디렉토리](https://user-images.githubusercontent.com/42866800/160276176-212d5759-cf37-4ca1-bb5f-e1586c0326f6.png)

- DOS, Windows, UNIX 등의 운영체제에서 사용되는 디렉터리 구조이다.
- 각 디렉터리는 서브디렉터리나 파일을 가질 수 있다.
- 서로 다른 디렉터리 내에 동일한 이름의 파일이나 디렉터리를 생성할 수 있다.
- 디렉터리의 생성과 파괴가 비교적 용이하다.
- 디렉터리의 탐색은 포인터를 사용하며, 경로명은 절대 경로명과 상대 경로명을 사용한다.

## 왜 파일 시스템을 쓰지 않고 DBMS를 만들어냈을까

### 데이터의 형식이나 내용을 프로그램과 상관없이 쉽게 변형가능

- 데이터의 무결성을 유지하기 어렵다
- 무결성 - 데이터가 얼마나 정확한다

### 프로그램이 데이터 파일에 종속된다

- 프로그램이 새로운 데이터 항목을 추가하거나 수정이 필요한 경우
- 다른 프로그램도 기능과 상관없이 프로그램을 수정해야 한다
- 예) 파일 경로를 바꾸면 작동이 안되는 프로그램

### 두가지 프로그램이 하나의 데이터를 공유할 수 있다

- 하지만 동시 접근이 허용되지 않는다
- 스케줄러를 통해 관리되어야 한다

### 참고

[https://vmilsh.tistory.com/388](https://vmilsh.tistory.com/388)

[https://vmilsh.tistory.com/388](https://vmilsh.tistory.com/388)

[https://rebro.kr/181](https://rebro.kr/181)

[https://jess2.tistory.com/86](https://jess2.tistory.com/86)

[https://luv-n-interest.tistory.com/555](https://luv-n-interest.tistory.com/555)

[https://luv-n-interest.tistory.com/555](https://luv-n-interest.tistory.com/555)

[https://moolgogiheart.tistory.com/tag/목적코드](https://moolgogiheart.tistory.com/tag/%EB%AA%A9%EC%A0%81%EC%BD%94%EB%93%9C)

[https://untitledtblog.tistory.com/59](https://untitledtblog.tistory.com/59)

[https://operatingsystems.tistory.com/entry/OS-File-System-1](https://operatingsystems.tistory.com/entry/OS-File-System-1)
