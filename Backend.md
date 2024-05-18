## HTTP

---

HTTP ( Hyper text transper protocol )
웹 프로토콜 중 하나

### HTTP 1.0

- 1 Request 1 connection
- 한번의 요청을 하면 TCP/IP 요청을 끊어버림
- 속도가 매우 느리고 비효율적임
- 한 요청에 담긴 데이터를 패킷이라고 생각해도 된다.
- RTT(rount trip time)이 길수밖에 없다.
- header가 없고 body만 있다.

### HTTP 1.1

- 1 Requeust 1 Response ( conntection을 바로 닫지 않는다 )
- default로 설정되어 있음 ( 문서에 적혀있다.. )
- pipe lining
  - 3개를 보내면 동기적으로 함
- header가 생김
  - content-type : application.json, multipart/form-data
- 대역폭도 늘렸음
- 헤더에 보안쪽 요소도 생겼다.

### HTTP 2.0

- HOL 문제 해결
  - 3개를 다 보내고 3개를 한번에 받음 ( 비동기적으로 렌더링이 가능 )
- 허프만 인코딩
  - HTTP 요청이 가벼워졌다.

## RESTFUL API

- axios 날려보는 과정을 생각하면 끝난다.
- "자원"이라는 것을 활용해서 api 통신을 하는것
- URL params
  - 명사로 사용해야 함
- https method
- 헤더
- body
- HATEOAS
  - id, name, content, \_links에 https요청에 대한 정보가 있음
- STATELESS

## www.naver.com 쳤을때 어떤일이 발생하는가

1. PC에 있는 캐시 폴더를 찾는다.
2. 캐시폴더에 없을때만 브라우저 DNS서버에 URL을 보냄
   1. DNS서버도 단계에 펼쳐서 찾음.
   2. DNS QUERY
      1. root DNS -> .com DNS 이런식으로 진행
3. 브라우저가 IP를 받아옴
4. IP에 해당되는 서버에 TCP연결을 보내고 HTTP요청을 만들어 보내야 함
5. router ( 공유기 )
   1. 내 private ip 와 public ip를 분리를 시켜줌
6. CDN
   1. 컨텐츠 캐싱용 서버
   2. 미국에서 서버가 있어도 동영상 등을 CDN으로 한국에두면? -> 렉이 안걸림
7. Global server load balancer
8. 6,7 번은 헬스체크가 필요하다. ( 진짜 정보랑 차이가 날 수 있으니까 ) TTL이 끝날떄 쯤 데이터를 가져옴
9. nginx가 이것저것 해줌
10. reverse proxy
    1. 서버쪽 private ip를 감싸줌
11. load balancer
12. 데이터 캐싱 등등...
13. 서버는 그에 해당하는 HTML,CSS,JS 파일을 보낸다.
14. 이후는 프론트영역 (^\_^)

## 쿠키 세션 jwt

- STATELESS 한 HTTP에서 STATE를 만들어 주기 위한 수단
- 결국 쿠키와 세션 모두 그냥 하나의 '값'

### 쿠키

- 브라우저 내부에 있는 영역 ( 유효기간을 정할 수 있는 )
- 전달해줄 때 header에 담김
  - set-cookie : key
  - value : id : 4
- 쿠키 저장소에서 헤더에 보낼 저장소와 비교를 해서 원하는 쿠키만 보냄
- 서드파티 쿠키 ( 제 3자 쿠키
  - 웹 페이지의 소유자가 아닌 업체에서 사용할 수 있는 쿠키 )
- 쿠키에 id,pw를 보내면 당연히 취약함 ( 프록시 서버 등이 탈취당하면 )

### 세션

- 그렇다면 id,pw를 서버에서 저장하고 있으면 되지 않는가?
- 쿠키에 세션 id만 보내고 서버에서 저장 ( 세션 id는 쿠키나 로컬스토리지 저장 )
- 결국 세션은 DB다.
- session id 탈취
  - 클라이언트가 로그인을 취소할 수 있음
  - 큰 기업같은 경우 IP를 같이 확인한다.

### 토큰 인증 방식

- id,권한,마지막 로그인날짜, 만료기간 등등 필수적인 것만 들어가야 함
- JWT (header body signature)
- 1(header값이라 예시) / 2(body값이라 예시) / header,body,signature 등등 합쳐서 만듬
- 방식 자체는 쿠키와 똑같기 때문에 탈취 위험이 있음
- 만료기간을 매우 낮게 만듬(3분...5분..)
- 낮은 사용자 경험을 위해 refresh token을 발급
- refresh token은 access token을 갱신하기위한 정보만 있음
- 만약 refresh token도 뺏길때를 대비하여 캐시를 활용하여 이전 로그인 정보를 저장
- a' 이란 만료 토근이 2개 컴퓨터로 들어오면 a'' , a''' 다른 2개의 티켓이 생기게 됨
- a-r키로 저장을 하고 만료된 a가 들어오면 a-r을 지우고 a'-r로 저장을 한후 비교

### OAUTH

- 결론은 전문적인 보안을 담당해주는 OAUTH를 이용한다.

### 웹 스토리지

- 로컬 스토리지
- 세션 스토리지
