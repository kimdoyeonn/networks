- HTTP는 HTML 문서와 같은 리소스들을 가져올 수 있도록 해주는 프로토콜
- **클라이언트-서버 프로토콜**
	- 수신자(보통 웹 브라우저) 측에 의해 요청이 초기화되는 프로토콜
- 하나의 완전한 문서는 텍스트, 레이아웃 설명, 이미지, 비디오, 스크립트 등 불러온(fetched) 하위 문서들로 재구성

![](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview/fetching_a_page.png)

![](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview/http-layers.png)
- 신뢰 가능한 전송 프로토콜이라면 이론상으로는 무엇이든 사용할 수 있으나 [[TCP]] 혹은 암호화된 TCP 연결인 [[TLS]]를 통해 전송
- HTTP의 확장석 덕문에 오늘날 하이퍼텍스트 문서 뿐만 아니라 이미지와 비디오, HTML 폼 결과 같은 내용을 서버로 POST하는 것에도 사용
- 웹 페이지를 갱신하기 위한 문서의 일부를 가져오는데 사용

## HTTP 기반 시스템의 구성요소
- HTTP의 요청은 하나의 개체, 사용자 클라이언트에 의해 전송됩니다. 대부분의 경우 사용자 클라이언트는 웹 브라우저이지만 무엇이든 될 수 있습니다. 그 예로 검색 엔진 인덱스를 위해 웹을 돌아다니는 봇이 있습니다.
![](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview/client-server-chain.png)
- 요청과 응답 사이에는 여러 개체들이 있는데, 예로 다양한 작업을 수행하는 게이트웨이 또는 캐시 역할을 하는 프록시 등이 있습니다.
- 실제로는 브라우저와 요청을 처리하는 서버 사이에는 좀 더 많은 컴퓨터들이 존재합니다.(라우터, 모뎀 등) 하지만 웹의 계층적인 설계 덕분에 이들은 네트워크와 전송 계층 내로 숨겨집니다.
### 클라이언트: 사용자 에이전트
- 사용자를 대신하여 동작하는 모든 도구로, 주로 브라우저에 의해 수행
- 브라우저는 항상 요청을 보내는 개체. 서버가 될 수 없음
- 웹 페이지를 표시하기 위해, 브라우저는 페이지의 HTML 문서를 가져오기 위한 요청을 전송한 뒤, 파일을 구문 분석하여 실행해야 할 스크립트, 페이지 내 포함된 하위 리소스(보통 이미지, 비디오)를 잘 표시하기 위한 레이아웃 정보(CSS)에 대응하는 추가적인 요청을 가져옵니다. 그런 뒤에 브라우저는 완전한 문서인 웹 페이지를 표시하기 위해 리소스들을 혼합합니다. 브라우저에 의해 실행된 스크립트는 이후 단계에서 좀 더 많은 리소스들을 가져올 수 있으며 브라우저는 그에 따라 웹 페이지를 갱신하게 됩니다.
- 웹 페이지는 하이퍼텍스트 문서로 표시된 텍스트의 일부는 사용자가 사용자 에이전트를 제어하고 웹 을 돌아다닐 수 있도록 새로운 웹 페이지를 가져오기 위해 실행될 수 있는 링크입니다. 브라우저는 HTTP 요청 내에서 이런 지시사항들을 변환하고 HTTP 응답을 해석하여 사용자에게 명확한 응답을 표시합니다.

### 웹 서버
- 통신 채널의 반대편에서 클라이언트에 대한 문서를 제공하는 서버
- 사실상 논리적으로 단일 기계
- 로드 밸런싱 혹은 다른 컴퓨터(캐시, DB 서버, e-커머스 서버 등)들의 정보를 얻고 완전하게 혹은 부분적으로 문서를 생성하는 소프트웨어의 복잡한 부분을 공유하는 서버들의 집합일수있기 때문
- 반드시 단일 머신일 필요는 없지만, 여러 개의 서버를 동일한 머신 위에서 호스팅할 수 있음

