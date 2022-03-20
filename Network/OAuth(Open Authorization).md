# OAuth(Open Authorization)

사용자가 가입된 서비스의 API에 접근하기 위해서는 사용자로부터 권한을 위임 받기 위해서 고안된 기술

- 서비스 APi 예시: Google peoples api, Gmail API, Google Calendar API, YouTube Analytics API

## 일반로그인과 다른점

- 사용자로그인에 필요한 정보(아이디, 비밀번호)를 직접 저장하고 관리하지 않음
- 아이디, 비밀번호 없이 어떻게? -> 다른서비스(구글, 네이버, 카카오)에서 인증(로그인) 후 다른서비스에서 사용자에 대한 정보를 제공 받음아서 사용자를 특정함
- OAuth는 로그인에 필요한 인증 뿐만아니라 인가도 동시에 들어가 있는 행위

  | 종류                 | 내용                                                        |
  | -------------------- | ----------------------------------------------------------- |
  | 인증(Authentication) | 유저가 누구인지 확인하는 절차, 회원가입하고 로그인 하는 것. |
  | 인가(Authorization)  | 유저에 대한 권한을 허락하는 것.                             |

## OAuth 버전변화

### OAuth1.0 -> OAuth1.0a

OpenID등 인증만을 위한 기능이 아닌 인증과 인가를 모두 사용할 목적으로 만들어졌으나 보안적인 문제로 OAuth1.0a이 나옴

- 세션 고정 공격(session fixation attack)
  > https://en.wikipedia.org/wiki/Session_fixation

### OAuth1.0a -> Oauth2.0

앱어플리케이션에서 사용하기 어려운점, 복잡한 절차, 구현의 어려움, 복잡한 절차로 인한 연산의 부담 등을 보완하여 OAuth2.0이 나옴

- OAuth1.0a Access Token 발급 과정

  <img src="https://oauth.net/core/diagram.png" style="margin: 5px 0px" height="400px">

  1. Request Token의 요청과 발급

  ```http
  POST /request?b5=%3D%253D&a3=a&c%40=&a2=r%20b HTTP/1.1
        Host: example.com
        Content-Type: application/x-www-form-urlencoded
        Authorization: OAuth realm="Example",
                        oauth_consumer_key="9djdj82h48djs9d2",
                        oauth_token="kkk9d7dh3k39sjv7",
                        oauth_signature_method="HMAC-SHA1",
                        oauth_timestamp="137131201",
                        oauth_nonce="7d8f3e4a",
                        oauth_signature="djosJKDKJSD8743243%2Fjdk33klY%3Dc2&a3=2+q"
  ```

  2. 사용자 인증 페이지 호출
  3. 사용자 로그인 완료
  4. 사용자의 권한 요청 및 수락
  5. Access Token 발급
  6. Access Token을 이용해 서비스 정보 요청

### Oauth2.0에서 변경된점

- 웹 애플리케이션이 아닌 애플리케이션 지원 강화
- HTTPS를 사용하여 HMAC-SHA1와 같은 암호화를 사용하지 않음
- Siganature 단순화 정렬과 URL 인코딩이 필요 없음
  oauth인증중 oauth_signature이외의 파라미터를 정렬하고 base64로 인코딩 해야했음
- Access Token의 Life-time(유효기간)을 지정 할 수 있도록 함

- Authorization Sever: 인증을 관리하고 있는 서버

## OAuth2.0

### 관련용어

| 용어                       | 역할                                                                                           |
| -------------------------- | ---------------------------------------------------------------------------------------------- |
| Resource Owner(사용자)     | 보호된 리소스에 대한 액세스 권한을 을 가진 소유자, 사람인 경우 최종사용자                      |
| Resource Server(구글)      | 액세스 토큰을 사용하여 보호된 리소스에 대한 응답하는 서버                                      |
| Authorization Server(구글) | Client에게 Resource Server에 접근가능하도록 인증, 인가정보를 담은 access token을 발급하는 서버 |
| Client(내사이트)           | Resource Owner를 대신하여 권한을 받고 리소스를 요청하는 응용프로그램, 사이트                   |

### 사용 과정

```bash
     +--------+                               +---------------+
     |        |--(A)- Authorization Request ->|   Resource    |
     |        |                               |     Owner     |
     |        |<-(B)-- Authorization Grant ---|               |
     |        |                               +---------------+
     |        |
     |        |                               +---------------+
     |        |--(C)-- Authorization Grant -->| Authorization |
     | Client |                               |     Server    |
     |        |<-(D)----- Access Token -------|               |
     |        |                               +---------------+
     |        |
     |        |                               +---------------+
     |        |--(E)----- Access Token ------>|    Resource   |
     |        |                               |     Server    |
     |        |<-(F)--- Protected Resource ---|               |
     +--------+                               +---------------+
```

