* 모든 함수 객체는 일반 객체에 없는 arguments과 length프로퍼티를 가지고있다(JavaScript엔진한테 바인딩 받는다). length를 가지므로 유사 배열 객체이다.
* arguments는 함수의 모든 인수를 저장한다.
* 함수의 length property는 매개 변수의 개수.
* arguments 의 length property는 인수의 개수.



# Prototype

* **Prototype: 상속을 구현하는 것.**

  * 상위 개념으로 객체 지향이 있다.

  > 클래스(class)
  >
  > ES6에서 새롭게 도입되었다.

* prototype: 함수 객체 만이 가지고 있음
  * 모든 객체는 자신의 부모(상위객체 역할을 하는) prototype 객체(prototype)를 갖는다.
  * 상위 객체들이 단방향으로 연결된 구조를 prototype chain이라한다.
  * Object.prototype 만 부모객체가 없다(최상위).
* _ _proto__: 모든 객체가 가지고 있다.
* me._ _proto__로 상위 객체(프로토타입)에 접근할 수 있다.
* 생성자 함수로 만든 인스턴스는 프로토타입 객체에게 프로퍼티를 상속받는다.
  * 생성자 함수는 프로토타입을 참조할 수 있다.(Person.prototype)
  * 프로토타입은 생성자 함수를 참조값으로 갖는다.
  * 생성자 함수는 인스턴스를 만들기만하고, 프로토타입이 프로퍼티를 상속해준다.
* prototype chain은 프로퍼티를 찾기 위해 존재한다.(scope chain이 식별자를 찾듯이)
  * 식별자는 식별자 네이밍 규칙을 따르고 스코프체인에서 검색한다.
  * 프로퍼티는 식별자 네이밍 규칙을 따르면 좋지만 필수는 아니고 프로토타입 체인에서 검색한다.



## 객체 지향 프로그래밍

* 속성들의 나열로 객체를 만든다. **프로퍼티로 상태를 나타내고 메소드로 행위를 나타낸다.**
* 객체는 독립적인데 서로 관계를 맺을수있다. 데이터를 주고받을 수 있다.
  * 부/자 객체사이에는 상속으로 상호작용한다.
* 템플릿으로 동일한 속성들에 값을 넣어 새롭게 객체(인스턴스)를 생성하는 것을 자바스크립트에선 생성자 함수, 자바는 클래스(class)라고 한다.
  * 객체의 생성을 위한 템플릿으로 볼수 있다(생성자 함수, 클래스).
  * 여러 객체들이 같은 프로퍼티를 공유하지만 프로퍼티 값은 재각각이다.
  * 인스턴스는 부모(프로토타입)을 가지고 태어난다. 생성될때 생성자 함수에 의해서 프로토타입이 결정된다.
* 추상화(abstraction): 관심있는 속성만을 추려내서 표현하는것.
* 클래스 기반 언어는 하나의 객체를 만들때도 클래스로 만들어야한다.
* 자바스크립트는 객체 리터럴로 하나의 객체를 간편하게 만들 수 있다.



## 상속과 프로토타입

