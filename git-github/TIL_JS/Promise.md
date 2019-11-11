# Promise

## 프로미스란

* 자바스크립트는 비동기 처리를 위한 하나의 패턴으로 콜백 함수를 사용한다.
* 전통적인 콜백 패턴은 가독성이 나쁘고 비동기 처리 중 발생한 에러의 예외 처리가 곤란하고 여러개의 비동기 처리 로직을 한꺼번에 처리하는 것도 한계가 있다.
* xhr를 쓰는일은 적고, promise를 많이 쓴다.
* ES6에서 비동기 처리를 위한 또 다른 패턴으로 프로미스(Promise)를 도입하였다.
* Promise는 전통적인 콜백 패턴의 단점을 보완하고, 비동기 처리 시점을 명확하게 표현한다.



## 콜백 패턴의 단점

#### 콜백 헬

* 동기식 처레 모델(Synchronous processing model)은 직렬적으로 task를 수행한다.

* 태스크는 순차적으로 실행되어 작업이 수행 중이면 다음 태스크는 대기한다.

* 서버에서 데이터를 가져와 화면에 표시하는 task를 수행할 때, 서버에 데이터를 요청하고 데이터가 응답될 때까지 이후 태스크들은 블로킹된다.

   ![synchronous](https://poiemaweb.com/img/synchronous.png) 

* 비동기식 처리 모델(Asynchronous processing model/Non-Blocking processing model)은 태스크가 종료되지 않은 생태에도 대기하지 않고 다음 태스크를 실행한다.