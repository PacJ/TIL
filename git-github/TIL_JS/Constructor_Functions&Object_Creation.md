# 생성자 함수에 의한 객체 생성

## Object 생성자 함수

* new 연산자와 함께 Object생성자 함수를 호출하면 빈 객체를 생성하여 반환.

  * 생성후 프로퍼티/메소드를 추가해 객체를 완성.

* 함수를 호출해서 객체를 만든다.

* 생성자(constructor)함수란 new 연산자와 호출해 객체(인스턴스)를 생성하는 함수다. 생성자 함수로 생성된 객체를 인스턴스(instance)라 한다.

  > 인스턴스(instance)
  >
  > 인스턴스는 객체가 메모리에 저장되 실제로 존재하는 것에 초점을 맞춘 용어이다. 생성자 함수도 객체이므로 생성자 함수나 클래스가 만든 객체를 다른 객체와 구분하기 위해 인스턴스라고 부른다.

  ```
  // String 생성자 함수에 의한 String 객체 생성
  const strObj = new String('Lee');
  console.log(strObj);        // String {"Lee"}
  
  // Number 생성자 함수에 의한 Number 객체 생성
  const numObj = new Number(123);
  console.log(numObj);        // Number {123}
  
  // Boolean 생성자 함수에 의한 Boolean 객체 생성
  const boolObj= new Boolean(true);
  console.log(boolObj);        // Boolean {true}
  
  // Function 생성자 함수에 의한 Function 객체(함수) 생성
  const func = new Function('x', 'return x * x');
  console.dir(func);        // ƒ anonymous(x )
  
  // Array 생성자 함수에 의한 Array 객체(배열) 생성
  const arr = new Array(1, 2, 3);
  console.log(arr);        // (3) [1, 2, 3]
  
  // RegExp 생성자 함수에 의한 RegExp 객체(정규 표현식) 생성
  const regExp = new RegExp(/ab+c/i);
  console.log(regExp);        // /ab+c/i
  
  // Date 생성자 함수에 의한 Date 객체 생성
  const date = new Date();
  console.log(date);        // Tue Mar 19 2019 02:38:26 GMT+0900 (한국 표준시)
  ```

  

## 생성자 함수

#### 객체 리터럴에 의한 객체 생성 방식의 문제

* 객체 리터럴은 생성 방식이 직관적이고 간편하지만, 하나의 객체만 생성한다.
* 동일한 프로퍼티를 갖는 객체를 여러개 생성할때, 비효율적이다.
* 객체는 프로퍼티를 통해 고유의 상태(state)을 표현하고, method로 상태(프로퍼티)를 참조하고 조작하는 동작(behavior)을 표현한다.
* 객체 리터럴로 생성하면, 매번 같은 프로퍼티와 메소드를 써야하는 불편한 점이 있다.
* 생성자 함수는 PascalCase로 구별가능한 이름을준다.



#### 생성자 함수에 의한 객체 생성 방식의 장점

* 객체(인스턴스)를 생성하기 위한 템플릿(클래스)처럼 생성자 함수를 사용해 프로퍼티 구조가 동일한 객체 여러 개를 편하게 생성할 수 있다.

  ```
  // 생성자 함수
  function Circle(radius) {
    // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
    this.radius = radius;
    this.getDiameter = function () {
      return 2 * this.radius;
    };
  }
  
  // 인스턴스의 생성
  const circle1 = new Circle(5);  // 반지름이 5인 Circle 객체를 생성
  const circle2 = new Circle(10); // 반지름이 10인 Circle 객체를 생성
  
  console.log(circle1.getDiameter()); // 10
  console.log(circle2.getDiameter()); // 20
  ```

  > **this**
  >
  > this는 객체 자신의 프로퍼티/메소드를 참조하는 자기 참조 변수(Self-referencing variable)이다. 객체 리터럴의 method 내부의 this는 자신이 소속된 객체를 가리킨다.

* 일반 함수로 호출: 전역 객체

* 메소드로 호출: 메소드를 호출한 객체

