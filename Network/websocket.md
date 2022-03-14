- 웹소켓과 Socket.io

  웹소켓 연결 과정
  HTTP 프로토콜과 마찬가지로, 80번 포트를 사용하여 웹 서버에 연결하고,
  Upgrade: WebSocket 헤더 등과 함께 랜덤한 키를 생성해서 웹 서버에 요청한다.
  이 키로 토큰을 발행하고, 브라우저에게 응답한다.
  이로써, WebSocket HandShaking이 이루어진다.

  그 다음부터는 Protocol Overhead 방식으로 데이터를 주고 받는다.
  Protocol Overhead 방식은 80번 포트의 TCP 커넥션 하나만 이용한다.
  그렇기 때문에 방화벽이 있는 환경에서도 무리없이 사용이 가능하다.

  그리고 스키마도 Http와 당연히 다르다.
  예를 들면, 우리가 흔히 사용하는 http://www.google.com 부분에서 http를 URI스키마 라고 부른다.
  여기서 WebSocket은 http가 아닌, ws를 사용한다. 따라서, 사용하려면, ws://www.google.com 이런 방식으로 선언해야 한다.
  추가로, 암호화된 소켓은 ws -> wss 로 바꾸면 된다.

  간단한 예제로,
  ```
  var socket = new WebSocket(“ws://localhost:16020”);

  socket.onmessage = function (e) { 
      console.log(e.data); 
  };

  socket.onopen = function (e) {
      console.log(“open”);
  };

  socket.onclose = function (e) {
      console.log(“close”);
  };

  socket.send(“message”);
      socket.close();
  ```

  위 코드에서 new WebSocket("스키마://호스트:포트") 이 부분은
  웹소켓을 사용을 위해 인스턴스를 생성해서 웹서버와 연결한다.
  그 후에 onmessage(메시지 받았을 때), onopen(소켓 연결), onclose(소켓 연결 종료)등 여러 메소드들은 사용할 수 있다.

  Socket.io는 JavaScript를 이용하여 브라우저 종류에 상관없이 실시간 웹을 구현할 수 있으며,
  WebSocket, FlashSocket(Flash가 설치된 브라우즈에서 사용할 수 있는 통신 방식 = 알 필요 없음), 
  AJAX Long Polling, AJAX Multi part Streaming, IFrame, JSONP Polling을 하나의 API로 추상화한다.

- Polling = Real-Time 웹을 위한 기법
  - 브라우저가 일정한 주기마다 서버에 HTTP 요청을 보내는 방식
    단점 : 요청 주기가 짧아지게 되면 서버에 부담이 되며, 반대로 주기가 길면, 실시간 성능이 떨어짐

- Long Polling = Polling의 단점을 보완한 방식
  - 기본적으로 Polling 방식과 유사하지만, 이벤트 처리 기반 즉, 클라이언트가 요청을 보내면, 대기중인 서버는 그 즉시 응답을 해서 실시간성이 매우 좋다.
  - Response는 Event가 발생할 때 하므로, Long Polling 이라고 불린다. 하지만, 연결이 많아지면 데이터량이 증가한다.





