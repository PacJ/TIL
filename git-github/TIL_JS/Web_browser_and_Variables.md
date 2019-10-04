# JavaScript 개발 환경
## JavaScript 실행 환경
* 모든 브라우저는 JavaScript 실행가능.

* Node.js도 자바스크립트 엔진 내장,  JavaScript 실행가능.

* 브라우저는 웹 페이지를 화면에 랜더링할목적, Node.js 는 서버 개발 환경을 제공 하는것이 목적.

* 따라서 Node.js와 브라우저에서 JS의 코어인 ECMAScript를 실행할수 있지만 이외에 추가적인 기능은 호환되지 않는다.

* 보안상으로 Web API에서는 File 시스템을 제공하지 않는다.

* 브라우저는 client-side Web API를 지원한다. Node.js는 client side Web API를 지원하지 않고 ECMAScript와 Node.js 고유의 Host API를 지원한다.

  ![img](https://poiemaweb.com/assets/fs-images/3-1.png)

## 웹 브라우저 작동
브라우저의 핵심기능: 웹페이지를  Client의 요청(Request)과 Server의 응답(Response)을 받아 표시하는것

* 웹사이트로 이동시, 서버측으로부터 HTML,CSS,JavaScript 다운로드(Loading)하고 페이지 나타냄.

  * Domain주소 뒤에 추가로 뭐가 없으면(ex: google.com), 페이지의 index.html을 http Request(GET /index.html) 보내서 받고, 받고난뒤에 html을 로딩한뒤 파싱을 하면서 DOM tree를 만들기 시작한다.
    * URL이 http(HyperText Transfer Protocol)로 시작한다: 브라우저가 http를 사용해 이 URL에 관련된 문서를 가져와야한다는것을 명시.
  * 파싱중에, HTML의 link 태그를 만나면, DOM tree 생성이 중단되고, link된 CSS 를 Load, Parse 하고 CSSOM tree를 만든한뒤에, 다시 HTML의 파싱과 DOM tree 생성을 재개한다.
  * 파싱중에 script 태그를 만나면, 다시 파싱과 DOM tree를 중단하고, JavaScript 엔진에게 렌더링 권한을 넘겨 load, parse 하고 Syntax tree를 만든후에 다시 HTML로 파서 권한이 돌아가서 남은 파싱을 완료한다.
    * JavaScript 엔진이 파일을 로딩하고 파싱하여 AST를 생성, 바이트코드를 실행.
      * 자바스크립트 파일의 소스코드는 문자열로 구성되어 있으므로,  파싱을할때 소스 코드를 해석하여 문법적 의미와 구조를 갖는 구조인 AST(Abstract Syntax Tree)를 생성, 이걸 통해 바이트 코드 생성후 실행.
        - Tokenizing: 소스 코드 문자열을 분석(Lexical analysis)하여 의미를 갖는 코드의 최소단위인 토큰(Token)들로 쪼갠다.
        - Parsing: 토큰들의 집합을 구문 분석(Syntactic analysis)하여 AST생성.
        - 코드 실행: 생성된 AST는 interpreter를 실행할수있는 Intermediate code인 bytecode로 변환되고 interpreter에 의해 실행된다.
      * AST는 Interpreter 나 Compiler만이 사용하는것이 아니다. AST로 TypeScript, Prettier Babel같은 트랜스파일러도 구현할 수 있다.
    * Syntax tree는 DOM tree 와 CSSOM tree 를 조작하고 수정하고, 둘이 결합되어 Render tree 생성.
  * Script 태그의 위치에따라 블로킹이 생겨 DOM 생성이 지연될수도 있다. HTML이 DOM객체로 변환되기 이전에 JavaScript가 실행되면 블로킹이된다. 따라서 Script태그 위치는 중요하다(보통 body태그 끝나기전에 넣음).
    * async: 웹페이지의 파싱과 외부 스크립트 파일의 다운로드가 동시에 진행. script 다운 완료후 실행됨.
    * defer:웹페이지 파싱과 외부 스크립트 파일 다운로드 동시 진행. 스크립트는 웹페이지 파싱 이후 실행.
  * DOM tree, CSSOM tree가 만들어지면, 둘이 합쳐져 Render tree를 만들고, Render tree를 기반으로 painting이 시작되고 웹페이지가 표시된다.




## 개발자 도구
| 패널 | 설명 |
| :------: | :-----|
| Elements | 로딩된 웹페이지의 DOM과 CSS를 편집하여 렌더링된 뷰를 확인할수있다. 편집한 내용은 저장x.|
| Console | 로딩된 페이지의 에러확인, 자바스크립트 소스코드에 포함된 console.log method의 결과 확인 가능. |
| Sources | 로딩된 웹페이지의 자바스크립트 코드를 디버깅할 수 있다. |
| Network | 로딩된 웹 페이지에 관련한 네트워크 요청(request)정보와 퍼포먼스 확인 |
| Application | 웹 스토리지, 세션, 쿠키 확인 및 관리 |

## 콘솔
* 자바스크립트 코드에서 에러가 발생하여 정상작동 하지 않을때 우선적으로 확인.
* 간편하게 코드의 실행결과를 확인하기위해 console.log 함수 사용 가능.

## Node.js
* 클라이언트 사이드(웹 브라우저에서 동작하는 간단한 웹 애플리케이션)은 브라우저만으로도 개발 가능.
* 규모가 커짐에따라 React, jQuery같은 외부 라이브러리를 도입하거나 여러가지 도구를 사용해야 할필요가 있다. 이떄 Node.js와 npm이 필요.

## Node.js 와 npm
* Node.js는 크롬 V8 JavaScript engine 으로 마들어진  JavaScript Runtime Environment(런타임 환경)
* 브라우저 이외에서 JavaScript 동작 가능하게 해줌(Node.js)
* Node.js는 주로 사이드 어플 개발에 사용, 필요한 module, file system, Http 등 built-in API제공.
* Node.js는 데이터를 실시간 처리하는 SPA(Single Page Application)에 적합, CPU 사용 높은 애플리케이션에는 좋지 않음.
*  npm(node package manager): JavaScript 패키지 매니저. Node.js에서 사용할수있는 module들을 패키지화, 저장소 역할과 패키치 설치/관리를 위한 CLI(Command  line interface) 제공.

# 변수
*  연산후 결과를 재사용하고싶으면 결과가 저장된 메모리 공간의 주소에 직접접근하는것 외에는 방법이없다. 하지만 직접접근하는 것은 시스템을 멈추게 할 수도 있는 치명적 오류를 생산할 가능성이 높은 위험한 일이여서, 자바스크립트는 개발자의 직접적인 메모리 제어를 허용하지 않음.
* 기억하고싶은 데이터를 메모리에 저장하고, 저장된 데이터를 읽어 들여 재사용하기위해 변수를 사용한다.
* 변수는 하나의 값을 저장할 수 있는 메모리 공간에 붙인 이름, 또는 메모리 공간 자체를 말한다.
* 변수에 값을 저장하는 것을 할당(assignment)이라 하고, 변수에 저장된 값을 읽어 들이는 것을 참조(reference)라한다.
* 변수는 사람이 이해할 수 있도록 지정한 이름이기에, 좋은 이름의 변수는 가독성을 높여주기도한다. 

## 식별자
* 변수 이름을 식별자(identifier)라고도 부름.
* 식별자는 어떤 값을 구별하여 식별해낼 수 있는 이름을 말함.
* 변수, 함수 클래스 등의 이름은 모두 식별자
* 메모리 상에 존재하는 어떤 값을 식별하는것. 
* 식별자 네이밍규칙을 준수하고, 선언(declaration)을 통해 JavaScript engine에 식별자의 존재를 알린다.

## 변수 선언(Variable declaration)
* 변수를 생성하는것, 선언할 떄는 var,let,const keyword 사용.(keyword: 자바스크립트 엔진이 수행할 동작을 규정한 명령어)
* 변수 선언후 값을 주지 않으면 Js Engine에 의해 undefined가 할당되어 초기화됨.(undefined: Js가 제공하는 Primitive value(원시 타입의 값))
* 변수 선언 2단계:
	* Declaration phase(선언 단계): 변수 이름 등록으로 엔진에 변수의 존재를 알림
	* Initialization phase(초기화 단계): 값을 지정하기 위해 메모리 공간을 확보하고 암묵적으로 undefined 할당.
		* 변수 이름을 비릇한 모든 식별자는 실행 컨텍스트에 등록된다(execution context)
		* execution context: Js engine이 실행가능한 코드를 평가하고 실행하기위해 필요한 환경을 제공하고 코드의 실행 결과를 관리하는 영역. execution context를 통해 식별자, 스코프를 관리.
* 초기화단계(undefined 할당)을 거치지 않으면 확보된 메모리 공가넹는 이전에 다른 어플이 사용했던 값이 남아있을수있음. 이것을 Garbage value(쓰레기 값)이라 한다.

## 변수 선언의 실행 시점과 변수 호이스팅
* 변수 선언은 소스 코드가 순차적으로 한줄씩 실행되는 시점(run-time)이 아니라 그 전단계인 구문 분석(Syntax analysis)단계에 먼저 실행됨.
* JS engine은 순차적으로 실행하기 전에 먼저 소스 코드를 평가, 모든 선언문을 찾아내 식별자를 등록하고 초기화후, 선언문을 제외한 소스 코드를 한줄씩 순차적으로 실행.
* 변수 선언문이 코드의 선두로 올려진것처럼 동작하는 특징을 변수 호이스팅(variable hoisting)이라 한다.

## 값의 할당
* 변수에 값을 할당할 때는 할당 연산자(=)를 사용.
* var score = 80; 변수 선언과 값의 할당으로 구분하여 실행, 하지만!! 변수 선언은 소스 코드가 순차적으로 실행되기 전, 런타임 이전에 먼저 실행되지만 값의 할당은 순차적 실행 시점인 런타임에 실행됨.
	* var score;
	* score = 80;
* 이렇게 선언하는것과 같다.

## 재할당
* var keyword로 선언한 변수는 값 재할당 가능.
* 기존값을 버리고 새로운 값을 저장하는것.
* 재할당을 할 수 없어 저장된 값을 변경할수 없다면 상수(Constant)라 부른다.
* ES6에서 const키워드로 선언한 변수는 재할당이 금지된다. 따라서 const 키워드를 사용하여 상수를 표현할 수 있다.
* 값을 재할당 할때 기존 메모리 공간을 지우고 새로운것을 넣는게 아니고 새로운 메모리 공간을 확보하고 그 공간에 새로운 값을 저장한다.
* 이전 값은 어떤 변수도 갖고있지 않으므로, 불필요한 값들은 Garbage Collector에 의해 메모리에서 자동 해제된다. 단, 언제 해제될 지는 알 수 없다.
* 메모리 관리 방식에 따라 Unmanaged Language 와 Managed Language로 분류할수있다.
	* C 언어같은 Unmanaged Language는 개발자가 직접 메모리를 할당하고 해제하기 위해 malloc()과 free()같은 low-evel(저수준) 메모리 관리 기능을 제공. 개별자의 역량에 따라 최적의 퍼포먼스를 확보할수있지만, 반대로 치명적 오류를 생산할 가능성도 동시에 존재.
	* JavaScript 같은 Managed Language는 메모리의 할당/해제를 위한 메모리 관리 기능을 언어 차원에서 담당하고 개발자의 직접 제어를 허용하지 않음. 개발자가 명시적으로 할당/해제 불가. 더 이상 사용하지 않는 메모리의 해제는 Garbage Collector가 수행하며 이것도 개발자가 관여할수 없음. 개발자 역량에 의존하는부분은 작아짐, 퍼포먼스 면에서는 손실.

## 식별자 네이밍 규칙
* 식별자(identifier)는 네이밍 규칙을 준수해야한다.
	* 식별자는 특수문자를 제외한 문자, 숫자, underscore(_), 달러 기호($)를 포함할 수 있다.
	* 단, 식별자는 특수문자를 제외한 문자, underscore(_), 달러기호($)로 시작해야 한다. 숫자로 시작하는 것은 허용하지 않는다.
	* 예약어(reserved word)는 식별자로 사용할 수 없다
		* reserved word(예약어): 프로그래밍 언어에서 사용되고 있거나 사용될 예정인 단어들.
