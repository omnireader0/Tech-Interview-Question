# HTTP 와 HTTPS

## HTTP (Hyper Text Transfer Protocol)

- html을 전송하는 프로토콜
- 클라이언트와 서버간 데이터를 주고받을 때도 HTTP를 사용한다
- 즉 , 클라이언트와 서버간 데이터를 주고 받기 위한 프로토콜

### HTTP 특징

- HTTP는 TCP/IP 프로토콜 위에서 동작한다
- 클라이언트 서버 구조
    - Request Response 구조
    - 클라이언트와 서버를 분리한다
    - 클라이언트는 서버에 요청을 보내고, 응답을 대기한다
    - 서버가 요청에 대한 결과를 만들어서 응답해 준다
- 무상태 프로코콜(Stateless) 비연결성
    - 서버가 클라이언트의 상태를 보존하지 않는다
    - 클라이언트가 요청할 때 필요한 데이터를 그때그때 담아서 넘겨준다
    - 갑자기 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다
    - 응답서버를 쉽게 바꿀수 있다
    - 서버는 상태를 보존하지 않는다
- HTTP는 기본적으로 서버와 클라이언트의 연결을 유지하지 않는 모델이다
    - 서버 자원을 매우 효율적으로 사용할 수 있다
    - TCP/IP 연결을 새로 맺어야 한다
    - 자원을 받을 때마다 클라이언트와 서버를 연결하고 자원이 해제 되었을떄 연결을 끊는 것은 비효율 적이다
    - HTTP 지속연결 (Persistent Connections)로 문제를 해결한다
    - 서버와 클라이언트가 요청을 보내고 응답을 받는 동안에 연결되어 있는 상태를 유지 한다
    
  ![스크린샷(235)](https://user-images.githubusercontent.com/42866800/156905743-622a2da0-1732-4227-aaef-676473cc14bd.png)

### HTTP 메세지 구조

HTTP 요청 메세지

```java
GET /search?q=hollo&hl=ko HTTP/1.1
HOST:www.google.com
```

http 요청 메세지도 본문에 필요한 body 부분을 가질수 있다

HTTP 응답 메세지

```java
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3423

<html>
	<body>...</body>
</html>
```

HTTP 메시지 구조

```java
start-line 시작 라인

header 헤더

empty line 공백 라인 (CRLF)

message body
```

![스크린샷(237)](https://user-images.githubusercontent.com/42866800/156905756-03d6fdc6-b4d9-4653-8dba-f10bfa39cb51.png)


![HTTP메서드구조](https://user-images.githubusercontent.com/42866800/156905850-9d855a7f-1c49-432c-8608-b2f035c3a690.png)

공식 스펙

```java
HTTP-message = start-line
							 * (header-field CRLF)
								CRLF
								[message-body]
```

### 시작라인

요청 메시지

- start-line = request-line(요청) / status-line(응답)
- request-line = method SP(공백) request-target SP (요청하는 대상) HTTP-version CRLF(엔터)

요청 메세지 - HTTP 메서드

- 종류: GET , POST , PUT , DELETE
- 서버가 수행해야 할 동작 지정
    - `GET` 리소스 조회
    - `POST` 요청 내역 처리
    

```java
GET /search?q=hollo&hl=ko HTTP/1.1
Host: www.google.com
```

요청 메시지 - 요청 대상

- absolute-path[?query] (절대경로[?쿼리])
- 절대경로 = `/` 로 시작하는 경로

```java
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
```

시작라인

요청 메시지 - HTTP 버전

- HTTP Version

```java
GET /search?q=hollo&hl=ko HTTP/1.1
Host: wwww.google.com
```

시작라인

응답 메시지

- start-line = request-line / status-line
- status-line = HTTP-version SP status-code SP reason-phrase CRLF

- HTTP 버전
- HTTP 상태 코드: 요청 성공 , 실패를 나타낸다
    - 200: 성공
    - 400: 클라이언트 요청 오류
    - 500: 서버 내부 오류
- 이유 문구:  사람이 이해할 수 있는 짧은 상태 코드 설명 글 (상태코드에 대한 짧은 설명)

HTTP 헤더

- header-field = field-name `:` OWS field-value OWS (OWS: 띄어쓰기 허용)
- field-name은 대소문자 구문 없음
- value는 대소문자를 구분한다

```java
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
```

```java
HTTP/1.1 200 OK
Content-TYpe: text/html;charset=UTF-8
Content-Length: 3423

<html>
	<body>...</body>
</html>
```

HTTP 헤더의 용도

- HTTP 전송에 필요한 모든 부가정보
- 예) 메시지 바디의 내용 , 메시지 바디의 크기 , 압축 , 인증 , 요청 클라이언트(브라우저) 정보 , 서버 애플리케이션 정보 , 캐시 관련 정보
    - 즉 , 메시지 바디 빼고 필요한 메타 데이터가 전부 들어있다
    
    ```java
    HTTP/1.1 200 OK
    Content-TYpe: text/html;charset=UTF-8
    Content-Length: 3423
    
    <html>
    	<body>...</body>
    </html>
    ```
    
- 표준 헤더가 너무 많음
- 필요시 임의의 헤더도 추가할 수 있다

HTTP 메시지 바디

용도

- 실제 전송할 데이터가 들어있다
- HTML 문서 , 이미지 , 영상 , JSON 등등 byte로 표현할 수 있는 모든 데이터가 전송 가능하다

```java
HTTP/1.1 200 OK
Content-Type: text.html;charset=UTF-8
Content-Length: 3423

<html>
	<body>...</body>
</html>
```

HTTP 결론

단순하고 확장이 가능하다

## HTTP2.0

### HTTP1.1이 느린 이유

- 클라이언트와 서버가 하나의 요청과 하나의 응답을 처리하도로 ㄱ되어 있다
- 클라이언트의 Request 순서와 서버의 응답 순서를 동기화 해야 한다
- http/1.1의 헤더에는 많은 메타 정보들이 저장되어 있다
    - 사용자가 방문한 웹페이지는 다수의 http 요청이 발생하게 도니다
    - 이 경우 매 요청시 마다 중복된 헤더 값을 전송하게 되며
    - 각 도메인에 설정된 쿠키 정보도 매 요청시 마다 헤더에 포함되어 전송한다

### HTTP2.0의 등장

- HTTP/1.1이 느려서 버전을 개선

### HTTP 2.0이 빠른 이유

1. Multiplexed Streams (한 커넥션에 여러개의 메세지를 동시에 주고 받을 수 있음)
2. 요청이 커넥션 상에서 다중화 되므로 HOL(Head Of Line) Blocking 이 발생하지 않음
3. Stream Prioritization (요청 리소스간 의존관계를 설정)
4. Header Compression (Header 정보를 HPACK 압축 방식을 이용하여 압축 전송)
5. Server Push (HTML문서 상에 필요한 리소스를 클라이언트 요청없이 보내줄 수 있음)
6. 프로토콜 협상 메커니즘 - 프로토콜 선택, 예. HTTP / 1.1, HTTP / 2 또는 기타.
7. HTTP / 1.1과의 높은 수준의 호환성 - 메소드, 상태 코드, URI 및 헤더 필드
8. 페이지 로딩 속도 향상

## HTTPS(Hyper Text Transfer Protocol Secure)

- HTTP에 데이터 암호화가 추가된 프로토콜
- HTTP와 다르게 443 번 포트를 사용한다
- 네트워크 상에서 중간에 제3자가 정보를 볼 수 없도록 암호화를 지원한다

### 대칭키 암호화 와 비대칭키 암호화

- 대칭키 암호화
    - 클라잉언트와 서버가 동일한 키를 사용하여 암호화/복호화 진행
    - 키가 노출되면 매우 위험하지만 연산 속도가 빠름
- 비대칭키 암호화
    - 1개의 쌍으로 구성된 공개키와 개인키를 암호화/복호화 하는데 사용
    - 키가 노출되어도 비교적 안전하지만 연산 속도가 느림
    - `공개키` - 모두에게 공개가능한 키
        - 공개키 암호화 - 공개키로 암호화를 진행하면 개인키로만 복호화 할 수 있다
        - 개인키는 나만 가지고 있으므로 나만 볼 수 있다
    - `개인지` - 나만 가지고 알고 있어야 하는 키
        - 개인키로 암호화 하면 공개키로만 복호화 할 수 있다
        - 공개키는 모두에게 공개되어 있으므로 내가 자인증한 정보임을 알려 신뢰성을 보장할 수 있다
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/56255dd8-8292-4871-8b0c-5182dbbb4c23/Untitled.png)
        

### HTTPS 연결과정

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a90f6178-3971-4a63-b460-5643ccebb1a5/Untitled.png)

