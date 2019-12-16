# Babel과 Webpack을 이용한 ES6 환경 구축

## Babel

#### Babel이란?

* transfiling 작업으로 EcmaScript의 버젼을 내려준다.

* 크로스 브라우징을 위해 하위 버전에 호환 가능하도록 최신 ES문법을 사용하여도 하위버젼 문법으로 transfiling해준다.

* browser 환경에서는 babel만으로 실행이 안된다. Node.js의 Commonjs의 require를 모른다.



## Webpack

#### Webpack이란?

* 의존 관계에 있는 모듈들을 하나의 자바스크립트 파일로 번들링한다.
* HTML의 script태그를 여러개 사용해야하는 번거로움도 사라진다.

* Webpack이 바벨을 사용해 컴파일을 하고 번들링을한다.
*  webpack.config.js은 Webpack이 실행될 때 참조하는 설정 파일이다. 



**DB**

* RDB(relative database)
  * graph/table로 되어있다.
  * 한줄을 Record라 부르는데, 이걸 가져오는 것이 Query다.
* NoSQL
  * SQL을 쓰지 않고, 함수로 Query를 한다.
  * MongoDB