* 생성자 함수의 단점: 인스턴스 100개를 만들면 프로퍼티는 인스턴스별로 값이 달라 모든 인스턴스가 가지고 있는것이 맞지만, 메소드는 똑같은 것을 100번 중복해서 만들어야한다.

  * 중복이 되지 않도록 상위 객체에게 메소드를 줘서 객체들이 상속받도록 하는 것이 이상적이다.

   ![img](https://poiemaweb.com/assets/fs-images/18-1.png) 

  * circle1.getArea === circle2.getArea: 내용은 같지만 인스턴스가 달라서 False가 나온다. 객체 타입은 주소값이 같아야 동일하다.
  * 부모객체(prototype 객체)에 getArea를 넣으면 된다.

  ![img](https://poiemaweb.com/assets/fs-images/18-2.png) 

  * 생성자 함수는 prototype 프로퍼티를 가지고 있다. ([[Constructor]] 내부 메소드를 보유한 함수만, arrow/method는 인스턴스를 만들지 않기에)
  * 함수 정의가 평가되어 함수 객체가 될때, Circle.prototype도 생성된다.
    * CreateFunction('kind')를 호출해서 kind가 normal이면 Circle.prototype도 만드는것이다.
    * Circle.prototype에 method를 추가해서 하위객체들이 상속받게함.
    * Circle.prototype.getArea = 
    * 생성자 함수 내부에 this는 생성할 인스턴스를 가리킨다.

* _ _proto__프로퍼티는 Object.prototype의 프로퍼티이고, 하위 객체들은 상속을 통해 사용한다.

   ![img](https://poiemaweb.com/assets/fs-images/18-3.png) 

  * 생성자 함수는 Circle.prototype을 prototype프로퍼티로 찾을 수 있다.
  * circle1 은 Circle.prototype을 circle1._ _proto__로 프로토타입 체인에서 찾을 수 있다.
  * Circle.prototype은 [[constructor]]가 있으므로 생성자 함수를 찾아갈 수 있다.
  * circle1.constructor를 사용하면 자신에게 [[constructor]]가 없으니 프로토타입 체인에 따라 Circle.prototype에 있는 constructor를 사용해 생성자 함수를 찾아갈 수 있다.
  * Circle.prototype은 circle1, circle2를 찾을 수 없다.

* 프로토타입 체인: 객체 인스턴스의 프로퍼티를 탐색하는 매커니즘이다.

* 인스턴스 메소드, 프로토타입 메소드, 정적 메소드(Constructor에 있는 메소드)

  * 인스턴스 메소드는 인스턴스가 있어야 호출할 수 있다.
  * 정적 메소드는 인스턴스 생성 과정이 없어도 호출할 수 있다.
  * 프로토타입 메소드는 인스턴스가 있어야 호출할 수 있다.



## _ _proto__ 접근자 프로퍼티

* _모든 객체는 _ _proto__ 접근자 프로퍼티를 통해 인스턴스가 자신의 프로토타입을 찾아갈 수 있다.

  * 참조하면 프로토타입을 get으로 가져온다
  * 할당하면 set을 통해 프로토타입을 바꾼다.

* **객체 리터럴로 만든 객체는 Object 생성자 함수가 생성한것으로 볼수있다.**

  ```
  const person = {name: 'Lee'};
  
  console.log(Object.getPrototypeOf(person)) === Object.prototype); // true
  ```

* _ _proto__와 Object.getPrototypeOf()는 같은 기능을 하지만, 메소드 이름이 제데로된 Object.getPrototypeOf()를 사용하자.
* 객체는 createObject 라는 추상 연산이 만든다.
  * 빈객체를 만든다.
  * 프로퍼티 키와 값들을 propertyDescriptor로 객체에 추가한다.
  * new.create는 함수가 new와 함께 생성되었는지 확인한다.
  * Object로 생성자 함수 만들면 new.create로 new가 없으면 생성자 함수로 만든것처럼 된다.
  * 객체 리터럴/ 생성자 함수로 만드는것 차이
* 빌트인 객체들은 상속시켜줄수 있는 프로퍼티들이 많다.
  * ex: Array 생성자함수가 만든 instance는 _ _proto__인 array.prototype의 프로퍼티들을 사용할 수 있다.
* method 호출방식 2가지: instance를 앞에둔다:
  * console.log(person.toString());
  * 프로토타입 메소드다, 인스턴스 메소드일 수 있다.
* console.log(Object.getprototypeOf(person));
  * 인스턴스가 없어도 볼 수 있는 정적 메소드다.

```
const obj = {};
const parent = { x: 1 };

// getter 함수인 get __proto__가 호출되어 obj 객체의 프로토타입을 취득
obj.__proto__;
// setter함수인 set __proto__가 호출되어 obj 객체의 프로토타입을 교체
obj.__proto__ = parent;

console.log(obj.x); // 1
```

* 프로토타입을 교체해서 상속받는 것들을 동적으로 교체할 수 있다.
* 모든 프로토타입 객체는 constructor라는 프로퍼티를 갖는데 교체를하면 없어진다.
  * instance가 생성자 함수를 찾아가지 못하게 되는 문제가 생긴다.
  * 객체 리터럴로 만든 일반 객체의 프로토타입은 Object.prototype이다.
  * parent의 프로토타입은 Object가 된다.
* 함수 객체의 프로토타입은 function.prototype이다.
  * 함수 객체는 function이 만든걸로 치기때문에.
* 배열 인스턴스의 프로토타입은 array.prototype이다.
  * 배열이기 전에 객체여서 Object.prototype의 프로퍼티들을 사용한다.
  * 배열의 기능을 사용해야 될때는 array.prototype의 프로퍼티들을 사용.
    * **종류에 따른 특별한 기능들.**
* Object.prototype의 프로토타입(_ _proto__)은 null이다. 프로토타입 체인의 종점이다.
  * 종점이 없으면 순환참조된다. 끝없이 찾게된다.
  * **모든 객체는 Object.prototype의 프로퍼티를 사용할 수 있다.**



## 함수 객체의 prototype 프로퍼티

* 생성자 함수 객체만 prototype을 가지고 있다. 일반 객체는 _ _proto__ 를 상속받아서 사용한다.
* 모든 prototype은 constructor 프로퍼티를 가진다.



## 프로토타입 생성 시점

* 생성자 함수가 만들어지면 프로토타입이 생성되 연결이 된다.



#### 빌트인 생성자 함수와 프로토타입 생성 시점

* 빌트인 생성자 함수는 전부 전역 객체(Object.prototype) 소속이다.

* 전역 객체(window)가 생길때 생성된다(브라우저가 실행될때)

   ![img](https://poiemaweb.com/assets/fs-images/18-15.png) 

* 원시 값도 사용 가능하다. 원시값 뒤에 마침표(.)을 사용하면 wrapper 객체가 생성되어 객체가 된다.
* Object.prototype은 어디서든 사용할 수 있다.



#### Object 생성자 함수에 의해 생성된 객체의 프로토타입

