# 1. HTTP 개관

전 세계의 웹브라우저, 서버, 웹 앱은 모두 HTTP를 통해 서로 대화한다.

이번 장에서 배울 것은 아래와 같다.

- 얼마나 많은 클라이언트와 서버가 통신하는지
- 리소스(웹 콘텐츠)가 어디서 오는지
- 웹 트랜잭션이 어떻게 동작하는지
- HTTP 통신을 위해 사용하는 메시지의 형식
- HTTP 기저의 TCP 네트워크 전송
- 여러 종류의 HTTP 프로토콜
- 인터넷 곳곳에 설치된 다양한 HTTP 구성요소

# 1.1. HTTP: 인터넷 멀티미디어 배달부

HTTP는 전 세계의 웹서버로부터 정보(HTML 페이지, 이미지 파일 등)를 웹 브라우저로 옮겨준다.

HTTP는 신뢰성을 보장하기 때문에 데이터 누락에 대한 걱정을 하지 않아도 된다.

# 1.2. 웹 클라이언트와 서버

HTTP 프로토콜로 의사소통 하는 두개의 주체가 있다. 요청을 하고 응답 받는 쪽을 HTTP 클라이언트, 반대는 HTTP 서버라 한다.

# 1.3. 리소스

웹 서버는 웹 리소스를 관리, 제공한다. 웹 리소스는 웹에 콘텐츠를 제공하는 모든 것을 말한다. 인터넷 검색엔진 역시 리소스다.

## 1.3.1. 미디어 타입

인터넷은 수많은 데이터 타입을 다루기 때문에, HTTP는 웹에서 전송되는 객체에 데이터 포맷 라벨인 MIME 타입을 붙인다. 원래는 이메일간 데이터 타입을 지정하기 위해 사용했지만 워낙 잘 동작해 HTTP에서도 채택했다.

MINE 타입은 주 타입(primary object type)과 부 타입(specific subtype)을 사선으로 구분한다.

- HTML → text/html
- jpeg → image/jpeg

## 1.3.2. URI

통합 자원 식별자(URI, Uniform resource identifier)를 통해 원하는 리소스의 위치를 찾을수 있다.URI에는 URL과 URN 이 있다.

### 1.3.2.1. URL(통합 자원 지시자, uniform resource locator)

특정 서버의 리소스에 대한 구체적인 위치를 서술한다.

크게 세 부분으로 이뤄진 표준 포맷을 따른다.

1. 스킴: 리소스 접근을 위한 프로토콜, 보통 HTTPS 프로토콜(https://)이다.
2. 호스트: 인터넷 주소(www.kakao.com)
3. 리소스 (/images/logo)

예시)

- https://www.kakao.com/index.html → 카카오의 URL
- https://www.naver.com/images/logo.webp → 네이버 로고 URL

### 1.3.2.2. URN(uniform resource name)

이름으로 접근한다.

# 1.4. 트랜젝션

클라이언트 기준으로 요청 명령에 대한 응답 결과 쌍을 HTTP 트랜젝션이라 한다.

## 1.4.1. 메서드

요청이 어떤 행위를 할 것인지 나타낸다. (GET, POST, HEAD, PUT, DELETE, …)

## 1.4.2. 상태 코드

요청에 대한 상태를 나타내는 세자리 숫자(200, 302, 404, …)

## 1.4.2. 웹페이지는 여러 객체로 이뤄질 수 있다.

하나의 웹페이지는 여러 HTTP 트랙젝션을 수행해 얻은 리소스로 만든다.

# 1.5. 메시지

HTTP 메시지는 이진 형식이 아닌 단순한 줄 단위의 텍스트로 사람이 읽고 쓰기 쉽다.

![스크린샷 2023-04-13 오후 8.56.41.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/70becf63-676e-420d-819b-5b970d14b7c9/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-04-13_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_8.56.41.png)