1. 클라이언트가 서버로 최초 연결 시도를 한다
2. 서버는 공개키를 브라우저에게 응답해 준다
3. 브라우저는 인증서의 유효성을 검사하고 세션키를 발급 받는다
4. 브라우저는 세션키를 보관하고 서버의 공개키로 세션키를 암호화 하여 서버로 전소앟ㄴ다
5. 서버는 개인키로 암호화된 세션키를 복호화 하여 세션키를 얻는다
6. 클라이언트와 서버는 동일한 세션키를 공유하므로 데이터를 전달할 때 세션키로 암호화/복호화를 진행한다

## 결론

- HTTP는 암호화가 추가되지 않았기 때문에 보안에 취약하다
- HTTPS는 안전하게 데이터를 주고 받을 수 있다
- 하지만 HTTPS를 사용하면 암호화/복호화 과정이 필요하기 때무넹 HTTP 보다 속도가 느리다
- HTTPS는 인증서를 발급하고 유지하기 위해 추가 비용이 발생한다
- 개인 정보와 같은 민감한 데이터를 주고 받아야 한다면 HTTPS를 사용
- 노출이 되어도 괜찮은 단순한 정보 조회 등을 처리하고 있다면 HTTP를 사용

참고 - 

[https://mangkyu.tistory.com/98](https://mangkyu.tistory.com/98)

[https://blog.wishket.com/http-vs-https-차이-알면-사이트의-레벨이-보인다/](https://blog.wishket.com/http-vs-https-%EC%B0%A8%EC%9D%B4-%EC%95%8C%EB%A9%B4-%EC%82%AC%EC%9D%B4%ED%8A%B8%EC%9D%98-%EB%A0%88%EB%B2%A8%EC%9D%B4-%EB%B3%B4%EC%9D%B8%EB%8B%A4/)

[https://devlog.oopy.io/bcac7b1c-130f-43b1-ad2e-e2a2db9ab738](https://devlog.oopy.io/bcac7b1c-130f-43b1-ad2e-e2a2db9ab738)

[https://goldfishhead.tistory.com/26](https://goldfishhead.tistory.com/26)