### 등록(Client Registration)

resource server의 자원을 사용하고자 하는 client가 사전에 승인을 받아두는 것

#### 필수 항목

- ClientID: 애플리케이션 식별
- ClientSecret: 비밀번호
- Authorized redirect URIs: 권한 부여중 Authorization code를 전달받을 Client의 주소
- ClientID과 ClientSecret은 Authorization Server에서 발급 하며 Authorized redirect URIs은 client가 입력

### 인가(Authorization)

- 인가를 진행하는 Grant Type에는 4가지가 있으며 가장 기본적인 Authorization Code을 중심으로 설명
- `Resource Owner`가 `Resource Server`의 자원을 `Client`에서 사용하고자 할떄 `Client`를 `Authorization Server`가 인가해주는 과정

```bash
     +----------+
     | Resource |
     |   Owner  |
     |          |
     +----------+
          ^
          |
         (B)
     +----|-----+          Client Identifier      +---------------+
     |         -+----(A)-- & Redirection URI ---->|               |
     |  User-   |                                 | Authorization |
     |  Agent  -+----(B)-- User authenticates --->|     Server    |
     |          |                                 |               |
     |         -+----(C)-- Authorization Code ---<|               |
     +-|----|---+                                 +---------------+
       |    |                                         ^      v
      (A)  (C)                                        |      |
       |    |                                         |      |
       ^    v                                         |      |
     +---------+                                      |      |
     |         |>---(D)-- Authorization Code ---------'      |
     |  Client |          & Redirection URI                  |
     |         |                                             |
     |         |<---(E)----- Access Token -------------------'
     +---------+       (w/ Optional Refresh Token)
```

1. Resource Owner가 Client에게 Resource Server의 자원을 요청
2. Resource Owner가 Client의 Resource Server에 접근을 허용을 위한 주소를 Resource Owner에게 전송

   - Authorization Server는 Resource Owner가 로그인했는 지를 확인하여 로그인 진행
   - 로그인 예시

      <img src="./OAuth/login-screen.png" style="margin: 5px 0px" height="200px">
      
      버튼의 링크 주소: https://authorization.server/?client_id=1&scopre=B,C&redirect_uri=http://client/callback

3. `Authorization Server`는 전송된 ClientID, ClientSecret, redirectURIs가 사전에 등록된 것과 일치하는지 확인
4. `Authorization Server`는 `Resource Owner`에게 `Client`에 부여하고자 하는 자원의 목록을 확인하는 메세지 전송
5. Authorization code(임시비밀번호) 전송
   - `Authorization Server`는 `Resource Owner`에게 header에 "Location: https://client/callback?code=3"를 전송
   - Location을 통하여 `Resource Owner`는 `Client`로 이동하면서 code=3이라는 Authorization code를 획득
6. `Client`는 Authorization code를 사용하여 `Authorization Server`에게 access token발급을 요청
   - 요청주소 예시: https://authorization.server/token?grant_type=authorization_code&code=3&redirect_uri=https://client/callback&client_id=1&client_secret=2
7. `Authorization Server`는 요청의 각 파라미터 확인 및 각 파라미터 내용이 담긴 access token을 생성하여 `Client`에게 전송

### 토큰갱신(refresh token)

`access token`은 만료기간이 존재하여 만료된 이후에는 사용이 불가능 하며 `access token`을 재발급 받아야함

- `access token`만 발급하는 경우도 있고, `refresh token`까지 발급하는 경우도 있음

#### refresh token 포함된 프로세스

```bash
  +--------+                                           +---------------+
  |        |--(A)------- Authorization Grant --------->|               |
  |        |                                           |               |
  |        |<-(B)----------- Access Token -------------|               |
  |        |               & Refresh Token             |               |
  |        |                                           |               |
  |        |                            +----------+   |               |
  |        |--(C)---- Access Token ---->|          |   |               |
  |        |                            |          |   |               |
  |        |<-(D)- Protected Resource --| Resource |   | Authorization |
  | Client |                            |  Server  |   |     Server    |
  |        |--(E)---- Access Token ---->|          |   |               |
  |        |                            |          |   |               |
  |        |<-(F)- Invalid Token Error -|          |   |               |
  |        |                            +----------+   |               |
  |        |                                           |               |
  |        |--(G)----------- Refresh Token ----------->|               |
  |        |                                           |               |
  |        |<-(H)----------- Access Token -------------|               |
  +--------+           & Optional Refresh Token        +---------------+
```

