# FrontEnd 질문
---
Attribute와 Property의 차이에 대해 설명해주세요.

1. 시맨틱 마크업에 대해 설명해주세요.
    - 이름에 맞게 html을 태그를 사용하는 것 문자를 쓸때는 p태그, 입력을 받을때는 input태그를 사용하는 등의 느낌
2. script 태그에서 Async와 Defer의 차이에 대해 설명해주세요.
    - 둘다 html에서 script를 실행시키는 경우 html파싱을 멈추지 않음
    - js를 백그라운드에서 다운받으며 실행은 DOM트리가 구성된 이후 실행
    - async는 파일의 다운이 끝나면 실행 ( 페이지와 완전 독립적으로 실행 )
    - → 방문자 수 카운터, 광고관련 스크립트같은 독립적인 기능을 구현할 때 사용하면 좋다.
    - defer는 파일의 다운이 끝나고 DOM이 준비되면 실행

3. 자바스크립트는 무슨 언어인가요?
   - 자바스크립트는 논블로킹 싱글스레드언어입니다.
   - 이게 가능한 이유는 이벤트 루프 때문입니다.
   - 싱글스레드지만 비동기 함수들을 만나면 (setTimeout, Promise등) 해당 함수들을 Web Api로 넘김
   - 이후 setTimeout은 태스크큐, promise는 마이크로태스크큐에 있다가
   - 콜스택이 비워질 때 추가되게 함