# JavaScript Event Loop란

### JS Enging
- 엔진은 Memory Heap 과 Call Stack 으로 구성
- ex. 구글의 V8 Engine
- 자바스크립트는 단일 스레드 (sigle thread) 프로그래밍 언어인데, <br>
  이 의미는 Call Stack이 하나라는 의미
- (Memory Heap : 메모리 할당이 일어나는 곳 / Call Stack : 코드가 실행될 때 쌓이는 곳. stack 형태로 쌓임)

### Web API
- 브라우저에서 제공하는 API 로, DOM, Ajax, Timeout 등이 있다
- Call Stack에서 실행된 비동기 함수는 Web API를 호출하고, Web API는 콜백함수를 Callback Queue에 밀어 넣는다

### Callback Queue
- 비동기적으로 실행된 콜백함수가 보관 되는 영역
- Event Loop에서 비동기 함수를 꺼내기 전까지는 계속 Queue방식으로 보관

### 🎉 Event Loop
- 1) Event Loop는 Call Stack과 Callback Queue의 상태를 체크
- 2) Call Stack이 빈 상태가 되면, Callback Queue의 첫번째 콜백을 Call Stack으로 밀어넣는다.
- 3) 그 후 Call stack 에서 비동기 함수를 실행시킴
  (이러한 반복적인 행동을 틱(tick) 이라 부른다.)
