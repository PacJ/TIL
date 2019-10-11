#  객체 리터럴

#### 객체란

* 자바스크립트는 객체(object) 기반의 프로그래밍 언어, 거의 모든것이 객체.
* 원시 타입 값들을 제외한 나머지 값들(함수,배열,정규표현식 등)은 모두 객체.
* **원시 타입은 하나의 값만**을 나타내는 반면 **객체 타입은 다양한 타입의 값(원시 타입 또는 다른 객체)들을 하나의 단위로 구성.**
  * 복합적 자료구조
* 원시타입은 immutable value(변경 불가능한 값)이지만 객체는 mutable value(변경가능한 값)
* JavaScript 객체는 key와 value(값)로 구성된 property들의 집합.
* 모든 값은 property값이 될 수 있다. property값으로 함수를 사용할 수도 있다.
  * 프로퍼티 값인 함수는 일반 함수와 구분하기 위해 Method라 부른다.
  * Property: **객체의 상태**를 나타내는 값(data)
  * Method: Property를 참조하고 조작할 수 있는 **동작**(behavior)
  * 객체는 Property와 Method로 구성된 집합체.



#### 객체 리터럴에 의한 객체 생성

* 클래스 기반 객체지향 언어는 사전에 클래스 정의하고 필요할때 new연산자와 생성자를 호출하여 인스턴스를 생성해야된다.
  * instance: 클래스에 의해 생성되어 메모리에 저장된 실체
* JavaScript는 prototype기반 객체지향 언어로 다양하게 객체 생성이 가능.
  * 객체 리터럴, Object 생성자 함수, 생성자 함수, Object.create 메소드, 클래스(ES6부터) 등
* 가장 일반적이고 간단한 방법은 객체 리터럴을 사용하는 방법.
* 중괄호 내에 0개 이상 프로퍼티 정의, 변수에 할당을 하는 시점에 객체 리터럴은 해석되고 결과 객체가 생성된다.
  * 중괄호 내에 프로퍼티를 정의하지 않으면 빈 객체가 생성된다.
* 객체 리터럴의 중괄호는 코드 블록을 의미하지 않는다.
  * 코드 블록 닫는 중괄호 뒤에 세미콜론 X, 리터럴 닫는 중괄호뒤에는O.
* 유연하고 강력한 객체 생성방식.
* 이외 객체 생성 방식은 모두 함수를 사용하는 방식.



#### 프로퍼티(Property)

* 객체는 Property들의 집합이며 key와 value(값)들로 구성된다.
* Property key/value로 사용할 수 있는 값:
  * 프로퍼티 키: 빈 문자열을 포함하는 모든 문자열 또는 symbol값
  * 프로퍼티 값: 자바스크립트에서 사용할 수 있는 모든 값
* 프로퍼티를 나열할 때는 쉼표(,)로 구분한다, 마지막 프로퍼티 뒤에는 사용하지 않아도 된다.
* 프로퍼티 키는 식별자 역할을 하지만 반드시 식별자 네이밍 규칙을 따라야 하는것은 아니다.
  * symbol값도 키로 사용할 수 있지만 일반적으로 문자열을 사용한다.
  * 하지만 식별자 네이밍 규칙에 맞는 이름(JS에서 사용 가능한 유효한 이름)일때, 따옴표('')를 생략할 수 있다.
  * **식별자 네이밍 규칙을 따르지 않는 이름은 반드시 따옴표를 사용해야한다.**

* 문자열로 반환하는 표현식을 사용해 프로퍼티 키를 동적으로 생성할수도 있다.

  * Property key로 사용할 표현식을 대괄호([])로 묶는다

  * 이를 계산된 프로퍼티 이름(Computed Property name)이라 한다.

    ```
    var obj = {};
    var key = 'hello';
    
    // ES5: 프로퍼티 키 동적 생성
    obj[key] = 'world';
    // ES6: 프로퍼티 키 동적 생성
    // var obj = { [key]: 'world' };
    
    console.log(obj); // {hello: "world"}
    ```

    

* 문자열/symbol 값 이외에 값들은 모두 문자열로 암묵적 변환.
* 키를 중복 선언하면 뒤에 선언한 것이 앞에것을 덮어쓴다.



