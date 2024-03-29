﻿

# 2019-10-01 기본개념, Javascript
* 프로그래밍이란: 컴퓨터에게 실행명령을 내리는 일종의 커뮤니케이션. 컴퓨터가 인간의 의도를 알아들을수있도록 컴퓨팅적인 사고로 생각을 하고 프로그래밍을 해야한다.

* ascii code, unicode: 사람의 문자들을 컴퓨터가 이해할수 있게 만든것
  * ascii code(America Standard Code for Information Interchange): 8비트 문자코드이며 비트 하나하나에 유니크한 문자가 들어있음. 8비트지만 하나의 비트는 통신용으로 사용. 256가지 경우의 수를 가지고있으며, 경우들이 서로 다른문자를 나타냄. 256가지 경우의수로 모든 언어를 나타낼수 없다. 8-bit 인코딩사용.
  * unicode: 유니코드는 ascii코드의 superset(확장판).
    0~127의 숫자가 ascii코드와 동일한 값. 각 문자마다 Code Point를 주고, 인코딩 선언으로 비트로 나타낸다. Variable bit encoding 사용: UTF-8, UTF-16, UTF-32 등, 인코딩은 문자하나가 가지는 비트를 정한다.


### compiler/interpreter:
컴퓨터는 0과 1밖에 이해할수 없다. 이런 코드를 machine code라고 부른다. 인간의 언어로 만든 프로그램은 source code라고 한다. 소스코드를 머신코드로 변환하기위해  compiler와 interpreter를 사용한다. 

#### Interpreter: 
* 프로그램을 한 statement씩 변환한다.
* 소스코드 분석시간이 적지만, 전체적인 실행시간이 길다.
* intermediate object code(소스코드 에서 머신코드로 변환하는 과정에 컴퓨터가 생성하는 중앙레벨 코드)가 필요없으므로, 메모리를 비교적 적게사용.
* 첫 에러 발견시 작동이 멈춰서 debugging이 쉽다.
* python, ruby, JavaScript등이 사용.

#### Compiler
* 정보를 수집후 실행파일을 만든다.
* 한번에 전체영역을 몰아서 번역, 소스코드 분석은 느리지만 전체적 실행속도는 빠르다.
* 변환과정에 링킹이 추가로 필요한 intermediate object code를 생성해서 용량을 많이먹는다.
* 전체프로그램을 스캔한 후에 에러메세지가 뜸으로 디버깅이 비교적 힘들다.
* C, C++등이 사용.

## Syntax and Semantics
Syntax = 문법(permitted phrases)
Semantics = 의미(associated meaning of phrases)
코드는 문법과 의미가 맞야야한다.

## JavaScript 탄생, 역사
* 1996년 3월에 "mocha" 라는 이름으로 탄생
* 9월에 "LiveScript"로 이름 변경, 12월에 "JavaScript"로 이름 바뀜.
* 마이크로소프트가 Internet Explorer 3.0에 JScript라는 언어 탑재, 자바스크립트와 JScript는 표준화되지 못하여 크로스브라우징에 문제가 생겼다. 
* 1997년 7월, 표준화된 자바스크립트 초판(ECMAScript1)의 사양이 완성되었고 JavaScript는 ECMAScript로 명명됨.
* ES3이후에 ES4는 decline당했고, 10년후 2009년에 ES5가 출시되었다.
* 2016년도에 ES6가 출시되엇고, 이버전 이후부터 모던 자바스크립트라 부를수있다.

## ECMAScript, JavaScript
* ECMAScript는 자바스크립트의 표준 사양인 ECMA-262를 말함.
* 표준 빌트인 객체(언어의 타입, 값, 함수 등)과 핵심 문법을 규정한ㄷ.
* 각 브라우저 제조사는 이를 준수하여 브라우저 JavaScript엔진을 구현.
* JavaScript는 웹브라우저에서 동작하는 유일한 프로그래밍언어, interpreter 언어이다.( 사실 compiler, interpreter 장점 결합함)
* 다른 언어들과 다르게 프로토타입 기반 상속이되고, 일급 함수 개념으로 함수형 프로그래밍이 가능하다.
* JavaScript는 일반적으로 ECMAScript와 브라우저가 별도 지원하는 client-side Web API(DOM,BOM,SVG,Web Storage) 등을 아우르는 개념. 
* JavaScript는 명령형(imperative), 함수형(functional), 프로토타입 기반(prototype-based) 객채지향 프로그래밍을 지원하는 멀티패러다임(객체지향형, 절차지향형(명령형), 함수지향형 다되는) 언어.

## Ajax
* JavaScript로 서버와 브라우저가 비동기적(asynchronous)으로 데이터를 교환할수 있게 해주는 통신 기능
* 서버로부터 필요한 데이터만 받아서 한정적인 부분만 랜더링하는 방식이 가능해짐.
* Google에서 2005년에 Ajax기반으로 동작 Google Maps 발표, 화면에 지도가 움직일때마다 reloading되지 않고 부드럽게 이동됨.

## DOM(Document Object Model)
* 문서의 구조를 나타냄으로 웹페이지를 스크립트나 프로그래밍언어에 연결시켜준다.
* DOM은 문서를 나무형식으로 논리적으로 나타낸다. 나무의 브랜치마다 노드로 끝나고, 노드마다 객체를 갖는다.
* DOM method들은 나무에 대한 프로그래밍적 접근을 할수있게해준다, 문서의 구조, 스타일이나 콘텐츠를 변경할수있다.
* 노드들에 추가로 event handler를 줄수있다, 이벤트가 일어나면 event handler들이 실행된다.

##jQuery
* 2006년에 등장하므로 번거롭고 논란이 있던 DOM을 제어할수 있게되었고 크로스브라우징 상황도 나아졌다. 배우기 쉽고 직관적이어서 jQuery를 JavaScript보다 선호하는 개발자들이 생기기도했지만, 현재는 많이 안쓰는쪽으로 가고있따.

##V8 JavaScript Engine
* 빠르게 동작하는 JavaScript 엔진.
* V8의 등장으로 JavaScript는 데스크톱 애플리케이션급 사용자 경험(user experience)를 제공할수 있는 웹 어플 개발 언어로 정착.
* 과거 웹 서버에서 수행되던 역할들이 많이 브라우저쪽으로 이동하였고, 웹 어플 개발에서 front end 영역이 주목받게된계기.

## Node.js
* V8 JavaScript Engine 탑재, 브라우저 밖에서도 JavaScrpt 사용을 가능하게함.
* front end영역뿐만아니라, back end 영역까지에서도 사용하는 언어가 됨.
* 이로써 자바스크립트는 cross platform을 위한 가장 중요한 언어로 주목받고있다.

## SPA 프레임워크
* 모던 웹 어플이 이제 데스크톱 어플과 비교해도 될정도의 고성능과 사용자경험을 제공해야되었고, 규모와 복잡도가 상승했다. 
* 유연하면서 확장이 쉬운 어플 구조를 구축하였고, 프레임워크가 등장하게됨.
* CBD(Component based development) 방법론을 기반으로 Angular, React, Vue.js 등 많은 사람들이 다양한 SPA 프레임워크/라이브러리 사용

## CBD(Component based development)
* CBD(컴포넌트-기반 개발)는 재사용성이 있는 소프트웨어 컴포넌트들로 컴퓨터 기반 시스템의 디자인과 개발을 수월하게 해주는것이다.
* 복잡한 소프트웨어 시스템을 만들때 개발시간을 줄여주고, 소프트웨어 퀄리티도 올려준다.