#### refresh token 요청 예시

```http
POST /token HTTP/1.1
Host: oauth2.googleapis.com
Content-Type: application/x-www-form-urlencoded

client_id=your_client_id&
client_secret=your_client_secret&
refresh_token=refresh_token&
grant_type=refresh_token
```

#### refresh token 응답 예시

```JSON
{
  "access_token": "1/fFAGRNJru1FTz70BzhT3Zg",
  "expires_in": 3920,
  "scope": "https://www.googleapis.com/auth/drive.metadata.readonly",
  "token_type": "Bearer"
}
```

### 그밖의 인가(Authorization)방법

- Implicit: Authorization code는 생략하고 바로 access token을 발급받음
- Resource Owner Password Credentials: `Resource Owner`의 아이디, 비밀번호를 `Client`직접 전달 받아 access token을 발급
- Client Credentials: `Resource Owner`가 `Authorization Server`에서 직접 access token을 발급 받고 `Client`에 전달

#### Implicit

- JavaScript와 같은언어를 사용하여 브라우저에서 구현되어 SPA와 앱에 적합함
- 클라이업트는 `Authorization Server`의 요청을 수신 가능하도록 상호작용이 가능해야함
- `Client` 인증과정이 없으며 리디렉션 URI에 의존
- `Resource Owner`의 동일한 장치에 있는 다른 응용 프로그램에 노출될 수 있음
- 발급과정
  ```bash
      +----------+
      | Resource |
      |  Owner   |
      |          |
      +----------+
            ^
            |
          (B)
      +----|-----+          Client Identifier     +---------------+
      |         -+----(A)-- & Redirection URI --->|               |
      |  User-   |                                | Authorization |
      |  Agent  -|----(B)-- User authenticates -->|     Server    |
      |          |                                |               |
      |          |<---(C)--- Redirection URI ----<|               |
      |          |          with Access Token     +---------------+
      |          |            in Fragment
      |          |                                +---------------+
      |          |----(D)--- Redirection URI ---->|   Web-Hosted  |
      |          |          without Fragment      |     Client    |
      |          |                                |    Resource   |
      |     (F)  |<---(E)------- Script ---------<|               |
      |          |                                +---------------+
      +-|--------+
        |    |
        (A)  (G) Access Token
        |    |
        ^    v
      +---------+
      |         |
      |  Client |
      |         |
      +---------+
  ```

### Resource Server의 자원 사용하기 위한 API요청

#### http를 사용한 요청

`query parameter`과 `Authorization: Bearer`두가지 방법이 있으며 Bearer를 사용하는것이 표준화되고 안전한 방법으로 권장함

- access_token을 query string parameter에 담아서 요청

  ```http
    GET https://www.googleapis.com/drive/v2/files?access_token=<access_token>
  ```

- 헤더의 Authorization: Bearer를 사용하여 access_token을 전송

  ```http
    GET /drive/v2/files HTTP/1.1
    Host: www.googleapis.com
    Authorization: Bearer <access_token>
    https://developers.google.com/calendar/api/v3/reference
  ```

#### API사용시 유의사항

- access token을 서버로 전송할 때는 반드시 https(TLS)를 이용.

  비밀번호인 access token이 노출을 막기위해

- 구글 같은 몇몇 서버스의 경우 api를 호출하기 전에 api를 활성화.
- Bearer token: oauth를 위하여 고안된 인증표준으로 header, payload, signature 3가지로 구성되어 있어야함

  jwt를 access token으로 사용할수 있으나 bearer 표준을 준수하지 못할시 oauth에서 사용불가

## QnA

## References

> https://opentutorials.org/module/3668\
>
> https://opentutorials.org/course/3405
>
> https://datatracker.ietf.org/doc/html/rfc6749
>
> https://developers.google.com/identity/protocols/oauth2#scenarios
>
> https://datatracker.ietf.org/doc/html/rfc6750
>
> https://gist.github.com/egoing/cac3d6c8481062a7e7de327d3709505f
>
> https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=jmjm223&logNo=221483149513
>
> https://velog.io/@aaronddy/%EC%9D%B8%EC%A6%9DAuthentication%EA%B3%BC-%EC%9D%B8%EA%B0%80Authorization
>
> https://oauth.net/core/diagram.png
>
> https://datatracker.ietf.org/doc/html/rfc5849
>
> https://developers.google.com/identity/protocols/oauth2/web-server#httprest_4
>
> https://jsonobject.tistory.com/369
>
> https://cheese10yun.github.io/oauth2/
