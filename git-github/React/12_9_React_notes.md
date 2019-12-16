* 별도의 fetch module을 사용하지 않는다면 axios사용 권장.
* 비동기 코드에서 forEach는 순서가 보장되지 않아서 forEach를 사용하면 안된다.
  * for문 가능.
* async/await에 try/catch를 사용하면 코드에 문제가 생겼을때 에러가 발생하는 시점에서 중단되고 catch로 넘어가서 에러 처리를 하고 코드를 게속 실행한다.
  * catch가 없다면 다음 코드로 실행이 넘어가지 않기 때문에 쓰는것이 좋다.

* HTML to JSX converter로 HTML을 쉽게 변환가능.
* react debounce: 변화가 될때마다 지연시간 이후에 마지막 이벤트만 실행되게 한다.
  * npm i lodash --save 로 download후 import 해야한다.
    * JS에서 사용하는 중요한 함수들을 묶어둔 패키지.
* state를 사용하기 위해 class 최상위 컴포넌트를 사용한다.
  * app.js 하위에 정의된 컴포넌트들은 state(상태)가 없다.
  * 상위에서 상태 변화를 시킬수 있는 함수를 만들고, props로 하위 컴포넌트들로 전달시켜 준다.
* state를 가지고 있는건 app.js밖에 없다.
  * 하위 컴포넌트들은 app.js의 props를 전달해 함수를 만들어 state를 변화 시킨다.

* higher arrow function? queryfunction HOC(high order component)

  ```
  const SearchBar = () => {
    // HOC: High order component
    // props.onSearchVideos가 search로 대입시킨다.
    // event handler에 arrow function을 다는 것과 같다.
    // e => {}를 return 한다.
    const handleEnter = search => e => {
      if (e.key === 'Enter') {
        search(e.target.value)
      }
    }
    return (
      <div className="search-wrapper">
        <input
         type="search"
         onChange={e => props.setInput(e.target.value)}
         onKeyPress={handleEnter(props.onSearchVideos)}
         className='search-bar'
         placeholder='검색어를 입력하세요.'
         >
  ```

  * HOC: High order component
    props.onSearchVideos가 search로 대입시킨다.
    event handler에 arrow function을 달지 않아도 된다.

* npm i react-infinite-scroller --save
  * --save를 하면 package.json에 save해둔다.

* UUID

  * 충돌이 일어나지 않는 고유의 문자열을 만들어준다. random string generator

    ```
    <div key={uuid.v4()}/>
    ```

  * npm i uuid --save

* componentDidUpdate: 업데이트되었을 경우에만 실행.

* componentWillMount: 랜더 이전에 실행.

* componentDidMount: 랜더 이후에 실행.