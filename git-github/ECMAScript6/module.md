## Module

* 모듈이 없으면 전역 스코프가 공유되어, 여러 파일이 하나의 스코프를 공유한다.
* 모듈은 파일로 쪼갠 단위인데, 모듈은 파일마다 독자적인 스코프가 존재한다.
* export/import로 파일을 외부로 공개하고, 다른 파일에서 사용 가능하도록 한다.
  * export 하는것은 public이 되는 것이다.
  * 여러개의 필요한 모듈들을 사용해서 애플리케이션을 구현한다.
  * 오픈소스는 모듈이다. 모듈은 코드를 공개하여 사용할 수 있게 가져오는것이다(import).
* API는 export할 모듈과 import할 파일의 접점이다. API의 I(interface)는 UI다.
* 모듈은 재사용을 위해 import한다.
  * 함수도 재사용에 유리하고, 가독성이 좋다.
* **모듈은 스코프가 있다.**
* ES6에 새로 생긴 모듈을 ESM이라고 부르고, script 태그 내부에 type로 쓴다.
  * 애플리케이션 개발에 쓸 레벨이 되지 않아서 사용하지 않는다.
* 자바스크립트를 클라이언트 사이드에 제한되지 않고 범용적으로 사용하고자 하면서 모듈을 사용해야하는 문제가 생겼다.
  * CommonJS(동기), AMD(Asynchronous Module Definition)이 제한되었다.
  * Node.js는 CommonJS를 표준으로 선택하였다.
  * require(~)를 사용한다.
* 하지만 client-side에서는 모듈을 사용하기 위해 Babel+Webpack을 사용한다.
  * 모든 모듈들을 한 파일로 번들링 하는것이 Webpack이다.
  * Babel은 ES6 이상의 문법들로 코딩을 하였을때, ES5 또는 ES3로 떨어트린다. 크로스 브라우징 때문에 그렇다.
  * 번들링된 파일은 CommonJs 함수를 가지고 있다(폴리필): import/export를 지원하기 위해서 CommonJs의 require문법 사용가능.
  * HTML을 제외한 모든 리소스를 하나로 번들링할 수 있다. 
    * CSS는 CSS끼리, 이미지는 이미지끼리, JS는 JS끼리 번들링할 수 있다.
* Sass도 CSS에 transfiling해줘서 브라우저가 이해할 수 있게 한다.



## ESM

* script 태그에 type attribute를 추가하면 로드된 파일은 모듈로 동작한다.

  ```
  <script type="module" src="lib.mjs"></script>
  <script type="module" src="app.mjs"></script>
  ```

* 확장자 mjs 와 js는 동작방식이 다르다.
  * mjs는 strict mode가 적용되고, 기본값으로 defer를 가진다.
*   아직까지는 브라우저가 지원하는 ES6 모듈 기능보다는 Webpack 등의 모듈 번들러를 사용하는 것이 일반적이다. 
  * IE를 포함한 구형 브라우저는 ES6 모듈을 지원하지 않는다.
  * 브라우저의 ES6 모듈 기능을 사용하더라고 transfiling이나 번들링이 필요하다.
  * 아직 지원하지 않는 기능(Bare import 등)이 있다.
    * Bare import: npm에서 패키지 이름만 써줘도 import된다.
    * ESM은 전체 경로를 모두 써줘야한다.
  * 아직 해결되지 않은 몇가지 이슈가 있다.
* 따라서 Babel과 Webpack을 사용한다.



## 모듈 스코프

* 모듈을 사용하지 않으면 분리된 자바스크립트 파일들이 하나의 전역을 공유한다.

* 모듈을 사용하면 모듈 파일별 스코프가 생긴다.

  * 모듈 스코프가 생겨, var x는 window의 프로퍼티가 되지 않고, 모듈의 스코프속에 들어간다.

  ```
  // foo.mjs
  var x = 'foo';
  
  console.log(x); // foo
  // 변수 x는 전역 변수가 아니며 window 객체의 프로퍼티도 아니다.
  console.log(window.x); // undefined
  ```

  ```
  // bar.mjs
  // 변수 x는 foo.mjs에서 선언한 변수 x와 스코프가 다른 변수이다.
  var x = 'bar';
  
  console.log(x); // bar
  // 변수 x는 전역 변수가 아니며 window 객체의 프로퍼티도 아니다.
  console.log(window.x); // undefined
  ```



## export 키워드

* 모듈은 독자적인 스코프를 가져 기본적으로 모듈 내부에서만 참조할 수 있다.

* export로 외부로 식별자들을 공개할 수 있다.

  ```
  // lib.mjs
  const pi = Math.PI;
  
  function square(x) {
    return x * x;
  }
  
  class Person {
    constructor(name) {
      this.name = name;
    }
  }
  
  // 변수, 함수 클래스를 하나의 객체로 구성하여 공개
  export { pi, square, Person };
  ```

* export 할 식별자를 객체 리터럴로 감싸서 객체를 export한다.



## import 키워드

* 모듈에서 export한 대상을 import키워드로 로드한다.

  ```
  // app.mjs
  // 같은 폴더 내의 lib.mjs 모듈을 로드.
  // lib.mjs 모듈이 export한 식별자로 import한다.
  // ES6 모듈의 파일 확장자를 생략할 수 없다.
  // Bare import다.
  import { pi, square, Person } from './lib.mjs';
  
  console.log(pi);         // 3.141592653589793
  console.log(square(10)); // 100
  console.log(new Person('Lee')); // Person { name: 'Lee' }
  ```

* 하나의 이름으로 import 할 수 있다.:

  ```
  // app.mjs
  import * as lib from './lib.mjs';
  
  console.log(lib.pi);         // 3.141592653589793
  console.log(lib.square(10)); // 100
  console.log(new lib.Person('Lee')); // Person { name: 'Lee' }
  ```

  * lib라는 객체가 만들어지고, export한 것들이 프로퍼티가 된다.
  * 가급적이면 *로 전체를 import하지 말자.

* 이름을 변경하여 import할 수도 있다.

  ```
  // app.mjs
  import { pi as PI, square as sq, Person as P } from './lib.mjs';
  
  console.log(PI);    // 3.141592653589793
  console.log(sq(2)); // 4
  console.log(new P('Kim')); // Person { name: 'Kim' }
  ```

* 여러 가지를 import 할때는 이름이 있어야한다.

* 모듈에서 하나만 export할 떄는 default 키워드를 사용할 수 있다.

  ```
  // lib.mjs
  export default function (x) {
  	return x * x;
  }
  ```

  * 하나를 export 할 때만 무명으로 함수를 선언할 수 있다.

  * 변수는 default export를 사용할 수 없다(var, let, const).

    ```
    // lib.mjs
    export default () => {};
    // => OK
    
    export default const foo = () => {};
    // => SyntaxError: Unexpected token 'const'
    ```

  