* 생성자 함수로 호출: 생성자 함수가 생성할 인스턴스

  ```
  // 함수는 다양한 방식으로 호출될 수 있다.
  function foo() {
    console.log(this);
  }
  
  // 일반적인 함수로 호출
  // 전역 객체는 브라우저 환경에서는 window, Node.js 환경에서는 global을 가리킨다.
  foo(); // window
  
  // 메소드로서 호출
  const obj = { foo }; // ES6 프로퍼티 축약 표현
  obj.foo(); // obj
  
  // 생성자 함수로서 호출
  const inst = new foo(); // inst
  ```

* 생성자 함수는 객체(인스턴스)를 생성하는 함수이다.

* **new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다.**

* 생성자 함수가 new와 호출되었을때 암묵적으로 단계를 거친다:

  * 빈객체를 생성한다
  * 생성된 빈 객체를 this에 할당한다(바인딩).
  * 기술한 코드를 실행한다.
  * return this; 를 실행한다.



#### 내부 메소드 [[Call]]과 [[Construct]]

* 함수 선언문/표현식을 정의한 함수는 일반적인 함수로 호출할수 있고, 생성자 함수로도 호출할 수 있다.

  * 생성자 함수로서 호출하는것은 new연산자와 호출하여 객체를 생성하는것이다.
  * 함수는 객체이므로 일반 객체와 동일하게 동작할수있다. 함수 객체는 일반 객체의 내부 슬롯과 메소드를 가지고 있다.

* **함수 객체는 일반 객체의 내부 슬롯/메소드 이외에 추가적인 내부슬롯/메소드가 있다.**

* 내부에 [[Call]]메소드를 갖는 함수 객체를 callable, [[Construct]]메소드를 갖는 함수 객체를 constructor, [[Construct]]를 갖지 않는 함수 객체는 non-constructor라고 부른다.

  * callable:호출할 수 있는 객체(모든 함수)

  * constructor: 생성자 함수로서 호출할 수 있는 객체

  * 일반적인 함수로 호출이되면 함수 객체의 내부 메소드[[Call]]이 호출된다.

  * 생성자 함수로서 호출하면 내부 메소드[[Construct]]가 호출된다.

    ```
    function foo() {}
    
    // 일반적인 함수로서 호출: [[Call]]이 호출된다.
    foo();
    
    // 생성자 함수로서 호출: [[Construct]]가 호출된다.
    new foo();
    ```

  * **모든 함수 객체는 내부 메소드 [[Call]]을 갖고 있어 호출할 수 있다.**
  * **모든 함수 객체가 [[Construct]]를 갖지는 않는다.**
  * constructor, non-constructor 함수가 있다.




#### constructor와 non-constructor의 구분

* JS 엔진은 함수를 생성할 때, FunctionCreate라는 추상(abstract operation) 연산을 사용한다.

  * 추상연산:ECMAScript 사양에서 내부 동작의 구현 알고리즘을 표현한것

* FunctionCreate은 함수 정의가 평가될때 호출된다.

  * 함수 정의 방식에 따라 FunctionCreate의 첫 매개변수 kind에 함수의 종류를 나타내는 문자열이 전달된다.

    * 일반 함수 정의(함수 선언문, 표현식)평가: Normal
    * 화살표 함수 정의 평가: Arrow
    * 메소드 정의 평가: Method

    ```
    // 일반 함수 정의 : kind = 'Normal'
    function foo() {}
    const bar = function () {};
    // 프로퍼티 x에 할당된 것은 일반 함수 정의이다. 메소드 정의로 인정하지 않는다.
    const baz = {
      x: function () {}
    };
    
    // 일반 함수로 정의된 함수만이 constructor이다.
    new foo(); // OK
    new bar(); // OK
    new baz.x(); // OK
    
    // 화살표 함수 정의 : kind = 'Arrow'
    const arrow = () => {};
    
    new arrow(); // TypeError: arrow is not a constructor
    
    // 메소드 정의 : kind = 'Method'
    // ES6의 메소드 축약 표현만을 메소드 정의로 인정한다.
    const obj = {
      x() {}
    };
    ```

* 일반적으로 프로퍼티의 값인 함수는 모두 method로 통칭한다.
  * ECMAScript에서 메소드 정의란 메소드 축약 표현만을 의미한다.
  * 함수가 어디에 할당되었는지가 아니라 정의 방식에 따라 종류를 구분.
