* react is made up of components

  * typically made of JavaScript class, has a state, and render() function.
  * no longer need to manipulate DOM directly.
  * update the virtual DOM, and REACT responds by applying changes to real DOM.

* create-react-app installs:

  * a lightweight development server
  * Webpack for bundling files.
  * Babel for compiling JS code.

* Babel: modern Javascript compiler: changes jsx syntax into Javascript code that browsers understand

  ```
  // jsx
  
  const element = <h1>Hello World</h1>
  
  // converted code
  "use strict";
  
  var element = React.createElement("h1", null, "Hello World");
  ```

  

#### index.js

```
import React from 'react';
import ReactDOM from 'react-dom';

// able to use jsx syntax because of imported React
const element = <h1>Hello World</h1>
console.log(element);

// render virtualDOM element inside actual DOM:
// in actual use, renders App component(root component) instead of single element.
ReactDOM.render(element, document.getElementById('root'));
```

* when importing default exports, no need for destructuring ex: { component }

* jsx components must have one parent element.

  * React.Fragment
  * wraps components without having to wrap with \<div>

  ```
  class Counter extends Component {
    render() {
      // compiled by babel into React.createElement
      return (
      <React.Fragment>
        <h1>Hello World</h1><button>Increment</button>
      </React.Fragment>
      );
    }
  }
  ```



#### JSX

* JSX expressions are like JavaScript objects.

  * you can return from or pass into functions, use them as value of a variable or constant.

  ```
  const x = <h1>Zero</h1>
  ```

  

#### Rendering lists

```
import React, { Component } from 'react';

class Counter extends Component {
  state = {
    count: 0,
    tags: ['tag1', 'tag2', 'tag3']
  };


  render() {
    // compiled by babel into React.createElement
    return (
    <React.Fragment>
      <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
      <button className="btn btn-secondary btn-sm">Increment</button>
      <ul>
        {/* mapping string from tags into jsx elements. */}
    	{this.state.tags.map(tag => <li>{ tag }</li>) }
      </ul>
    </React.Fragment>
    );
  }

  // extracted (ctrl + shift + r)
  // code for rendering classes dynamically
  getBadgeClasses() {
    let classes = "badge m-2 badge-";
    classes += (this.state.count === 0 ? "warning" : "primary");
    return classes;
  }

  formatCount() {
    // destructuring count property from state;
    const { count } = this.state;
    return count === 0 ? <div>Zero</div> : count;
  }
}

export default Counter;
```

* Console gives us the following warning:

  >  Warning: Each child in a list should have a unique "key" prop. 

  * This is because when an element is changed in react,  it has to figure out which element has changed, and where in the DOM it should make changes to keep the DOM in sync with the virtual DOM.

  * If each child does not have a unique "key" property, react can't figure out which element has changed within the virtual DOM.

    ```
    {this.state.tags.map(tag => <li key={tag}>{ tag }</li>) }
    ```

    * A unique key must be assigned to each child.



#### Conditional Rendering

* Objective: render differently depending on state.tags

  ```
  import React, { Component } from 'react';
  
  class Counter extends Component {
    state = {
      count: 0,
      tags: ['tag1', 'tag2', 'tag3']
    };
    
    render() {
      return (
      <React.Fragment>
        <ul>
      	{this.state.tags.map(tag => <li>{ tag }</li>) }
        </ul>
      </React.Fragment>
      );
    }
  
  export default Counter;
  ```

* create a helper function for conditional rendering:

  ```
  import React, { Component } from 'react';
  
  class Counter extends Component {
  	state = {
  		count: 0,
  		tags: ['tag1', 'tag2', 'tag3']
  	};
  	
  	renderTags() {
  		if (this.state.tags.length === 0) return <p>There are no tags!</p>
  		
  		return <ul>{ this.state.tags.map(tag => <li key={tag}>{ tag }</li>) }</ul>
  	}
  	
  	render() {
  		return (
  			<React.Fragment>
  				{/* two ways of conditional rendering */}
  				{this.state.tags.length === 0 && 'Please create a new tag!'}	
  				{this.renderTags()}
  			</React.Fragment>
  		)
  	}
  }
  ```

  ```
  console.log(this.state.tags.length === 0 && 'Please create a new tag!')
  // Please create a new tag!
  ```

  * Because the first operand is true, the JS engine will continue the evaluation and the result will be the second operand.
  * **단축 평가**



## Handling Events

* Handling events in vanilla JS: you call the method when the event is triggered. First letter is capitalized.

  * $button.Onclick=handleIncrement();

* When handling events in React, you pass the function by reference.

  * events are camelCase, and case sensitive.
  * \<button onClick={this.handleIncrement}>\</button>

  ```
  import React, { Component } from 'react';
  
  class Counter extends Component {
    state = {
      count: 0,
    };
  
    handleIncrement() {
      console.log('Increment Clicked!', this);
    }
  
  
    render() {
      return (
      <React.Fragment>
        <span 
        	className={this.getBadgeClasses()}
        	>
        	{this.formatCount()}
        </span>
        <button
          onClick={this.handleIncrement}
          className="btn btn-secondary btn-sm"
          >
          Increment
        </button>
      </React.Fragment>
      );
    }
  
    getBadgeClasses() {
      let classes = "badge m-2 badge-";
      classes += (this.state.count === 0 ? "warning" : "primary");
      return classes;
    }
  
    formatCount() {
      const { count } = this.state;
      return count === 0 ? <div>Zero</div> : count;
    }
  }
  
  export default Counter;
  ```



* A TypeError occurs when event is triggered, stating this is undefined.

* Because handleIncrement is a stand-alone function, this by default returns a reference to the window object, but is undefined in strict mode.

  * (obj.method() vs function())

  ```
  class Counter extends Component {
    state = {
      count: 0,
    };
    
    constructor() {
    	console.log(this);
    }
  }
  ```

  * Error: this is not allowed before super()
  * super() must be used in all derived classes (extends).
    * Because a constructor was added to the child class, the constructor of the parent class must be called first using super().

  ```
  class Counter extends Component {
    state = {
      count: 0,
    };
    
    constructor() {
    	super();
    	this.handleIncrement.bind(this);
    }
    
    handleIncrement() {
    	console.log(this);
    }
  }
  ```

* By using the bind method, a new instance of the handleIncrement function will be returned.

  * this will now always reference the current object no matter how it is called.

  ```
  class Counter extends Component {
    state = {
      count: 0,
    };
    
    constructor() {
    	super();
    	this.handleIncrement = this.handleIncrement.bind(this);
    }
    
    handleIncrement() {
    	console.log(this);
    }
  }
  ```

  * handleIncrement() is now set to the function returned from the bind method.



#### this and arrow functions

* Another way to solve the 'this is undefined' problem
* In arrow functions, there are no bindings of **this**.
  * In regular functions, **this** represents the object that called the function.
  * With arrow functions, **this** always represents the object that *defined* the arrow function.
* **this** in arrow functions represent the *owner* of the function.
* Do not have to use constructor and super() to bind **this**.

```
handleIncrement = () => {
	console.log('Increment Clicked', this);
};
```





## Updating the State

* React is not aware of state changes without using setState() to tell it.

* **setState()**

  * Method inherited from base Component of React.
  * Tells React that state is updating.
  * Will sense when something is changed, and based on what part of the virtualDOM has changed, will sync with DOM.

  ```
  handleIncrement = () => {
    // cannot tell state has changed
    this.state.count++;
    // tells state is going to change
    this.setState({ count: this.state.count + 1 })
  }
  ```

* The setState method tells react that the state of the component is going to change.

  

