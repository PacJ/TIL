# 프로퍼티 정의

* 프로퍼티 attribute의 값을 정의하여 프로퍼티의 상태를 관리하는것.

* 객체의 프로퍼티가 어떻게 동작해야 하는지 정의할 수 있다.

* **자바스크립트 엔진은 프로퍼티를 생성할때(객체 리터럴 평가, 프로퍼티 동적 생성)프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.**

  ```
  const obj = {};
  
  // 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.
  obj.prop = 10;
  
  // 프로퍼티 attribute은 Object.getOwnPropertyDescriptor 
  // 메소드로 확인할 수 있다.
  var descriptor = Object.getOwnPropertyDescriptor(obj, 'prop');
  console.log(descriptor);
  
  // {value: 10, writable: true, enumerable: true, configurable: true}
  ```

* 프로퍼티 정의는 property attribute을 정의하는 것이다.
  * property attribute은 property의 상태를 나타낸다.
  * 프로퍼티의 상태는 프로퍼티의 값(value), 값의 갱신 가능 여부(writable), 열거 가능 여부(enumerable), 재정의 가능 여부(configurable)
  * Object.getOwnPropertyDescriptor 메소드로 어트리뷰트를 참조할 수 있다.
    * 존재하지 않는 프로퍼티나 상속받은 프로퍼티를 사용하면 undefined가 반환된다.
    * 인수는 객체의 참조와 데이터 프로퍼티의 키를 문자열로 전달한다.



## 내부 슬롯/메소드

* 내부 슬롯(Internal slot)과 내부 메소드(Internal method)는 ECMAScript스펙에서 요구하는 객체와 관련된 내부 상태와 동작을 정의한것이다.

* 자바스크립트 엔진의 내부 구현 사양을 정의한 것으로 ECMAScript 사양의 만족을 요구할 뿐, 이를 외부로 노출시키지는 않는다.

* 대부분의 내부 슬롯/메소드는 비공개다.

  * 접근하고 수정할수 있으면 엔진을 바꿀수 있게되어 비공개로 한다.
  * 일부의 내부 슬롯/메소드들은 접근할 수 있다.

* 내부 슬롯/메소드는 객체의 프로퍼티가 아니다.

  * 직접적으로 접근하거나 호출할 수 있는 방법을 제공하지 않는다.
  * 간접적으로 접근할 수단은 있다.

* [[Get]] 내부 메소드는 프로퍼티 키로 프로퍼티 값에 접근하면 내부적으로 호출된다.

  * [[Get]]동작: 프로퍼티키가 유효한지 확인한다(문자열이나 심볼). 

  * 프로토타입 체인에서 프로퍼티를 검색한다.

    > 프로토타입과 프로토타입 체인
    >
    > 프로토타입은 어떤 객체의 상위 객체의 역할을 하는 객체이다. 프로토타입은 하위 객체에게 자신의 프로퍼티와 메소드를 상속한다. 프로토타입 체인은 단방향 linked 리스트 형태로 연결된 상속 구조다. 객체의 프로퍼티나 메소드에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티 또는 메소드가 없다면 프로토타입 체인을 따라 차례대로 검색한다.

  * 검색된 property가 "데이터 프로퍼티(Data property)"라면 프로퍼티 값([[Value]] attribue)을 반환.

  * 프로퍼티가 접근자 프로퍼티(Accessor property)라면 접근자 프로퍼티의 프로퍼티 어트리뷰트 [[Get]]의 값, 즉 getter 함수를 호출해 결과를 반환한다.



## 데이터/접근자 프로퍼티

**프로퍼티는 데이터 프로퍼티와 접근자 프로퍼티로 구분할 수 있다**

* 데이터 프로퍼티(Data property)

  * 키와 값으로 구성된 일반적 프로퍼티다. 
  * console.log(Object.getOwnPropertyDescriptors); 로 attribute을 확인할 수 있다.
  * 접근자에 없는 value값이 있고, writable(재정 가능), enumerable(열거 가능), configurable(설정 가능(위에것들 수정)) 어트리뷰트 들이 있다.
  * 프로퍼티에 value가 있다면 데이터 프로퍼티고, JavaScript에서 value는 공개된다(public).

* 접근자 프로퍼티(Accessor property)

  * value를 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수(Accessor function)로 구성된 프로퍼티.

* 다른 데이터 프로퍼티의 value attribute를 조작하는 함수다.

*  get, set, enumerable, configurable attribute들을 갖는다.

* 접근자 함수는 getter/setter 함수라고도 부른다.

