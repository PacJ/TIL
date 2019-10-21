# 함수와 일급 객체(first-class object)

일급객체는 해당 조건을 만족시켜야한다.

1. 무명의 리터럴로 생성할 수 있다: 런타임에 생성이 가능하다.
   * 무명의 리터럴은 반드시 어던가에 할당해야한다.
   * 할당을 해야하기때문에 런타임에 생성이되는것이다.
2. 변수나 자료 구조(객체, 배열 등)에 저장할 수 있다.
3. 함수의 매개 변수에게 전달할 수 있다.
4. 함수의 결과값으로 반환할 수 있다.

* 함수는 이 모든조건을 만족시켜 일급 객체이다. 값이기에 가능하다.

* 객체와 동일하게 사용할 수 있다

  * 객체는 값이므로 함수도 값과 동일하게 취급할 수 있다.

  > **함수형 프로그래밍**
  >
  > 함수형 프로그래밍은 순수 함수와 보조 함수의 조합으로 외부 상태를 변경하는 부수 효과를 최소화하여 불변성(Immutability)을 지향하는 프로그래밍 패러다임이다.



## 함수 객체의 프로퍼티

* **함수 객체는 일반객체가 없는 추가적인 프로퍼티가있다(일반객체의 프로퍼티는 다 가지고 있음)**

* 모든 함수 객체는 일반 객체에 없는 arguments와 length프로퍼티를 가지고있다(JavaScript엔진한테 바인딩 받는다). length를 가지므로 유사 배열 객체이다.

* arguments는 함수의 모든 인수를 저장한다.

* 함수의 length property는 매개 변수의 개수.

* arguments 의 length property는 인수의 개수.

* 브라우저 콘솔에서 console.dir method로 함수 객체 내부를 볼수 있다.

  ```
  function square(number) {
    return number * number;
  }
  
  console.dir(square);
  ```

   ![img](https://poiemaweb.com/assets/fs-images/17-1.png) 

* 가변 인자 함수: 인수가 몇개가 들어와도 된다.

* 콜백함수를 사용하려면 함수가 일급객체가 되어야한다(JS는 함수가 일급객체)



#### arguments 프로퍼티

* 함수 객체의 arguments 프로퍼티 값은 arguments 객체이다.

* arguments 객체는 함수 호출시 전달된 인수들의 정보를 담고 있는 iterable(순회 가능한) 유사 배열 객체이며 함수 내부에서 지역 변수처럼 사용한다.

  * 함수 외부에서 사용 불가능하다.
  * arguments 객체속 Symbol(Symbol.iterator)프로퍼티가 객체를 순회 가능한 자료 구조인 이터러블로 만든다.

* 함수의 선언된 매개변수의 개수보다 인수를 많이 전달되었을때 암묵적으로 arguments 객체의 프로퍼티로 보관된다.

* arguments 객체는 매개변수의 개수를 확정할 수 없는 가변 인자 함수를 구현할 떄 유용하다.

  ```
  function sum() {
    let res = 0;
  
    // arguments 객체는 length 프로퍼티가 있는 유사 배열 객체이므로 for 문으로 순회할 수 있다.
    for (let i = 0; i < arguments.length; i++) {
      res += arguments[i];
    }
  
    return res;
  }
  
  console.log(sum());        // 0
  console.log(sum(1, 2));    // 3
  console.log(sum(1, 2, 3)); // 6
  ```

* arguments 객체는 배열 형태로 parameter 정보를 담고 있지만 실제 배열이 아닌 유사 배열이다.
  * 유사배열객체: length property를 가진 객체로 for문으로 순회 가능한객체
* 유사 배열 객체는 배열이 아니므로 배열 메소드를 사용하면 에러가 발생한다.



#### length property

* 함수 객체에서는 매개변수의 개수를 나타낸다.
* arguments 객체에서는 인수의 개수를 가리킨다.



#### name property

* ES6에서 표준이 되었다.
* ES5에서는 익명 함수(이름없는 함수)의 name프로퍼티는 빈 문자열 값이지만 ES6에서는 함수 객체를 가리키는 변수이름을 값으로 갖는다.