### 프록시
- 웹 브라우저와 서버 사이에 수많은 컴퓨터와 머신이 HTTP 메시지를 이어 받고 전달
- 이러한 컴퓨터/머신들은 대부분 전송, 네트워크 혹은 물리 계층에서 동작하며, 성능에 상당히 큰 영향을 주지만 HTTP 계층에서는 이들이 어떻게 동작하는지 눈에 보이지는 않음
- 이런 컴퓨터/머신 중에서도 애플리케이션 계층에서 동작하는 것들을 일반적으로 프록시라고 부름
- 프록시는 눈에 보이거나 보이지 않을 수 있으며(프록시를 통해 요청이 변경되거나 변경되지 않는 경우) 다양한 기능들을 수행

- 캐싱(캐시는 공개 또는 비공개될 수 있음 ex 브라우저 캐시)
- 필터링(바이러스 스캔, 유해 컨텐츠 차단)
- 로드 밸런싱(여러 서버가 서로 다른 요청을 처리하도록 허용)
- 인증(다양한 리소스에 대한 접근 제어)
- 로깅(이력 정보를 저장)

# HTTP
- 간단합니다.
	- 사람이 읽을 수 있으며 간단하게 고안되었음
- 확장가능합니다.
	- HTTP 헤더는 HTTP를 확장하고 실험하기 쉽게 만들어줌
	- 클라이언트와 서버가 새로운 헤어의 시멘틱에 대해 간단한 합의만 한다면, 언제든 새로운 기능을 추가할 수 있음
- 상태는 없지만 세션은 있습니다.
	- Stateless
	- HTTP 쿠키는 상태가 있는 세션을 만들도록 해줌
- HTTP와 연결
	- 연결은 전송 계층에서 제어되므로 근본적으로 HTTP 영역 밖임
	- HTTP는 연결될 수 있도록 하는 근본적인 전송 프로토콜을 요청하지 않음
	- 다만 신뢰할 수 있거나 메시지 손실이 없는 연결을 요구함
	- 인터넷 상의 가장 일반적인 전송 프로토콜 중에서 TCP는 신뢰할 수 있으며 UDP는 그렇지 않음
	- 그러므로 HTTP는 연결이 필수는 아니지만 연결 기반인 TCP 표준에 의존
	- 클라이언트와 서버가 HTTP를 요청/응답으로 교환하기 전에 여러 왕복이 필요한 프로세스인 TCP 연결을 설정해야함
	- HTTP/1.0: 각 요청/응답에 대해 별도의 TCP 연결을 염 -> 여러 요청을 연속해서 보내는 경우에는 단일 TCP 연결을 공유하는 것보다 효율적이지 못함
	- HTTP/1.1: 파이프라이닝 개념과 지속적 연결 개념을 도임
	- HTTP/2.0: 연결을 더 지속되고 효율적으로 유지하는데 도움이 되도록, 단일 연결 상에서 메시지를 다중전송(multiplex)

## HTTP로 제어할 수 있는 것
### 캐시
- HTTP로 문서가 캐시되는 방식을 제어
- 서버는 캐시 대상과 기간을 프록시와 클라이언트에 지시 가능
- 클라이언트는 저장된 문서를 무시하라고 중간 캐시 프록시에 지시 가능
### origin 제약사항을 완화
- 스누핑과 다른 프라이버시 침해르 막기 위해, 브라우저는 웹 사이트 간의 엄격한 분리르 강제
- 동일한 origin으로부터 온 페이지만이 웹 페이지의 전체 정보에 접근 가능
- 제약사항이 서버에 주는 부담을 HTTP 헤더로 완화할 수 있음
### 인증
- 기본 인증은 HTTP를 통해 WWW-Authenticate 또는 유사 헤더를 사용해 제공되거나 HTTP 쿠키를 사용해 특정 세션을 설정하여 이루어질 수 있음
### 프록시와 터널링
- 서버 혹은 클라이언트는 종종 인트라넷에 위치하며 다른 개체들에게 그들의 실제 주소를 숨기기도 함
- 이런 경우 HTTP 요청은 네트워크 장벽을 가로지르기 위해 프록시를 통해 나가게됨
- 모든 프록시가 HTTP 프록시는 아님
### 세션
- 쿠키 사용은 서버 상태를 요청과 연결하도록 해줌