* 접근자 프로퍼티는 getter와 setter를 모두 정의할 수도 있고 하나만 정의할 수도 있다.

  ```
  const person = {
    // 데이터 프로퍼티
    firstName: 'Ungmo',
    lastName: 'Lee',
  
    // fullName은 접근자 함수로 구성된 접근자 프로퍼티이다.
    // getter 함수
    get fullName() {
      return `${this.firstName} ${this.lastName}`
    },
    // setter 함수
    set changeFirstName(name) {
      this.firstName = firstName;
    }
  };
  
  // 데이터 프로퍼티를 통한 프로퍼티 값의 참조.
  console.log(person.firstName + ' ' + person.lastName); // Ungmo Lee
  
  // 접근자 프로퍼티를 통한 프로퍼티 값의 저장
  // 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출된다.
  person.changeFirstName = 'Heegun Lee';
  console.log(person); // {firstName: "Heegun", lastName: "Lee"}
  
  // firstName는 데이터 프로퍼티이다.
  let descriptor = Object.getOwnPropertyDescriptor(person, 'firstName');
  console.log(descriptor);
  // {value: "Heegun", writable: true, enumerable: true, configurable: true}
  
  // changeFirstName는 접근자 프로퍼티이다.
  // 접근자 프로퍼티는 get, set, enumerable, configurable 프로퍼티 어트리뷰트를 갖는다.
  descriptor = Object.getOwnPropertyDescriptor(person, 'fullName');
  console.log(descriptor);
  // {get: ƒ, set: ƒ, enumerable: true, configurable: true}
  ```
  
* 접근자 프로퍼티는 자체적으로 값(value property attribute)을 가지지 않고 데이터 프로퍼티의 값을 읽거나 저장할 때 관여만 한다.

* 접근자 프로퍼티로 프로퍼티 값에 접근하면 내부 메소드가 호출되어 동작.

  1. 프로퍼티 키가 유효한지 확인한다.
  2. 프로토타입 체인에서 프로퍼티를 검색한다.
  3. 검색된 프로퍼티가 데이터 프로퍼티인지 접근자 프로퍼티인지 확인.
  4. 접근자 프로퍼티면 getter,setter함수를 호출한다.

* [[Prototype]]은 내부 슬롯, -_proto__는 접근자 프로퍼티다.





## 프로퍼티 어트리뷰트

* 모든 프로퍼티(데이터,접근자)는 자신의 상태/동작을 정의한 내부 슬롯/메소드를 가지고 있다.
  * 프로퍼티 어트리뷰트(property attribute)라 한다.
  * 엔진이 프로퍼티를 생성할때 기본값으로 자동 정의.
  * 이후 정의된 어트리뷰트를 설정해 프로퍼티의 세부 동작을 제어.



* **데이터 프로퍼티:** 
  * [[Value]]: 
    * 프로퍼티 키로 값에 접근하면 내부 method [[Get]]에 의해 반환되는 값.
    * 프로퍼티 키로 값을 저장하면 [[Value]]에 값을 저장한다. 프로퍼티가 없으면 생성하고 생성된 [[Value]]에 값을 저장한다.
  * [[Writable]]
    * 프로퍼티 값이 변경 가능한지 나타낸다(불리언 값).
    * 값이 false인 경우 [[Value]]의 값을 변경할 수 없다.
  * [[Enumerable]]
    * 프로퍼티의 열거 가능 여부를 나타낸다(불러인 값).
    * 값이 false인 경우 for...in문, Object.keys 메소드 등으로 열거 불가.
  * [[Configurable]]
    * 프로퍼티의 configure(재정)가능 여부를 나타낸다(불리언 값).
    * false인 경우 삭제, 어트리뷰트 값의 변경이 금지된다.
    * [[Writable]]이 true인 경우 [[Value]]와 [[Writable]]을 false로 변경하는 것은 허용된다.



* **접근자 프로퍼티:**

  * [[Get]]
    * 접근자 property로 데이터 프로퍼티 값을 읽을때 호출되는 함수.
    * 접근자 property로 값에 접근하면 프로퍼티 어트리뷰트 [[Get]]의 값, 즉 getter 함수가 호출되고 결과가 프로퍼티 값을 반환된다.
  * [[Set]]
    * 접근자 property로 프로퍼티 값을 저장할때 호출되는 함수.
    * 접근자 property키로 값을 저장하면 프로퍼티 어트리뷰트 [[Setter]]의 값, 즉 setter함수가 호출되고 결과가 값을 저장된다.
  * [[Enumerable]]
    * 데이터 프로퍼티와 같다.
  * [[Configurable]]
    * 데이터 프로퍼티와 같다.

  ```
  // 데이터 프로퍼티 정의
  Object.defineProperty(person, 'firstName', {
    value: 'Ungmo',
    writable: true,
    enumerable: true,
    configurable: true
  });
  
  Object.defineProperty(person, 'lastName', {
    value: 'Lee'
  });
  
  let descriptor = Object.getOwnPropertyDescriptor(person, 'firstName');
  console.log('firstName', descriptor);
  // firstName {value: "Ungmo", writable: true, enumerable: true, configurable: true}
  
  // 디스크립터 객체의 프로퍼티를 누락시키면 undefined, false가 기본값이다.
  descriptor = Object.getOwnPropertyDescriptor(person, 'lastName');
  console.log('lastName', descriptor);
  // lastName {value: "Lee", writable: false, enumerable: false, configurable: false}
  ```

* Object.defineProperty 메소드로 프로퍼티를 정의할때 프로퍼티 디스크립터 객체의 프로퍼티를 일부 누락할 수 있다.
  * value, get, set, writable, enumerable, configurable
  * 누락시 기본값은 undefined, undefined, undefined, false, false, false
* Object.defineProperty 메소드는 한번에 하나의 프로퍼티만 정의가능하다.
* Object.defineProperties메소드로 여러개의 프로퍼티를 한번에 정의.

