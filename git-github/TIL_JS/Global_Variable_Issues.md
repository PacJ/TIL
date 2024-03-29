# 전역 변수의 문제점

## 변수의 생명 주기

#### 지역 변수의 생명 주기

* 변수는 선언으로 생성되고 할당으로 값을 가지며, 언젠가는 소멸한다.
* 변수에 생명 주기(Life cycle)가 없으면 프로그램을 종료하지 않는한 영원히 메모리 공간을 차지하게 되므로 전역 변수의 생명주기는 애플리케이션의 생명 주기와 같다.
* 변수는 선언된 위치에 생성되고 소멸한다, 함수 내부에 선언된 지역 변수는 함수가 호출되면 생성되고 함수가 종료되면 소멸한다.
* 함수를 호출하면 함수 몸체에 다른 문들이 실행되기 이전에 함수 내부에 변수가 호이스팅되어 먼저 선언되고(undefined로 초기화), 다른 문들이 실행된다. 함수를 종료하면 변수가 소멸된다.
* **변수 호이스팅은 스코프 단위로 동작한다.**



#### 전역 변수의 생명 주기

* 전역 코드는 명확한 호출없이 실행된다.

  * 함수 호출처럼 실행하는 특별한 진입점(entry point)이 없다.

  * 코드가 로드 되자마자 해석되고 실행된다.

    > **진입점(entry point)**
    >
    > C나 Java로 코드를 실행하면 가장 먼저 main함수가 호출된다. 이 main함수는 프로그램이 시작되는 지점으로 진입점/시작점이라 한다.

* 함수는 몸체의 마지막문 또는 return문이 실행되면 종료되지만, 전역 코드는 마지막 문이 실행되고 나서 종료한다.

* var 키워드로 선언한 변수는 **전역 객체**의 프로퍼티가 된다.

  * 브라우저 환경에서는 전역 객체는 window이므로 window의 프로퍼티가 된다, node.js에서는 global의 프로퍼티가 된다.
  * 전역 객체 window는 웹페이지 종료 전까지 유효하다.
  * 전역 변수는 스코프체인의 최상위에 있어 검색 속도가 느리다.
    * 전역 변수를 참조할때 스코프체인을 타고 최상위까지 올라가야되므로.
    * 성능에 악영향을 준다.
  
* 함수를 짧게 만들어서 변수의 생명주기를 짧게한다.

  * 가독성을 높이고 함수를 단순하게 해준다.
  * 단순한 함수들을 조합해서 사용하는것이 이상적이다.



#### 전역 변수의 문제점

* **암묵적 결합**
  * 전역 변수를 사용하는 것은 코드 어디에서든 사용하겠다는 것이다.
  * 모든 코드가 전역 변수를 참조하고 변경할 수 있는 **암묵적 결합(implicit coupling)** 을 허용한다.
  * 변수의 유효 범위가 크면 클 수록 코드의 가독성은 나빠지고 의도치 않게 상태가 변경될 수 있는 위험성도 높아진다.



* **긴 생명 주기**
  * 전역 변수는 생명 주기가 길기 때문에, 상태를 변경할 수 있는 시간도 길고, 모든 함수가 참조할 수 있기에 상태가 변경될 기회도 많다.
  * 메모리 리소스도 오랜 기간동안 소비한다.
  * var 키워드는 변수의 중복 선언을 허용하여 생명 주기가 긴 전역 변수는 이름이 중복될 가능성이 있다. 중복되면 의도치 않은 재할당이 이루어진다.
  * 지역 변수는 생명주기가 짧아 상태를 변경할수있는 시간도 짧고 기회도 적다, 메모리 리소스도 짧은 기간만 소비하고, 오류가 발생할 확률이 적다.



* **스코프 체인 상에서 종점에 존재**
  * 스코프 체인 상에서 종점이 존재하는 문제가 있다.
  * 변수를 검색할 때 전역 변수가 가장 마지막에 검색되는것이다.
  * **전역 변수의 검색 속도가 가장 느리다.**



* 네임 스페이스 오염
  * 자바스크립트에서 가장 큰 문제점 중의 하나는 파일이 분리되어 있어도 하나의 전역 스코프를 공유한다는 것이다.
  * 파일 내에 동일한 이름의 변수나 함수가 같은 스코프내에 존재할 경우 예상치 못한 결과가 생길수 있다.



## 전역 변수 사용 억제 방법

​	**전역 변수를 반드시 사용해야할 이유가 없다면 지역 변수를 사용해야한다.**

​	**변수의 스코프는 좁을수록 좋다.**



#### 즉시 실행 함수(IIFE)로 감싸는 방법

* 함수의 정의와 동시에 호출하는 즉시 실행 함수는 한번만 호출된다.
* **모든 코드를 즉시 실행 함수로 감싸면 모든 변수는 즉시 실행 함수의 지역 변수가 된다.**



#### 네임 스페이스 객체

* 전역에 네임 스페이스(Namespace) 역할을 담당할 객체를 생성하고 전역 변수처럼 사용하고 싶은 변수를 프로퍼티로 추가한다.

* 전역 변수를 전역 객체 하나속에 모두 담는다.

  ```
  var MYAPP = {}; // 전역 네임 스페이스 객체
  
  MYAPP.person = {
    name: 'Lee',
    address: 'Seoul'
  };
  
  console.log(MYAPP.person.name); // Lee
  ```



#### 모듈 패턴

* 모듈 패턴은 클래스를 모방해 관련이 있는 변수와 함수를 모아 즉시 실행 함수로 감싸고 하나의 모듈을 만든다.

* 특징으로는 전역 변수의 억제, 캡슐화까지 구현하는 것이다.

* **캡슐화는 정보를 외부에 노출시키지 않고 숨기는 것이다.**
  
  * 정보 은닉(information hiding)이라고도 한다.
  
  ```
  var Counter = (function () {
    // private 변수
    // JS에서는 private을 지원하지 않아서 클로저로 기능을 구현해야한다.
    var num = 0;
  
    // 외부로 공개할 데이터나 메소드를 프로퍼티로 추가한 객체를 반환한다.
    return {
      increase() {
        return ++num;
      },
      decrease() {
        return --num;
      }
    };
  }());
  
  // private 변수는 외부로 노출되지 않는다.
  console.log(Counter.num); // undefined
  
  console.log(Counter.increase()); // 1
  console.log(Counter.increase()); // 2
  console.log(Counter.decrease()); // 1
  console.log(Counter.decrease()); // 0
  ```
  
* Java는 public,private,protected 등 접근 제한다(Access modifier)를 사용한다.

* public으로 선언된 데이터/method는 외부에서 접근 가능하지만 private은 외부에서 접근할 수 없고 내부에서만 사용한다.

* JavaScript는 이런 접근 제한자를 제공하지 않는다.

* 모듈 패턴은 전역 네임 스페이스의 오염을 막고 한정적으로 캡슐화를 구현한다.

* 클로저 때문에 즉시실행함수 속 변수 num은 실행 후 사라져야하는데 남아서 사용할 수 있게된다.



