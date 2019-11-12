# Promise

## 프로미스란

* 자바스크립트는 비동기 처리를 위한 하나의 패턴으로 콜백 함수를 사용한다.
* 전통적인 콜백 패턴은 가독성이 나쁘고 비동기 처리 중 발생한 에러의 예외 처리가 곤란하고 여러개의 비동기 처리 로직을 한꺼번에 처리하는 것도 한계가 있다.
* 콜백 패턴의 가독성, 비동기 처리, 후속처리, 
* xhr를 쓰는일은 적고, promise를 많이 쓴다.
* ES6에서 비동기 처리를 위한 또 다른 패턴으로 프로미스(Promise)를 도입하였다.
* Promise는 전통적인 콜백 패턴의 단점을 보완하고, 비동기 처리 시점을 명확하게 표현한다.
  * 비동기 처리를 잘해야 처리 속도가 빨라지고 성능이 좋아진다.
* 브라우저는 기본적으로 multi-thread로 돌지만, 자바스크립트 엔진은 call stack이 single-thread다.



## 콜백 패턴의 단점

#### 콜백 헬

* 동기식 처레 모델(Synchronous processing model)은 직렬적으로 task를 수행한다.

* 태스크는 순차적으로 실행되어 작업이 수행 중이면 다음 태스크는 대기한다.