* 일반 함수로 정의된 함수만이 constructor다.
  * 종류가 Arrow, Method인 함수는 non-constructor가 된다.
  * 일반 함수만을 생성자 함수로 호출할 수 있다.
  * 일반 함수로 호출되면 내부 메소드 [[Call]]이 호출.
  * new/super연산자와 생성자 함수로서 호출되면 내부 메소드 [[Construct]]가 호출된다.
* non-constructor 함수는 내부 메소드 [[Construct]]를 갖지 않는다.
  
  * 생성자 함수로서 호출하면 에러가 발생한다.
* 생성자 함수는 PascalCase로 첫문자를 대문자로해서 일반함수와 구별한다.



#### 생성자 함수의 인스턴스 생성 과정

* 생성자 함수는 프로퍼티 구조가 동일한 인스턴스를 생성한다.

  * 생성자 함수가 인스턴스를 생성하는것은 필수, 초기화하는 것은 옵션.
  
```
  // 생성자 함수
  function Circle(radius) {
    // 인스턴스 초기화
    this.radius = radius;
    this.getDiameter = function () {
      return 2 * this.radius;
    };
  }
  
  // 인스턴스 생성
  const circle1 = new Circle(5);  // 반지름이 5인 Circle 객체를 생성
  ```
  
* this프로퍼티를 추가하고 인수로 전달된 초기값을 값으로 할당.

* 자바스크립트 엔진은 암묵적으로 인스턴스를 생성하고 반환한다.
  * 인스턴스 생성과 this바인딩으로 암묵적으로 빈 객체가 생성된다.

  * 생성자 함수가 만든 인스턴스의 프로토타입으로 생성자 함수의 prototype 프로퍼티를 객체가 상속받는다.

  * 암묵적으로 생성된 빈객체(인스턴스)는 this에 바인딩된다.

    > **바인딩(binding)**
  >
    > 바인딩은 식별자와 값을 연결하는 과정을 의미한다. 
    >
    > ex: 변수는 할당에 의해 값이 바인딩된다.
  
* 인스턴스 초기화

  * 생성자 함수에 있는 코드가 실행되고 this에 바인딩되어있는 instance를 초기화한다.
  * this에 바인딩되있는 인스턴스에 property/method를 추가하고 생성자 함수가 인수로 전달받은 초기값을 프로퍼티에 할당하여 초기화하거나 고정값을 할당한다.

  ```
  function Circle(radius) {
    // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
  
    // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
    this.radius = radius;
    this.getDiameter = function () {
      return 2 * this.radius;
    };
  }
  ```

* 인스턴스 반환

  * 생성자 함수 내부의 모든 처리가 끝나면 인스턴스가 바인딩된 this가 암묵적으로 반환된다.

  ```
  function Circle(radius) {
    // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
  
    // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
    this.radius = radius;
    this.getDiameter = function () {
      return 2 * this.radius;
    };
  
    // 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다
  }
  
  // 인스턴스 생성. Circle 생성자 함수는 암묵적으로 this를 반환한다.
  const circle = new Circle(1);
  console.log(circle); // Circle {radius: 1, getDiameter: ƒ}
  ```

  * this가 아닌 다른 객체를 명시적으로 반환하면 this가 반환되지 못하고 return에 명시한 객체가 반환된다.
  * 명시적으로 원시 값을 반환하면 원시 값은 무시되고 암묵적으로 this가 반환된다.



#### new 연산자

* new연산자와 함께 함수를 호출하면 해당 함수는 생성자 함수로 동작한다.

* 함수가 constructor여야 생성자 함수로서 호출이 가능하다.

* new연산자 없이 생성자 함수를 호출하면 일반 함수로 호출된다

  * 객체의 내부 메소드[[Construct]]가 아니라 [[Call]]이 호출된다

    ```
    // 생성자 함수
    function Circle(radius) {
      this.radius = radius;
      this.getDiameter = function () {
        return 2 * this.radius;
      };
    }
    
    // new 연산자 없이 생성자 함수 호출하면 일반 함수로서 호출된다.
    const circle = Circle(5);
    console.log(circle); // undefined
    
    // 일반 함수 내부의 this는 전역 객체 window를 가리킨다.
    console.log(radius); // 5
    console.log(getDiameter()); // 10
    
    circle.getDiameter(); //
    ```

  * Circle 함수를 new연산자와 생성자 함수로서 호출하면 함수 내부의 this는 Circle생성자 함수가 생성할 인스턴스를 가리킨다.
  * Circle을 일반적인 함수로 호출하면 this는 전역객체 window를 가리킴.

