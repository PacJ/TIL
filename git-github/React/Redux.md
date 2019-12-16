## Redux

* Open source library for managing application state.

* Based on Flux.

* 모든 state를 최상위 component에 보관하는 vanilla react.

  * 각각의 state를 관리해야할 때 사용한다.
  * 필요가 명확하지 않으면 사용하지 말자.
  * 최상위 store에 component의 state들을 보관시킨다.

* Actions(Changing state), Reducers(function receives action as a parameter), store(manages states)

  * State is read-only
    * **The only way to change the state is to emit an action, an object describing what happened.**
  * **To specify how the state tree is transformed by actions, you write pure reducers.** 
    * Mutable arguments, creating side effects, impure functions are all forbidden in reducers.
  * 모든 상태변화를 명백하게 예측하기 위해 사용하기 때문에, pure function을 기반으로 변화를 준다.

* Has one immutable store, actions trigger changes, reducers update state.

  * state에 대해 직접 변경하지 않고, 업데이트를 한다.

    ```
    return ({
    	...state
    	query: NewQuery
    })
    ```

* Action은 객체로 되어있고, { type: change, rating: 5} type빼고 다른 property들(rating)을 변경하라는 것이다.

* pure function: 자신의 parameter에 의해서만 반환값이 결정되고, 외부에 어떠한 영향을 주지 않는 함수.



### reducer

* All reducers are called on each dispatch.
* actions are dispatched(dispatch.action) allowing states to be updated.
* The reducer function receives the action as a parameter.



### redux store

* **"single source of truth"**

* **Immutable**

* to change a state, a new object must be returned(does not mutate state)

  ```
  state = {
  	name: 'Ivan',
  	role: 'developer'
  }
  
  return state = {
  	name: 'Ivan',
  	role: 'admin'
  }
  ```

  * Object.assign ( {}, state, { role: 'admin' }); 

  * 일반적으로 reducer parameter로 (기존 상태, Action)을 인수로 전달한다.

    

* React is like a wallet, you can put money(states) in your wallet, but there also is the possibility of losing it. Redux is a bank. The store is like a bank account. Every time your balance changes(Action), a new line of transaction information is added with your balance is updated(Reducer).
  * React는 state를 직접 변경하고 접근하고 관리할 수 있다.
    * state = 'New State'
  * Redux는 명백하고 체계적으로 state를 관리할 수 있다.



#### Provider

* Redux의 store를 React에서 제공해주고, 하위 component들에게 store를 제공해준다.
* <Provider store={createStore(reducers)}
  * The only way to change the data in store is to call dispatch() on it.
  * createStore의 인수로 reducers를 넣어준다.

* Actions:

  ```
  export const CALC = 'CALC'
  
  // action을 전달하기 위한 함수.
  export function calc() {
    // action creator
    return({ type: CALC, val })
  }
  ```

* Reducers:

  ```
  import { CALC } from '../actions'
  
  const INITIAL_STATE = {
    count: 0
  }
  
  export default function counter(state = INITIAL_STATE, action) {
    switch(action.type) {
      case CALC:
        return {
          ...state,
          count: state.count + action.val
        }
      default:
        return state
    }
  }
  ```

  