#### Method(메소드)

* JS내에 사용가능한 모든 값은 프로퍼티 값이 될수 있다.
* JS의 함수는 객체(일급 객체, First-class object)이다.
* 함수는 값으로 취급할수 있으며 프로퍼티 값이 될수 있다.
* 프로퍼티 값이 함수일때, 일반 함수와 구분해 Method라 부른다.
  * 객체에 제한되어 있는 함수를 의미



#### Property 접근

* Property 값에 접근 하려면 마침표(.) 표기법(Dot notation)이나 대괄호([]) 표기법(Bracket notation)을 사용해야한다.

  * 마침표 좌측은 객체 표현식이름(식별자), 우측에는 내부의 프로퍼티 키

    ```
    // 마침표 표기법에 의한 프로퍼티 접근
    console.log(person.name); 
    
    // 대괄호 표기법에 의한 프로퍼티 접근
    console.log(person['name']);
    ```

  * **대괄호 내부 프로퍼티 키는 반드시 따옴표로 감싼 문자열이어야 한다.**

  * 따옴표가 없으면 키가 아닌 식별자로 취급한다.

  * Property key가 식별자 네이밍 규칙을 준수 하지 않는 이름이면, 무조건 대괄효 표기법을 사용해야한다.)

    * Property key가 숫자로 이루어진 문자열일떄, 따옴표 생략 가능하다.



#### Property 값 갱신

* 이미 존재하는 Property 값에 할당을 하면 값이 갱신된다.
* 원시(primitive)타입이 아니므로 값 변경 가능.



#### Property 동적 생성

* 존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 추가되고 값이 할당된다.

  ```
  var person = {
    name: 'Lee'
  };
  
  // person 객체에는 address 프로퍼티가 존재하지 않는다.
  // 따라서 person 객체에 address 프로퍼티가 동적으로 생성되고 값이 할당된다.
  person.address = 'Seoul';
  
  console.log(person); // {name: "Lee", address: "Seoul"}
  ```

  

#### Property 삭제

* delete 연산자는 객체의 프로퍼티를 삭제.

* 연산자의 피연산자는 프로퍼티 값에 접근할 수 있는 표현식이어야한다.

  ```
  var person = {
    name: 'Lee'
  };
  
  // 프로퍼티 동적 추가
  person.address = 'Seoul';
  
  // person 객체에 address 프로퍼티가 존재한다.
  // 따라서 delete 연산자로 address 프로퍼티를 삭제할 수 있다.
  delete person.address;
  
  console.log(person); // {name: "Lee"}
  ```

  

### ES6에서 추가된 리터럴의 확장 기능



#### Property 축약 표현

* 객체 리터럴은 프로퍼티 키, 값으로 구성. Property 값은 변수에 할당된 값, 식별자 표현식일 수도 있다.

* 프로퍼티 값으로 변수를 사용하는 경우, key와 변수이름이 동일할때 프로퍼티 키를 생략할수 있다.(Property shorthand). 키는 변수이름으로 자동생성된다.

  ```
  let x = 1, y = 2;
  
  const obj = {
    x: x,
    y: y
  };
  // Property shorthand(프로퍼티 축약): 키가 변수 이름으로 자동생성.
  // 프로퍼티 축약 표현
  const obj = { x, y };
  
  
  console.log(obj); // {x: 1, y: 2}
  ```




#### Property key 동적 생성

* 문자열/문자열로 변환 가능한 값을 반환하는 표현식으로 프로퍼티키를 동적으로 생성할 수 있다.
* Property key로 사용할 표현식을 대괄호([])로 묶어야 한다.
* 계산된 프로퍼티 이름(Computed property name)이라 한다.
* ES6에서는 객체 리터럴 내부에서도 Property key 동적 생성할수 있다.
* 사용할일이 거의 없다.

```
const prefix = 'prop';
let i = 0;

// 객체 리터럴 내부에서 프로퍼티 키 동적 생성
var obj = {
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i
};

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
```



#### Method 축약 표현

* ES5에서는 메소드를 정의하려면 프로퍼티 값으로 함수를 할당하게되는데
  * sayHi: function() {}

* ES6에서는 메소드를 정의할떄 function을 생략할 수 있다.
  * sayHi() {}