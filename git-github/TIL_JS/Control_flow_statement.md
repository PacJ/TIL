# 제어문(Control flow statement)

* 제어문(Control flow statement)은 주어진 조건에 따라(조건문) 코드 블록을 실행하거나 반복실행(반복문)할때 사용한다.
* 일반적으로 코드는 위에서 아래로 순차적으로 실행되지만, 제어문을 통해 코드의 실행 흐름을 제어할 수 있다.
* 하지만 실행 순서가 변경되면, 코드의 흐름을 이해하기 어렵게 만들어 가독성을 해친다.



#### 블록문(Block statement/ Compound statement)

* 0개 이상의 문을중괄호로 묶은것.
* 하나의 실행 단위로 취급한다.
* 단독으로 사용 가능하지만 일반적으로 제어문/함수 선언문에서 사용한다.
* 블록문의 끝에는 세미콜론을 붙이지 않는다.



#### 조건문(conditional statement)

* 조건식(conditional expression)의 평가결과에 따라 블록문의 실행을 결정.
* Boolean 값으로 평가될 수 있는 표현식.
* JavaScript에는 if...else문과 switch문이 있다.



#### if...else 문

* 주어진 조건식(불리언 값)의 평가 결과, 즉 True/False에 따라 실행할 코드블록을 결정한다.

* 평가 결과가 Boolean값이 아니면 강제로 변환시켜서 참,거짓을 구별한다.

* 조건식을 else if문으로 추가할 수 있다. else if문은 여러번 사용할 수 있다.

* if...else문은 삼항 조건 연산자로 바꿔 쓸 수 있다. 

  * // x가 짝수이면 문자열 '짝수' 반환, 홀수이면 문자열 '홀수'를 반환.
    
    ```
var x = 2;
    var result;
    
    if (x % 2) { // 2 % 2는 0이고 0은 false로 취급된다
      result = '홀수';
    } else {
  result = '짝수';
    }

    console.log(result); // 짝수
```
    
**결과가 0이면 0 은 False임으로 '짝수' 로 반환된다.**
    

    
    **삼항 조건 연산자로 바꾸면:**

    ```
    // x가 짝수이면 문자열 '짝수'를 반환하고 홀수이면 문자열 '홀수'를 반환한다.
var x = 2;
    
    **0은 false로 취급된다**.
    var result = x % 2 ? '홀수' : '짝수';
    
    console.log(result); // 짝수
    ```



**세가지 경우의 수(양수, 음수, 영):**

삼항 조건 연산자:

```
var num = 2;

// num이 0이 아니면 크면 true가 되므로 좌변에서 한번더 평가.

// 0보다 크면 true로 '양수', 작으면 false로 '음수' 반환

var kind = num ? (num > 0 ? '양수' : '음수') : '영';

console.log(kind); // 양수
```



#### switch 문

* 주어진 표현식을 평가하여 값과 일치하는 표현식을 갖는 case문으로 실행 순서 이동.

* 상황(case)을 의미하는 표현식을 지정하고 콜론으로 마친다.
  ```
  switch (표현식) {
  case 표현식1:
    switch 문의 표현식과 표현식1이 일치하면 실행될 문;
    break;
  case 표현식2:
    switch 문의 표현식과 표현식2가 일치하면 실행될 문;
    break;
  default:
    switch 문의 표현식과 일치하는 표현식을 갖는 case 문이 없을 때 실행될 문;
  }
  ```
  
* switch 문의 표현식과 일치하는 것이 없다면 default로 이동한다.

* switch문의 표현식은 Boolean값보다 문자열, 숫자 값인 경우가 많다.

* if...else문과 다르게 true/false보다는 다양한 상황(case)에 따라 실행할 코드블록을 결정한다.

* 중간에 break문을 사용하지 않으면, case를 만난후에 탈출하지않고 마지막 case후 default까지 실행되어서 default가 반환된다. 이를 폴스루(fall through)라고 한다.
  
  * **break 문으로 해당하는 case일경우 탈출할 수 있게 해줘야한다.**
  
* default 문은 일반적으로 마지막에 위치하므로 실행이 종료되면 switch문을 빠져나가기에 별도로 break 문이 필요하지 않다.

* case, default, break 등 다양한 키워드를 사용해야하고 fall through가 발생하는 등 복잡하다. if...else문으로 해결할 수 있다면 사용하는게 낫다. 하지만 switch문을 사용했을때 가독성이 더 좋다면 switch문을 사용하는게 좋다.



## 반복문(Loop statement)

* 주어진 조건식의 평가 결과가 true일때 코드블럭을 실행한다.
* 실행후에 다시 평가하여 여전히 true면 다시 실행한다.
* 조건식이 거짓일 때까지 반복된다.
* JavaScript는 3가지 반복문 for 문, while 문, do...while문을 제공, 그외에도 for...in 문, ES6에 도입된 for...of 문도 있다.



#### for 문

* 조건식이 거짓으로 판별될때까지 코드 블록을 반복 실행.

  * 일반적으로 for (변수 선언문/할당문; 조건식; 증감식) {

    조건식이 참인 경우 반복 실행될 문;

    }


![img](https://poiemaweb.com/assets/fs-images/7-1.png)

#### while 문

* 주어진 조건식의 평가 결과가 참이면 코드 블록을 반복 실행한다.

* 평가 결과가 거짓이 되면 실행 종료, 평가 결과가 불리언 값이 아니라면 강제로 불리언 값으로 변환된다.

  ```
  var count = 0;
  
  while (count < 3) {
  
  console.log(count);
  
  count++;
  
  } // 0 1 2
  ```

  

* 조건식의 평가 결과가 언제나 참이면 무한루프가 된다.

  * 무한루프를 탈출하려면 블록 내의 if문으로 탈출 조건을 만들고 break로 탈출한다.

    ```
var count = 0;
    
while (true) {
    
	console.log(count);
    
	count++;
    
if (count === 3) break;
    
    } // 0 1 2
    ```
    
    

#### do...while 문

* 코드 블록을 먼저 실행하고 조건식을 평가한다. 코드 블록은 무조건 한번 이상 실행된다.

  ```
var count = 0;
  
do {
  
	console.log(count);
  
	count++;
  
} while ( count < 3); // 0 1 2
  // while 이 충족되는한 계속 실행된다.
  ```



#### break 문

* 레이블 문, 반복문 또는 switch문의 코드 블록을 탈출시켜준다.
* for문, while문, switch문 안에서만 사용한다.
* 레이블 문(Label statement): 코드블록에 식별자 이름을 지은것.
  * ex: foo: console.log('foo');
  * 레이블 문은 프로그램의 실행 순서를 제어하기 위해 사용.
  * 중첩된 for문을 외부로 탈출할때는 유용하지만 그외에는 일반적으로 사용하지 않는것이 좋다. 레이블 문은 프로그램의 흐름을 복잡하게하고 가독성을 떨어트려서 오류를 발생시킬 가능성을 높인다.
* 반복문, switch문에 사용할경우 break문에 레이블 식별자를 지정하지 않는다.



#### continue 문

* 반복문의 코드 블록 실행을 현 시점에서 중단하고 반복문의 증감식으로 이동.
* break처럼 반복문을 탈출하지는 않는다.

