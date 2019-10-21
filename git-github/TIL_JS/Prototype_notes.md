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

* _ _proto__와 Object.getPrototypeOf()는 같은 기능을 하지만, 메소드 이름이 ES5 까지는 비표준이여서 Object.getPrototypeof()를 사용하자.
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

* 전역 객체(window)가 생길때(브라우저가 실행되자마자) 빌트인 생성자함수 Object가 생성된다.

  * 빌트인 생성자 함수와 같이 프로토타입들이 생성된다.
  * 생성자 함수 Object의 prototype프로퍼티에 바인딩된다.

   ![img](https://poiemaweb.com/assets/fs-images/18-15.png) 

* 원시 값도 사용 가능하다. 원시값 뒤에 마침표(.)을 사용하면 wrapper 객체가 생성되어 객체가 된다.
* Object.prototype은 어디서든 사용할 수 있다.



#### Object 생성자 함수에 의해 생성된 객체의 프로토타입

* Object.create(null) : 상위에 프로토타입이 없다. 상속받는 프로퍼티가 없다.



## 캡슐화

* 객체 캡슐화: 약처럼 안에있는 쓴맛을 캡슐로 감춰서 쓴맛을 못느끼게 한다.
  * 객체의 공개할 프로퍼티와 공개하지 않을 프로퍼티를 구분한다.
  * 정보은폐다.
    * 클래스 기반 언어는 public, private, protected 접근제한자가 있다.
    * public: 다른 객체에 있는 것들도 이 객체의 것들을 참조할 수 있다.
    * protected: 상속된 관계에서만 보여진다.
  * 자바스크립트는 접근제한자가 없어 모든게 public이다.
  * 자바스크립트는 클로저로 캡슐화를 한다.
* 프로퍼티(상태)들이나 메소드(동작)들을 외부에서 접근하지 못하게 한다.
* 중첩 함수는 모듈 패턴으로 외부에서 접근할수 있게 할 수 있다.
* this는 기본적으로 public이어서 this.name을 하면 name이 public된다.
  * 변수로 묶어서 해결한다.

* 모든 함수는 자신이 생성될때 자신의 상위 스코프를 기억한다.

* [[Environment]] 를 자바스크립트 렉시컬 환경 자료구조.
* 자바스크립트는 클로져로서 private이 없어도 정보은폐를 할수 있다.



## 오버라이딩과 프로퍼티 쉐도잉

* 프로토타입 메소드를 주고 인스턴스 에도 메소드를 준후에 메소드를 호출하면 식별자인 인스턴스에 가까운 메소드를 찾아서 호출한다.

  ```
    // 프로토타입 메소드
    Person.prototype.sayHello = function () {
      console.log(`Hi! My name is ${this.name}`);
    };
    
    // 인스턴스 메소드
  me.sayHello = function () {
    console.log(`Hey! My name is ${this.name}`);
  };
  
  // 인스턴스 메소드가 호출된다. 프로토타입 메소드는 인스턴스 메소드에 의해 가려진다.
  me.sayHello(); // Hey! My name is Lee
  ```

   ![img](https://poiemaweb.com/assets/fs-images/18-25.png) 

```
const Person = (function () {
  // 생성자 함수
  function Person(name) {
    this.name = name;
  }

  // 프로토타입 메소드
  Person.prototype.sayHello = function () {
    console.log(`Hi! My name is ${this.name}`);
  };

  // 생성자 함수를 반환
  return Person;
}());

const me = new Person('Lee');

// 인스턴스 메소드
me.sayHello = function () {
  console.log(`Hey! My name is ${this.name}`);
};

// 인스턴스 메소드가 호출된다. 프로토타입 메소드는 인스턴스 메소드에 의해 가려진다.
me.sayHello(); // Hey! My name is Lee
```

* this 바인딩을 바꿀수 있다. 

* prototype method를 호출하면 this의 값을 몰라 undefined 반환.

  > 오버라이딩(Overriding)
  >
  > 상위 클래스가 가지고 있는 메소드를 하위 클래스가 재정의하여 사용하는 방식이다.
  >
  > 오버로딩(Overloading)
  >
  > 함수의 이름은 동일하지만 매개변수의 타입 또는 개수가 다른 메소드를 구현하고 매개변수에 의해 메소드를 구별하여 호출하는 방식이다. 자바스크립트는 오버로딩을 지원하지 않지만 arguments 객체를 사용하여 구현할 수는 있다.



## 프로토타입의 교체

* [[SetPrototypeOf]] 메소드로 프로토타입을 교체할 수 있다.

  #### 생성자 함수로 프로토타입 교체

  ```
  const Person = (function () {
    function Person(name) {
      this.name = name;
    }
  
    // ① 생성자 함수의 prototype 프로퍼티를 통해 프로토타입을 교체
    Person.prototype = {
      sayHello() {
        console.log(`Hi! My name is ${this.name}`);
      }
    };
  
    return Person;
  }());
  
  const me = new Person('Lee');
  ```

* Person.prototype을 재할당 해서 프로토타입을 교체했다.

* 링크가 깨지지만 프로토타입 체인에는 문제가 없다.

  * constructor 프로퍼티가 없다.

   ![img](https://poiemaweb.com/assets/fs-images/18-26.png) 



#### 인스턴스를 통한 프로토타입 교체

```
function Person(name) {
  this.name = name;
}

const me = new Person('Lee');

// 프로토타입으로 교체할 객체
const parent = {
  sayHello() {
    console.log(`Hi! My name is ${this.name}`);
  }
};

// ① me 객체의 프로토타입을 parent 객체로 교체한다.
Object.setPrototypeOf(me, parent);
// 위 코드는 아래의 코드와 동일하게 동작한다.
// me.__proto__ = parent;

me.sayHello(); // Hi! My name is Lee
```

 ![img](https://poiemaweb.com/assets/fs-images/18-27.png) 

* Person도 prototype가 사라지고, parent도 construct가 없어서 프로토타입 체인에따라 상위로 올라간다.
* parent에는 constructor가 없어 프로토타입 체인을 따라 Object.prototype의 constructor로 가서 생성자 함수가 Object가 된다.



## 직접 상속

#### Object.create에 의한 직접 상속

* Object.create method는 명시적으로 프로토타입을 지정하고 새로운 객체를 생성한다.

* new 연산자 없이도 객체를 생성할 수 있다.

* 프로토타입을 지정하면서 객체를 생성할 수 있다. 이때 생성자 함수와 프로토타입 간의 링크가 파괴되지 않는다.

* 객체 리터럴에 의해 생성된 객체도 특정 객체를 상속받을 수 있다.

* 링크를 파괴하는 방식이 아닌 Object.create로 상속시켜줘야된다.

  ```
  const obj = { a: 1 };
  const child = Object.create(obj);
  
  console.log(obj.hasOwnProperty('a'));       // true
  console.log(obj.isPrototypeOf(child));      // true
  console.log(obj.propertyIsEnumerable('a')); // true
  ```

* console.log(obj.hasOwnProperty('a')); 보다

  ```
  // 프로토타입이 null인 객체를 생성한다.
  const obj = Object.create(null);
  obj.a = 1;
  
  // console.log(obj.hasOwnProperty('a')); // TypeError: obj.hasOwnProperty is not a function
  
  // Object.prototype의 빌트인 메소드는 객체로 직접 호출하지 않는다.
  console.log(Object.prototype.hasOwnProperty.call(obj, 'a')); // true
  ```

* console.log(Object.prototype.hasOwnProperty.call(obj, 'a'));
* Object.create(null)로 프로토타입 체인 종점에 있는 객체일 수 있기 때문에 hasOwnProperty를 사용하지 말자.



## 객체 리터럴 내부에서 __proto__에 의한 직접 상속

```
const myProto = { x: 10 };

// 객체 리터럴에 의해 객체를 생성하면서 프로토타입을 지정하여 직접 상속받을 수 있다.
const obj = {
  y: 20,
  // 객체를 직접 상속받는다.
  // obj → myProto → Object.prototype → null
  __proto__: myProto
};
// 위 코드는 아래와 동일하다.
// const obj = Object.create(myProto, { y: { value: 20 } });

console.log(obj.x, obj.y); // 10 20
console.log(Object.getPrototypeOf(obj) === myProto); // true
```



## 정적 프로퍼티/메소드

* 프로토타입 메소드와 인스턴스 메소드는 인스턴스를 만들어야 호출할수 있다.

* 정적 메소드는 인스턴스와 상관없이 언제든 호출할 수 있다.

   ![img](https://poiemaweb.com/assets/fs-images/18-32.png) 



## 프로퍼티 존재 확인

```
const person = {
  name: 'Lee',
  address: 'Seoul'
};

// person 객체에 name 프로퍼티가 존재한다. ''를 빼면 식별자를 찾는다.
console.log('name' in person);    // true
// person 객체에 address 프로퍼티가 존재한다.
console.log('address' in person); // true
// person 객체에 age 프로퍼티가 존재하지 않는다.
console.log('age' in person);     // false
// in은 상속관계에 있는 프로퍼티도 다나온다.
console.log('toString' in person); // true
// Object.prototype.hasOwnProperty 메소드를 사용해도 객체의 프로퍼티의 존재 여부를 확인할 수 있다.
console.log(person.hasOwnProperty('name')); // true
console.log(person.hasOwnProperty('age'));  // false
```



## 프로퍼티 열거

* 열거: 프로퍼티를 하나하나 나열해서 보는것.

  #### for...in문

  ```
  // in 연산자는 객체가 상속받은 모든 프로토타입의 프로퍼티를 확인한다.
  console.log('toString' in person); // true
  
  // for...in 문도 객체가 상속받은 모든 프로토타입의 프로퍼티를 열거한다.
  // 하지만 toString과 같은 Object.prototype의 프로퍼티가 열거되지 않는다.
  for (const prop in person) {
    console.log(prop + ': ' + person[prop]);
  }
  
  // name: Lee
  // address: Seoul
  ```

* 상속받은 프로토타입의 프로퍼티를 제외하고 열거:

```
const person = {
  name: 'Lee',
  address: 'Seoul',
  __proto__: { age: 20 }
};

for (const prop in person) {
  // 객체 자신의 프로퍼티인지 확인한다.
  if (!person.hasOwnProperty(prop)) continue; // 다시 위로 올라간다
  console.log(prop + ': ' + person[prop]);
}

// name: Lee
// address: Seoul
```



#### Object.keys/values/entries 메소드

* keys: 프로퍼티 키들을 자료구조인 배열에 담아서 반환한다.
* values: 프로퍼티 값들을 배열에 담아서 반환한다.
* entries: key 와 value 들을 찍지어 배열로 반환한다.

```
const person = {
  name: 'Lee',
  address: 'Seoul',
  __proto__: { age: 20 }
};

console.log(Object.keys(person)); // ["name", "address"]
console.log(Object.values(person)); // ["Lee", "Seoul"]
console.log(Object.entries(person)); // [["name", "Lee"], ["address", "Seoul"]]
```

* ____proto____는 Object.prototype의 접근자 프로퍼티로 enumerable 값이 false여서 열거가 불가능하다.

