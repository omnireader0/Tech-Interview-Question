# CORS(Cross-Origin Resource Sharing)

- CORS의 개념과 CORS로 인한 이슈 발생 구분
- CORS 동작 방식 - preflight request 간단히 알면 될 것 같아요.
- 심화 질문 : CORS 이슈 해결 방법 -> 필요한 분만 보시면 될 것 같습니다.

## CORS와 SOP

### CORS (Cross-Origin Resource Sharing)

교차 출처 리소스 공유는 추가 HTTP 헤더를 사용하여**, 한 출처(Origin)에서 실행 중인 웹 애플리케이션이 다른 출처(cross-origin)의 선택한 자원에 접근할 수 있는 권한을 부여**하도록 브라우저에 알려주는 정책입니다.

(한마디로 서로 다른 도메인 간 자원 공유하는 것을 말합니다.)

여기서 

##### origin (출처)

origin은 protocol, host, port로 구성

예를 들어서, https://github.com:443 주소가 있습니다.

| protocol | host       | port |
| -------- | ---------- | ---- |
| https:// | github.com | 443  |

**cross- origin** **(다른 출처)**

https://a.com:80

https://b.com:80

protocol, host, port 중 1개라도 다르면 cross-origin입니다.

### SOP

같은 출처에서만 리소스 공유할 수 있다는 규칙

##### same-origin (같은 출처)

protocol, host, port 동일하면 same-origin이다.

### CORS 등장 배경

CORS, SOP 이런 정책이 존재하는 이유는 

기본적으로 동일한 출처에 대해 통신하는 것을 규칙으로 합니다.(SOP)

그 이유는 서로 다른 출처 간 통신을 제약하지 않으면 보안에 문제가 생길 수 있기 때문입니다.

다른 출처의 리소스를 불러와야 하는 경우, 그 출처에서 올바른 CORS 헤더를 포함한 응답을 반환해줘야 하며, CORS는 안전한 교차 출처 요청 및 데이터 전송을 지원합니다.(CORS는 최소한의 리소스 안전 장치) 

### CORS와 CORS 이슈를 구분하자!

CORS는 서로 다른 도메인 간 자원 공유하는 매커니즘이며, **CORS 자체가 에러는 아닙니다.**

CORS 이슈는 **SOP(동일 출처 정책)에 의거해 다른 출처의 리소스를 사용할 때 경고가 생기고, 이를 해결하기 위해 CORS를 사용하여 접근을 허용하도록 설정**함으로써 해결할 수 있습니다.



## CORS 동작과 이슈 해결 방법

### CORS 동작 원리

##### Prefilght request

브라우저는 본 요청을 보내기 전에 예비 요청을 먼저 보내고, 요청의 유효성을 검사한다.

> 실제 요청 보내도 안전하지 판단하기 위해 사전에 보내는 요청
>
> OPTIONS 메서드로 요청하며 CORS를 허용하는지 확인
>
> CORS가 허용된 웹 서버라면 사용 가능한 리소스를 헤더에 담아 응답

![image](https://user-images.githubusercontent.com/93963499/158049107-f9eea86f-84dc-49af-9ba8-86f26e35f317.png)

### CORS 이슈 해결 방법

CORS 정책 위반으로 에러 발생했을 때 해결 방법

##### Access- Control-Allow-Origin 응답 헤더 셋팅

- 서버측 응답에서 접근 권한을 주는 헤더를 추가하여 해결

~~~javascript
app.use((req, res, next) => {
  res.header("Access-Control-Allow-Origin", "*"); // 모든 도메인
  res.header("Access-Control-Allow-Origin", "https://example.com"); // 특정 도메인
});
~~~

이런식으로 서버(서버 엔진 설정에 추가)에서 Access-Control-Allow-Origin 헤더에 알맞은 값을 셋팅하는 방법이 정석이나 불편합니다.

따라서 소소코드 내에서 셋팅하는 방법(Spring, Django 등)이 있습니다.

##### 스프링 셋팅 방법

https://wonit.tistory.com/572

## QnA



### Reference

https://evan-moon.github.io/2020/05/21/about-cors/

https://velog.io/@jesop/SOP%EC%99%80-CORS

https://ingg.dev/cors/