* 일반 함수와 생성자 함수에는 형식적 차이가 없으므로 생성자 함수의 첫 문자를 대문자로 PascalCase를 사용한다.



#### new.target

* new연산자 없이 생성자 함수를 호출하는것을 방지하기 위해 ES6에서는 new.target을 지원한다.

* this와 유사하게 모든 함수 내에서 암묵적 지역 변수와 같이 사용되고 메타 프로퍼티(meta property)라고 부른다. IE는 지원하지 않는다.

* 함수 내에서 new.target을 사용하면 new연산자와 같이 호출되었는지 확인.

* new연산자 없이 호출된 함수의 new.target은 undefined다.

  ```
  // 생성자 함수
  function Circle(radius) {
    // 이 함수가 new 연산자와 함께 호출되지 않았다면 new.target은 undefined이다.
    if (!new.target) {
      // new 연산자와 함께 호출하여 생성된 인스턴스를 반환한다.
      return new Circle(radius);
    }
  
    this.radius = radius;
    this.getDiameter = function () {
      return 2 * this.radius;
    };
  }
  
  // new 연산자 없이 생성자 함수를 호출하여도 생성자 함수로서 호출된다.
  const circle = Circle(5);
  console.log(circle.getDiameter());
  ```

  **스코프 세이프 생성자(Scope-Safe Constructor) 패턴**

  new.target을 사용할 수 없는 상황이라면 스코프 세이퍼 생성자(Scope-Safe Constructor) 패턴을 사용할 수 있다.

  ```
  // Scope-Safe Constructor Pattern
  function Circle(radius) {
    // 생성자 함수가 new 연산자와 함께 호출되면 함수의 선두에서 빈 객체를 생성하고
    // this에 바인딩한다. 이때 this와 Circle은 프로토타입에 의해 연결된다.
  
    // 이 함수가 new 연산자와 함께 호출되지 않았다면 이 시점의 this는 전역 객체 window를 가리킨다.
    // 즉, this와 Circle은 프로토타입에 의해 연결되지 않는다.
    if (!(this instanceof Circle)) {
      // new 연산자와 함께 호출하여 생성된 인스턴스를 반환한다.
      return new Circle(radius);
    }
  
    this.radius = radius;
    this.getDiameter = function () {
      return 2 * this.radius;
    };
  }
  
  // new 연산자 없이 생성자 함수를 호출하여도 생성자 함수로서 호출된다.
  const circle = Circle(5);
  console.log(circle.getDiameter()); // 10
  ```

* 생성자 함수로 생성된 객체(인스턴스)는 프로토타입에 의해 생성자 함수와 연결된다.

* 이를 이용해 new연산자와 함께 호출되었는지 확인할 수 있다.

  * 대부분의 built-in constructor 함수(Object, String, Number, Boolean, Function, Array Date 등)는 new와 함께 호출되었는지 확인한 후 적절한 값을 반환한다.

  * 예를 들어 Object 나 Function 생성자 함수는 new없이 호출해도 new와 함께 호출했을 떄와 동일하게 동작한다.

    ```
    let obj = new Object();
    console.log(obj); // {}
    
    obj = Object();
    console.log(obj); // {}
    
    let f = new Function('x', 'return x ** x');
    console.log(f); // ƒ anonymous(x) { return x ** x }
    
    f = Function('x', 'return x ** x');
    console.log(f); // ƒ anonymous(x) { return x ** x }
    ```

  * 하지만 String 생성자 함수는 new와 함께 호출했을때 String 객체를 생성하여 반환하지만 new없이 호출하면 문자열 리터럴을 반환한다.

    ```
    let s = new String('abc');
    console.log(s); // String {"abc"}
    
    s = String('abc');
    console.log(s); // abc
    ```

    