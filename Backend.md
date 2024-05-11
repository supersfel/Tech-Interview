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

-

## 프로세스와 스레드