## HTTP 흐름
1. TCP 연결을 연다. 요청을 보내거나 응답을 받는데에 사용
	- 클라이언트는 새 연결을 열거나, 기존 연결을 재사용하거나, 서버에 대한 여러 TCP 연결을 열 수 있음
2. HTTP 메시지를 전송
3. 서버에 의해 전송된 응답을 읽어들임
4. 연결을 닫거나 다른 요청들을 위해 재사용
- HTTP 파이프라이닝이 활성화되면 첫 응답을 완전히 수신할 때까지 기다리지 않고 여러 요청을 보낼 수 있음
- HTTP 파이프라이닝은 오래된 소프트웨어와 최신 버전이 공존하는 기존의 네트워크 상에서 구현하기 어렵다는게 입증되어 프레임 안에서 보다 활발한 다중 요청을 보내는 HTTP/2로 교체되고 있음

## HTTP 메시지
- HTTP/1.1과 초기 HTTP 메시지는 사람이 읽을 수 있음
- HTTP/2에서 새로운 이진구조인 프레임 안으로 임베드되어, 헤더의 압축과 다중화와 같은 최적화를 가능케함, HTTP 메시지의 일부만이 2 버전의 HTTP 내에서 전송된다고 해도 각 메시지의 의미들은 변하지 않으며 클라이언트는 HTTP/1.1 요청을 가상으로 재구성함. 그러므로 HTTP/1.1 포맷 내에서도 HTTP/2를 이해할 수 있음

### Requests
![](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview/http_request.png)
- HTTP 메서드: 클라이언트가 수행하고자 하는 동작을 정의한 동사(GET, POST, PUT, PATCH, DELETE) 혹은 OPTIONS, HEAD 같은 명사
- 가져오려는 리소스 경로: 프로토콜(https://), 도메인(naver.com), 또는 TCP 포트(80) 인 요소를 제거한 리소스의 URL
- HTTP 프로토콜의 버전
- 서버에 대한 추가 정보를 전달하는 선택적 헤더
- POST와 같은 몇 가지 메서드를 위한, 전송된 리소스를 포함하는 응답의 본문과 유사한 본문
### Responses
![](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview/http_response.png)
- HTTP 프로토콜의 버전
- 요청의 성공 여부와, 그 이유를 나타내는 상태 코드
- 아무런 영향력이 없는, 상태 코드의 짧은 설명을 나타내는 상태 메시지
- 요청 헤더와 비슷한 HTTP 헤더
- 선택 사항으로 가져온 리소스가 포함되는 본문

## HTTP 기반 API
- XMLHttpRequest API: user agent와 서버간에 데이터를 교환하는데 사용될 수 있음
- 서버-전송 이벤트: 서버가 전송 메커니즘으로 HTTP를 사용하여, 클라이언트로 이벤트를 보낼 수 있도록 하는 단방향 서비스
	- 클라이언트는 EventSource 인터페이스를 사용하여 연결을 맺고 이벤트 핸들러를 설정
	- 클라이언트 브라우저는 HTTP 스트림으로 도착한 메시지를 적절한 Event 객체로 자동 변환하여, 알려진 경우 해당 이벤트 type에 대해 등록된 이벤트 핸들러로 전달하거나 특정 유형의 이벤트가 설정되지 않은 경우에는 onmessage 이벤트 핸들러로 전달

[HTTP 개요](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)