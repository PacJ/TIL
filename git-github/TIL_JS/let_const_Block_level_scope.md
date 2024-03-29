# let, const와 블록 레벨 스코프

## var 키워드로 선언한 변수의 문제점

* ES5까지는 var키워드가 변수를 선언하는 유일한 방법이었다.
* 중복 선언으로 의도치 않은 재할당이 일어날수 있다.
* 호이스팅이 되어 선언 이전에 참조를 해도 에러를 보여주지 않는다.
* 함수레벨 스코프로 코드블록에 스코프가 생기지 않는다.
* 함수내부가 아닌곳에서 선언하면 전역 변수가 된다.
* 전역 변수가 되면 전역 객체의 프로퍼티가 되어 종료 이전까지 살아있다.



#### 변수 중복 선언 허용

* var키워드로 선언한 변수는 중복 선언이 가능하다.
* 변수 이름이 이미 선언되었는지 모르고 중복 선언하고 값을 할당하면, 먼저 선언한 변수값이 변경된다.
* 변수 중복 선언은 문법적으로 허용되지만 사용하지 않는것이 좋다.



#### 함수 레벨 스코프

* var 키워드로 선언된 변수는 함수의 코드 블록 만을 지역 스코프로 인정한다.
* 함수 밖에서 선언된 변수는 코드 블록 내에서 선언되었다 할 지라도 모두 전역 변수이다.
* 함수 레벨 스코프는 전역 변수를 남발할 가능성을 높인다.

```
var x = 1;

if (true) {
  var x = 10;
}

console.log(x); // 10
```



#### 변수 호이스팅

* var 키워드로 변수를 선언하면 호이스팅에 의해 스코프의 선두로 올려진것처럼 동작한다.
* 변수 선언문 이전에 변수를 참조하는 것은 가독성을 떨어뜨리고 오류를 발생시킬 여지를 남긴다.



## let 키워드

**var 키워드의 단점을 보완하기 위해 ES6에서 let과 const를 도입했다.**

**블록 레벨 스코프를 가져 코드블록 내에 스코프를 갖는다.**

* let는 블록 레벨 스코프로 전역 스코프, 함수 레벨 스코프, 블록 레벨 스코프 모든 코드 블록을 스코프로 인정한다.

  

#### 변수 중복 선언 금지

* let으로 변수를 중복 선언하면 문법에러(SyntaxError)가 발생.

  

#### 블록 레벨 스코프

* var로 선언한 변수는 함수의 코드블록 만을 지역 스코프로 인정한다.

* let으로 선언한 변수는 모든 코드 블록(함수,if문,for문,while문,try/catch문 등)을 지역 스코프로 인정하는 블록 레벨 스코프(Block-level scope)를 따른다.

* 함수 내의 코드 블록은 함수 레벨 스코프에 중첩된다.

  ![img](https://poiemaweb.com/assets/fs-images/14-1.png)



#### 변수 호이스팅

* let으로 선언한 변수는 호이스팅이 발생하지 않는 것처럼 보인다.

* **let으로 선언한 변수는 선언 단계 와 초기화 단계가 분리되어 진행된다.**

  ![img](https://poiemaweb.com/assets/fs-images/14-3.png)

  ```
  let foo = 1; // 전역 변수
  
  {
    console.log(foo); // ReferenceError: foo is not defined
    let foo = 2; // 지역 변수
  }
  ```

* 런타임 이전에 엔진에 의해 변수 선언을 하지만 아직 var와 다르게 초기화를 할당하는 시점에서 하기때문에 값을 가지지 않고 참조하려고 하면 참조에러가 발생한다

* 아직 정의되지 않고 값이 없는 구간, 즉 스코프 시작 지점부터 초기화 단계 시작점(값이 정의되는 문)까지는 참조할 수 없다.

  * 이 구간이 **일시적 사각지대(Temporal Dead Zone)** 이다.

* 자바스크립트 ES6는 모든 선언(var, let, const, function, class 등)을 호이스팅한다.



#### 전역 객체와 let

* **전역 객체(Global Object)는 어떤 객체보다도 먼저 생성되는 최상위 객체이다.**

* 브라우저에서는 window객체, Node.js에서는 global객체를 의미.

  ```
  var x = 1;
  console.log(window.x) // 1
  console.log(x) // 1
  ```

  * 전역 객체의 프로퍼티는 객체명(window)를 생략하고 사용할 수 있다.

* var 키워드로 선언한 전역변수는 모두 전역 객체의 property가 된다.

  - function foo(){}
  - var foo = foo(){}
  - 둘다 전역 객체의 프로퍼티가 된다.

* var로 선언한 전역 변수, 선언하지 않은 변수에 값을 할당한 암묵적 전역 변수, 전역 함수는 전역 객체의 property가 된다. 전역 객체의 프로퍼티를 참조할 떄 window를 생략할 수 있다.

* let으로 선언한 전역 변수는 전역 객체 window의 프로퍼티가 아니다.

  * let으로 전역 변수를 선언해도 생명주기가 var보다 짧다.
  * let은 전역 코드의 실행이 종료되면 소멸된다. 전역 객체 window는 브라우저 종료하는 시점까지 남아있다.

* let 전역 변수는 보이지 않는 개념적인 블록내에 존재하게 된다.



## const 키워드

**const는 상수(변하지 않는 고정된 값)를 선언하기 위해 사용된다.**

하지만 반드시 상수만을 위해 사용하지는 않는다.



#### 선언과 초기화

* let으로 선언한 변수는 재할당이 자유로우나 **const는 재할당이 금지된다**.
* 처음 할당한 값을 그대로 유지하므로 고정된 값(상수)를 할당하기 위해 사용.
* **const로 선언한 변수는 반드시 선언과 동시에 할당이 이루어져야 한다.**
  * 그러지 않으면 문법에러(SyntaxError)가 발생한다.
* let변수와 같이 블록 레벨 스코프를 갖는다.



#### 상수

* 상수는 가독성과 유지보수의 편의를 위해 적극 사용해야한다.
* 상수를 값으로 갖는 변수는 일반적으로 변수 이름을 대문자로 선언한다.

```
// 세율
const TAX_RATE = 0.1

// 세전 가격
let preTaxPrice = 100;

// 세후 가격
let afterTaxPrice = preTaxPrice + (preTaxPrice * TAX_RATE);

console.log(afterTaxPrice); // 110
```

* 세후 가격 계산에 (preTaxPrice * 0.1)을 했다면 의미를 잘 모르지만, TAX_RATE라는 상수를 사용하면 의미를 쉽게 파악할 수 있다.



#### const 키워드와 객체

* const로 선언된 변수는 재할당이 금지된다.
* const 변수에 원시값을 할당할 경우, 원시값은 immutable value(변경 불가한 값)이고 const는 재할당이 금지되므로 할당된 값을 변경할 방법이 없다.
* const로 선언한 변수에 객체를 할당한 경우, 재할당은 금지되지만 객체는 mutable value(변경 가능한 값)이므로 변경이 가능하다.
  * 새로운 객체를 할당하는 것은 불가능하지만 객체의 내용을 변경하는것은 가능하다.



#### var vs. let vs. const

* 변수 선언에는 기본적으로 const를 사용하고 let은 재할당이 필요한 경우 사용.
* 원시 값의 경우, 상수를 사용하는 편이 좋다.
* const 키워드를 사용하면 의도치 않은 재할당을 방지해줘서 안전하다.
* 변수를 선언하는 시점에는 재할당이 필요할지 모르는 경우가 많으므로 일단 const 키워드를 사용하자.

