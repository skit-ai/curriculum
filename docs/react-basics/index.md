### REACT BASICS

In this document we will be going through some basics of REACT , especially react-hooks since we use that on a daily basis. This document covers the basics of react hooks , some ideologies in React , and some facts that would be helpful to a beginner.
We assume that you have a basic familiarity in HTML,CSS & JS.
If not we recommend to get a basic understanding of those fields from
[here](https://www.youtube.com/watch?v=hdI2bqOjy3c) and [here](https://www.youtube.com/watch?v=UB1O30fR-EE&list=PLillGF-RfqbZTASqIqdvm1R5mLrQq79CU).
Nevertheless we will go through some concepts of react that might be interesting to some ;).

# Introduction

React is a declarative, efficient, and flexible JavaScript library for building user interfaces. It lets you compose complex UIs from small and isolated pieces of code called “components”.
In react one might have seen earlier strange mixture of HTML and JavaScript inside each component. React actually uses a language called JSX that allows HTML to be mixed with JavaScript.
Not only can you use JSX to return pre-defined HTML elements, you can also create your own. For example, instead of rendering <h2> elements directly in the class component, you can render the functional component which returns the same thing.
So lets start by understanding some fundamental concepts of react.

- state
  In React we keep the data in regular JS variables and maintains its own virtual DOM(Document Object Model). So basically whenever you want to update something in the DOM we have to locate the appropriate node and then manually append or remove elements. React then compares the virtual DOM and the actual DOM by checking the application state. It then updates the UI accordingly.
  For example if we store a counter value and two buttons for increment and decrement.

```jsx
const Timer = () => {
  const [counter, setCounter] = useState(0);
};
```

We stored the value counter having initial value 0 and a callback function for setting counter value. In this we used a hook useState which we will discuss later on. We should always keep in my mind that **Data everytime flows down**

Using State in a right manner.

1. Do not modify the state directly.
2. State updates maybe asynchronous.
3. State updates are merged.

```jsx
const Timer = () => {
  const [counter, setCounter] = useState(0);
  const handleDecrement = () => {
    setCounter((prevState) => prevState - 1);
  };
  const handleIncrement = () => {
    setCounter((prevState) => prevState + 1);
  };
  return (
    <div>
      <h2>{counter}</h2>
      <button onClick={handleDecrement}>Decrement</button>
      <button onClick={handleIncrement}>Increment</button>
    </div>
  );
};
```

We updated the state by calling setCounter in each of the functions handling a button click. The counter displayed on the page will update in real time. Thus, React gets its name because it reacts to state changes.

In short, React automatically monitors every component state for changes and updates the DOM appropriately.

- props
  Props can be considered as properties of a component which we pass through to define certain aspect of the UI.

```JSX
const Display = (props) => {
    return(
        <div>
            {props.counter ? (<h1>Yes Positivity</h1>) : (<h1> NO Negativity</h1>)}
        </div>
    )
}

const Timer = () => {
    const [state , setState] = useState("0")
    return(
        <>
            <Display counter={state}/>
        </>
    )
}
```

In here you can see we are accessing the counter variable like a props counter in the Display component.

- component lifecycle

In updating the UI , react follows various norms which can be coined to be its lifecycle.
It has its phases from initialization to mountin to updating state to unmounting the component.

Some lifecycle methods are

shouldComponentUpdate() Function: By default, every state or props update re-render the page but this may not always be the desired outcome, sometimes it is desired that updating the page will not be repainted. The shouldComponentUpdate() Function fulfills the requirement by letting React know whether the component’s output will be affected by the update or not. shouldComponentUpdate() is invoked before rendering an already mounted component when new props or state are being received. If returned false then the subsequent steps of rendering will not be carried out. This function can’t be used in the case of forceUpdate(). The Function takes the new Props and new State as the arguments and returns whether to re-render or not.

componentDidUpdate() Function: tThis function is invoked after the component is rerendered i.e. this function gets invoked once after the render() function is executed after the updation of State or Props.

You can take a look at the examples given [here](https://reactjs.org/docs/state-and-lifecycle.html)

So lets start by analysing what do we mean by components and how do we set it up.

Here is an example of simple navbar.

```jsx
const Awesomenav = () => {
  return (
    <div>
      <nav>
        <ul>
          <li>Nav1</li>
          <li>Nav2</li>
          <li>Nav3</li>
          <li>Nav4</li>
        </ul>
      </nav>
    </div>
  );
};
export default Awesomenav;
```

You can write the above piece of code multiple times wherever you need but after a time it becomes tedious.
Instead you can follow write once read everywhere principle.

```jsx
import Awesomenav from "<specified folder>"
//just import it and use it anywhere.
<div>
    <Awesomenav>
</div>
```

You can just import the above piece of code as a component and can use it anyhwere.
This is an basic example of how one can use components.

Now we would dive a bit into different types of hooks available for us to use.

- useState hook

This hook basically deals with setting up the state of the component. As you would have seen in examples given above we have used the useState to establish an identity of an object , variable in the component.

```jsx
import {useState} from "react";
const App = () => {
    const [counter , setCounter] = useState(0)
    ...
}
```

In the above example the useState return the state i.e variable counter and a function (setCounter) to set the counter variable.

- useEffect hook
  The Effect Hook lets you perform side effects in function components:

```jsx
import { useState, useEffect } from "react";
const Example = () => {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:  useEffect(() => {    // Update the document title using the browser API    document.title = `You clicked ${count} times`;  });
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
};
```

Data fetching, setting up a subscription, and manually changing the DOM in React components are all examples of side effects.
The useEffect Hook can be determined as componentDidMount, componentDidUpdate, and componentWillUnmount combined.

- Exercise for the react basic \*
  There is a exercise folder given in the directory. You have been given the designs for creating a todolist app.

[^1]:
    - https://www.geeksforgeeks.org/reactjs-lifecycle-components/
    - https://reactjs.org/docs/getting-started.html