* 서버에서 데이터를 가져와 화면에 표시하는 task를 수행할 때, 서버에 데이터를 요청하고 데이터가 응답될 때까지 이후 태스크들은 블로킹된다.

   ![synchronous](https://poiemaweb.com/img/synchronous.png) 

* 비동기식 처리 모델(Asynchronous processing model/Non-Blocking processing model)은 태스크가 종료되지 않은 생태에도 대기하지 않고 다음 태스크를 실행한다.



#### 에러 처리의 한계

* Error는 caller에게 throw되어 발생한다.

  ```
  try {
    setTimeout(() => { throw new Error('Error!'); }, 1000);
  } catch (e) {
    console.log('에러를 캐치하지 못한다..');
    console.log(e);
  }
  ```

* 화살표함수는 caller가 없어 window가 caller가 되는것과 마찬가지다.
* 비동기 함수인 setTimeout은 console.log문들이 모두 실행 컨텍스트에서 빠진 후에 실행되기 때문에, 에러를 잡을수가 없다.



## Promise의 생성

* Promise 생성자 함수를 통해 인스턴스화한다.
* 비동기 작업을 수행할 콜백 함수를 인수를 받고, 이 콜백 함수는 resolve와 reject 함수를 인자로 받는다.

```
// promise 객체
const promise = new Promise((resolve, reject) => {
  // 비동기 처리를 여기서 한다.
  const random = Math.floor(Math.random() * 10);
  setTimeout(() => {
    if (random >= 5) resolve(random);
    else reject (new Error(`your number is ${random}.`));
  });
});

promise
  .then(res => console.log(res))
  .catch(err => console.log(err));
```

* Promise는 비동기 처리의 상태 정보를 갖는다.

| 상태          | 의미                                       | 구현                                               |
| :------------ | :----------------------------------------- | :------------------------------------------------- |
| pending       | 비동기 처리가 아직 수행되지 않은 상태      | resolve 또는 reject 함수가 아직 호출되지 않은 상태 |
| **fulfilled** | 비동기 처리가 수행된 상태 (성공)           | resolve 함수가 호출된 상태                         |
| **rejected**  | 비동기 처리가 수행된 상태 (실패)           | reject 함수가 호출된 상태                          |
| settled       | 비동기 처리가 수행된 상태 (성공 또는 실패) | resolve 또는 reject 함수가 호출된 상태             |

* Promise 생성자 함수가 인자로 전달받은 콜백 함수는 내부에서 비동기로 작업을 처리한다.
* 비동기 처리 성공시 프로미스는 resolve함수를 호출하며 fullfilled 상태가 되고, 실패시 rejected 상태가 되어 reject 함수를 호출한다.

```
const ajax (method, url, payload) => {
	return new Promise((resolve, reject) => {
		const xhr = new XMLHttpRequest();
		xhr.open(method, url);
		xhr.setRequestHeader('Content-type', 'application/json');
		xhr.send(JSON.stringify(payload));
		
		xhr.onload () => {
		if (xhr.readyState === 200 || xhr.readyState == 201) {
			resolve(xhr.response)
			} else {
			reject(new Error(xhr.status));
			}
		};
	});
};
```



## Promise의 후속 처리 메소드

* Promise로 구현된 비동기 함수는 Promise 객체를 반환하여야한다.
  * Promise로 구현된 비동기 함수를 호출하는 측에서 Promise 객체의 후속 처리 메소드(then, catch)를 통해 처리 결과 또는 에러를 전달받는다.
  * then: 두개의 콜백 함수를 인자로 전달받는다: 첫번째는 성공시 호출, 두번째 함수는 실패시 호출된다.
  * catch:  예외(비동기 처리에서 발생한 에러와 then 메소드에서 발생한 에러)가 발생하면 호출된다. catch 메소드는 Promise를 반환한다. 



## Promise의 에러 처리

* Promise 객체의 후속 처리 메소드로 비동기 처리 결과에 대한 후속 처리를 수행한다.

  ```
  promiseAjax('GET', 'http://jsonplaceholder.typicode.com/posts/1')
    .then(JSON.parse)
    .then(render)
    .catch(console.error);
  ```

* .then의 두번째 콜백 함수도 에러를 처리하지만, .catch와 차이가 있다.
  * .then메소드는 비동기 처리에서 발생한 에러(reject 함수가 호출된 상태)만을 캐치한다.
  * .catch는 비동기 처리와 추가로 .then 메소드 내부에서 발생한 에러도 캐치한다.



## Promise Chaining

*  비동기 함수의 처리 결과를 가지고 다른 비동기 함수를 호출해야 하는 경우, 함수의 호출이 중첩(nesting)이 되어 복잡도가 높아지는 콜백 헬이 발생한다.

* 프로미스는 후고 처리 메소드를 chaining하여 여러 개의 프로미스를 연결하여 사용할 수 있다.

  * 콜백 헬을 해결한다.

* then메소드가 Promise 객체를 반환하도록 하고, 여러개의 then으로 프로미스를 연결하여 사용할 수 있다.

  ```
   const url = 'http://jsonplaceholder.typicode.com/posts';
  
      // 포스트 id가 1인 포스트를 검색하고 프로미스를 반환한다.
      promiseAjax('GET', `${url}/1`)
        // 포스트 id가 1인 포스트를 작성한 사용자의 아이디로 작성된 모든 포스트를 검색하고 프로미스를 반환한다.
        .then(res => promiseAjax('GET', `${url}?userId=${JSON.parse(res).userId}`))
        .then(JSON.parse)
        .then(render)
        .catch(console.error);
  ```

  

## Promise의 정적 메소드

* 4가지 메소드를 제공한다.



#### Promise.resolve/reject

* 두 메소드는 존재하는 값을 Promise로 래핑하기 위해 사용한다.

* Promise.resolve는 인자로 받은 값들을 resolve하는 Promise를 생성한다.

  ```
  const resPromise = Promise.resolve([1, 2, 3]);
  resPromise.then(console.log) // [1, 2, 3]
  
  // 이방식과 동일하게 동작한다.
  const resPromise = new Promise(resolve => resolve([1, 2, 3]));
  resPromise.then(console.log); // [1, 2, 3]
  ```

* Promise.reject는 인자로 받은 값들을 reject하는 Promise를 생성한다.

  ```
  const rejPromise = Promise.reject(new Error('Error!'));
  rejPromise.catch(console.log); // Error: Error!
  
  // 이방식과 동일하게 동작한다.
  const rejPromise = new Promise((resolve, reject) => reject(new Error('Error!')));
  rejPromise.catch(console.log); // Error: Error!
  ```

  

#### Promise.all

* Promise.all method는 Promise가 담겨 있는 배열 등의 이터러블을 인자로 전달 받는다.

* 모든 프로미스를 병렬로 처리하고, 결과를 resolve하는 새로운 Promise를 반환한다.

  ```
  Promise.all([
    new Promise(resolve => setTimeout(() => resolve(1), 3000)), // 1
    new Promise(resolve => setTimeout(() => resolve(2), 2000)), // 2
    new Promise(resolve => setTimeout(() => resolve(3), 1000))  // 3
  ]).then(console.log) // [ 1, 2, 3 ]
    .catch(console.log);
  ```

* 각각의 프로미스가 resolve한 결과를 배열에 담아 resolve하는 새로운 프로미스를 반환한다.

  * 첫번째 프로미스가 resolve한 처리결과부터 차례대로 배열에 담는다.
  * 따라서 처리 순서가 보장된다.

* 프로미스의 처리가 하나라도 실패하면 가장 먼저 실패한 프로미스가 reject한 에러를 reject하는 새로운 프로미스를 **즉시 반환한다.**

  ```
  Promise.all([
    new Promise((resolve, reject) => setTimeout(() => reject(new Error('Error 1!')), 3000)),
    new Promise((resolve, reject) => setTimeout(() => reject(new Error('Error 2!')), 2000)),
    new Promise((resolve, reject) => setTimeout(() => reject(new Error('Error 3!')), 1000))
  ]).then(console.log)
    .catch(console.log); // Error: Error 3!
  ```

  * 세번째 프로미스가 가장 먼저 실패하여 에러가 catch메소드로 전달된다.

* Promise.all 메소드는 전달받은 iterable의 요소가 프로미스가 아닌 경우, Promise.resolve 메소드로 프로미스로 래핑된다.

  ```
  Promise.all([
  	1, // => Promise.resolve(1)
  	2, // => ""(2)
  	3 // => ""(3)
  ]).then(console.log) // [1, 2, 3]
    .catch(console.log);
  ```

* Promise.all 예제:

  ```
  const githubIds = ['jeresig', 'ahejlsberg', 'ungmo2'];
  
  Promise.all(githubIds.map(id => fetch(`https://api.github.com/users/${id}`)))
    // [Response, Response, Response] => Promise
    .then(responses => Promise.all(responses.map(res => res.json())))
    // [user, user, user] => Promise
    .then(users => users.map(user => user.name))
    // [ 'John Resig', 'Anders Hejlsberg', 'Ungmo Lee' ]
    .then(console.log)
    .catch(console.log);
  ```



#### Promise.race

* Promise.all 메소드와 동일하게 이터러블을 인자로 전달 받는다.

* Promise.race는 모든 프로미스를 병령 처리하지 않고, 가장 먼저 처리된 프로미스가 resolve한 결과를 resolve하는 새로운 프로미스를 반환한다.

  ```
  Promise.race([
    new Promise(resolve => setTimeout(() => resolve(1), 3000)), // 1
    new Promise(resolve => setTimeout(() => resolve(2), 2000)), // 2
    new Promise(resolve => setTimeout(() => resolve(3), 1000))  // 3
  ]).then(console.log) // 3
    .catch(console.log);
  ```

* 에러 발생은 Promise.all과 동일하게 처리된다.