## 웹 소켓
### reference : https://spring.io/guides/gs/messaging-stomp-websocket/

1. 의존성 추가하기 WebSocket
2. Resource Representation Class 만들기 (데이터 직렬화 포맷용 클래스) HelloMessage, GreetingMessage
3. Controller 생성
   1. @MessageMapping의 목적지로 메세지가 보내지면 해당 메소드실행  
   메세지 페이로드는 실매개변수인 객체에 매핑됨
   2. @SendTo에 설정된 엔드포인트의 구독자들에게 리턴타입의 객체가 브로드캐스트됨
4. Config빈 설정
   1. @Configuration 어노테이션으로 빈 등록
   2. @EnabledWebSocketMessageBroker : 메세지 브로커의 지원을 받아, 웹소켓 메세지를 처리함.
      1. configureMessageBroker(String... destinationPrefixes) : WebSocketMessageBrokerConfigurer는 enableSimpleBroker()를 통하여
메모리 기반 브로커를 활성화하는데   
      인수로 전달된 string의 prefix에 대한 엔드포인트에 greeting 메세지를 되돌려준다
      2. setApplicationDestinationPrefixes(String... prefixes) : 컨트롤러에 설정된 @MessageMapping의 prefix를 설정한다.  
      prefix가 /app이고 @MessageMapping("/hello")이면 /app/hello 엔드포인트가 설정된 메소드를 호출한다.
   3. registerStompEndpoint(String... paths)는 해당  경로들을 엔드포인트로 등록하고  
      WebSocket이 이용불가능할 때,  alternate transports가 사용되기 위해 SockJS fallback 옵션들을 활성화한다

   
   
   