- 시작줄 - 메시지의 첫 줄은 시작줄이다. 요청이라면 무엇을 해야 하는지, 응답이라면 무슨 일이 일어났는지 나타낸다.
- 헤더 - 0개 이상의 헤더 필드로 구성돼 빈 줄로 끝난다. 콜론으로 구분된 하나의 이름과 값으로 구성된다. (빈 줄로 끝나는 것을 헤더 다음에 개행으로 보는 시각도 있다)
- 본문 - 요청, 응답 데이터로 이진 데이터도 사용 가능해 다양한 포멧을 넣을수 있다.

예시

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6e123072-e67a-46fb-890b-4cbd7bcdeb59/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8f62bd3f-15a3-4663-9266-df338d2e213f/Untitled.png)

# 1.6. TCP 커넥션(Transmission Control Protocol)

## 1.6.1. TCP/IP

HTTP는 애플리케이션 계층 프로토콜로, 네트워크 통신의 핵심적인 세부사항에 대해선 신경쓰지 않고 신뢰성 있는 전송 프로토콜인 TCP/IP에게 맡긴다.

TCP는 다음을 제공한다.

- 오류 없는 데이터 전송
- 순서에 맞는 전달
- 조각나지 않는 데이터 스트림

![스크린샷 2023-04-13 오후 9.13.26.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/543b5f1b-03c9-40f1-bc2b-02a056f9d6fe/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-04-13_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.13.26.png)

## 1.6.2. 접속, IP 주소 그리고 포트번호

HTTP 클라이언트가 서버에 메시지를 전송하기 전에 TCP/IP 커넥션을 맺어야 한다. 이때 IP 주소와 포트번호를 사용한다. 

IP와 포트번호를 이용해 다음과 같은 순서를 거쳐 통신한다.

1. 웹브라우저는 서버의 URL에서 호스트 명을 추출한다.
2. 웹브라우저는 서버의 호스트 명을 IP로 변환한다.
3. 웹브라우저는 URL에서 포트번호를 추출한다.
4. 웹브라우저는 웹 서버와 TCP 커넥션을 맺는다.
5. 웹브라우저는 서버에 HTTP 요청을 보낸다.
6. 서버는 웹브라우저에 HTTP 응답을 돌려준다.
7. 커넥션이 닫히면, 웹브라우저는 문서를 보여준다.

## 1.6.3. 텔넷(Telnet)을 이용한 실제 예제

(생략)

# 1.7. 프로토콜 버전

### HTTP/0.9

디자인 결함이 있음. GET 메서드만 지원. MIME 타입, HTTP 헤더 미지원.

### HTTP/1.0

버전 번호, HTTP 헤더, 추가 메서드, 멀티미디어 객체 처리를 추가. 잘 정의된 명세는 아님.

### HTTP/1.0+

“keep-alive” 커넥션, 가상 호스팅 지원, 프락시 연결 지원 등.

### HTTP/1.1

설계의 결함 교정, 성능 최적화.

### HTTP/2.0

앞선 성능 문제를 개선

# 1.8. 웹의 구성요소

### 1. 프락시

클라이언트와 서버 사이에 위치한 HTTP 중재자.

웹 보안, 애플리케이션 통합, 성능 최적화를 위한 구성요소.

클라이언트를 대신해 서버에 접근.

주로 보안을 위해 사용하고 요청과 응답을 필터링하여 위험을 제거함.

### 2. 캐시

많이 찾는 웹페이지나 리소스를 캐시 서버에 보관해 서버의 부하를 덜어줌. 

HTTP 창고 역할을 하는 프락시 서버.

### 3. 게이트웨이

다른 애플리케이션과 연결된 특별한 웹 서버.

주로 HTTP 트래픽을 다른 프로토콜로 변환하기 위해 사용 됨.

![스크린샷 2023-04-13 오후 9.41.21.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b00cce3e-810f-49ef-a563-00254b1bf5cb/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-04-13_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.41.21.png)

### 4. 터널

단순히 HTTP 통신을 전달하기만 하는 특별한 프락시

예시로, 외부에서 요청된 HTTPS를 터널을 통해 사내망으로 들어가고 사내망 안에서는 HTTP로 변환해 전달하는 역할을 할수 있음. 보완 필요.

### 5. 에이전트

자동화된 HTTP 요청을 만드는 준지능적 웹클라이언트.