# 타입 변환과 단축 평가

* 개발자가 의도적으로 타입을 변환하는 것을 **명시적 타입 변환(Explicit coercion)** 또는 **타입 캐스팅(Type casting)**

  * 명시적 타입 변환: 

  * var x = 10;

    var str = x.toString(); // .으로 함수method를 사용해 문자열로 변환

    console.log(typeof str, str); // string 10

  

* 개발자 의도와 상관없이 엔진에 의해 암묵적 자동변경: **Implicit coercion(암묵적 타입 변환)** 또는 **Type coercion(타입 강제 변환)**

  * var x = 10;

    var str = x  + ''; // 문자열 연결 연산자는 숫자 타입 x로 새로운 문자열 생성.

    console.log(typeof str, str); // string 10

    
  
  * 암묵적 타입 변환은 변수의 값을 재할당하는 것이 아니라 엔진이 피수산자 값을 바탕으로 새로운 타입의 값을 만들어 한번만 사용하고 버린다.
  
    * ex: var x = 10;
  
      var str = x + '';
  
      console.log(typeof str, str); // string 10
  
      여기서 x가 '10'으로 변경된후 평가가 끝나면 참조되지 않아서 버려진다.
  
      

## 암묵적 타입 변환

**자바스크립트 엔진이 표현식을 평가할 때 코드의 문맥을 고려하여 암묵적 타입 변환을 실행한다.**

* ex: '10' + 2 // '102' (숫자 -> 문자열)

  5 * '10' // 50 (문자열 -> 숫자)

  !0 // true (숫자 -> boolean)



#### 문자열 타입으로 변환

* +연산자는 피연산자중 하나 이상이 문자열이면 문자열 연결 연산자로 동작.

* 문자열 타입이 아닌 피연산자를 문자열 타입으로 암묵적 변환.(피연산자도 표현식이다.)
  * 1 + '2' // 12
* Template literal(템플릿 리터럴)내에 문자열 인터폴레이션(String Interpolation)은 표현식의 평가 결과를 문자열 타입으로 암묵적 변환.
  * console.log(`1 + 1 = ${1 + 1}`); // "1 + 1 = 2"



#### 숫자 타입으로 변환

* -, *, / 같은 산술 연산자는 코드 문맥상 피연산자 모두 숫자 타입이여야 한다. 숫자 타입으로 암묵적 변환한다.
  * 1 - '1' // 0
  * 1 * '10' // 10
  * 1 / 'one' // NaN
* 엔진이 숫자 타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입 변환.

* 숫자 타입으로 변환이 불가능할경우 산술 연산을 할수 없으므로 표현식의 평가 결과가 NaN이 된다.

* 비교 연산자는 불리언 값을 만드는것이므로 모든 피연산자를 문맥상 숫자 타입으로 암묵적 변환한다.

  * '1' > 0 // true

* 숫자 타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입 변환.

  * +'0' // 0
  * +'1' // 1
  * +'string' // NaN
  * +'true' //1
  * +'false' // 0

  

#### 불리언 타입으로 변환

* 제어문, 삼항 조건 연산자의 조건식은 불리언 값(True/False)를 반환해야한다.
* 엔진은 조건식의 평가 결과를 Boolean 타입으로 암묵적 타입 변환한다.
* 이때 JavaScript engine은 Boolean타입이 아닌 값을 Truthy값(Truth로 인식할 값) 또는 Falsy 값(거짓으로 인식할 값)으로 구분한다. Truthy는 Truth로, Falsy는 False로 변환한다.
  * false, undefined, null, 0, -0, NaN, ''(빈문자열): false로 평가되는 falsy값.

* 함수
  * 어떤 작업을 수행하기 위해 필요한 문들의 집합을 정의한 코드 블록.
  * 이름과 매개변수를 가지고 필요할때 호출하여 일괄적으로 실행할 수 있다.



## 명시적 타입 변환

* 원레는 래퍼 객체를 생성하기 위해 사용하는 표준 빌트인 생성자 함수(String, Number, Boolean)를 new연산자 없이 호출하는 방법, built-in method를 사용하는 방법, 암묵적 타입 변환을 이용하는 방법 등이 있음.
  * 래퍼 객체: 원시 값은 객체가 아니지만 객체처럼 사용하면 원시 값을 감싸는 객체(래퍼 객체)를 생성한다.



#### 문자열 타입으로 변환

* String 생성자 함수를 new 연산자 없이 호출

  * console.log(String(1)); // '1'

  

* Object.prototype.toString 메소드를 사용

  * console.log((1).toString()); // '1'

  

* 문자열 연결 연산자를 이용

  * console.log(1 + ''); // '1'



#### 숫자 타입으로 변환

* Number 생성자 함수를 new 연산자 없이 호출

  * console.log(Number('-1')); // -1
  * console.log(Number(true)); // 1

  

* parseInt, parseFloat 함수를 사용 (문자열만 변환 가능)

  * console.log(parseInt('-1')); // -1

  

* +단항 연결 연산자를 이용

  * console.log(+'-1'); // -1
  * console.log(+true); //1

  

* *산술 연산자를 이용

  * console.log('-1' * 1); // -1
  * console.log(true * 1); // 1



#### 불리언 타입으로 변환

* Boolean 생성자 함수 new 연산자 없이 사용

  * console.log(Boolean('x')); // true
  * console.log(Boolean('')); // false
  * console.log(Boolean(0)); // false
  * console.log(Boolean({})); // true 

  

* !부정 논리 연산자 두번 사용

  * console.log(!! 'x'); // true
  * console.log(!! ''); // false
  * console.log(!! 0); // false



## 단축 평가

* 논리합OR(||)연산자와 논리곱AND(&&)연산자의 연산 결과가 불리언이 아닐수도 있다. 이 두 연산자는 언제나 피연산자 중 한쪽 값을 반환한다.

  * 논리곱 (AND) 연산자: 'Cat' && 'Dog' // 'Dog'

    * 'Cat'은 Truthy, 'Dog'도 Truthy로 둘다 true로 평가.
    * **논리곱 연산 결과를 결정한 것은 두번째 피연산자, 문자열 'Dog'를 반환**.

    

  * 논리합 (OR) 연산자:'Cat' || 'Dog' // 'Cat'

    * 'Cat'은 Truthy 로 true평가된다. 이시점에서 논리합 OR연산자는 둘중 하나만 true여도 결과가 정해지므로 두번째 피연산자를 평가하지 않아도 표현식을 평가할 수 있다.
    * 논리합 OR 연산자는 논리 연산의 결과를 결정한 첫번쨰 피연산자, 문자열 'Cat'을 반환한다.

    

  * **논리곱/논리합 연산자는 논리 평가를 결정한 피연산자를 그래도 반환한다.**

    * **이를 단축 평가(Short-Circuit evaluation)라 부른다.**

      * true || anything = true
      * false || anything = false
      * true && anything = anything
      * false && anything = false

      

  * 객체가 null인지 확인하고 프로퍼티를 참조할때 유용.

    * var elem = null;

      console.log(elem.value); // TypeError Cannot read property 'value' of null

      console.log(elem && elem.value); // null

    * 객체의 프로퍼티를 참조하면 타입 에러가 발생하는데 단축 평가로 에러를 발생시키지 않고 참조할 수 있다.

    

  * 함수 매개변수에 기본값을 설정할 때 유용.







