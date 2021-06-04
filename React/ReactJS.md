# React Notes


### Key aspects of Functional Programming

* **First class Objects**
    * In JS, functions are first class objects.
    * So JS have concept of Higher-Order-Functions (HoF).
    * React have similar concept of Higher-Order-Components (HoC), treat components as functions and enhance it with behaviours.
* <b>Purity</b> - A pure function is when there is no side effects, which means function does not change anything that is not local to the functions itself. Sample is below -
    ```const add = (x, y) => x + y ``` 
* <b>Immutability</b>
* <b>Currying</b> is the process of converting a function that takes multiple arguments into a function that takes on argument at a time, returning another function.
* <b>Composition</b> Functions or components can be combined to produce new functions/components with more advanced features and properties.

* <b>FP and UI</b> ```UI = f(state)```  This function is idempotent (Idempotence is the property of certain operations in mathematics and computer science whereby they can be applied multiple times without changing the result beyond the initial application). Components can be composed to form the final UI, which is property of FP.

## PropTypes
Define the type of Props a React Component can accept, Default value of Props if not provided by parent.
```js
class Button extends React.Component { 
  render() { 
    return <button>{this.props.text}</button> 
  } 
} 
 
Button.propTypes = { 
  text: React.PropTypes.string, 
} 
 
Button.defaultProps = { 
  text: 'Click me!', 
} 
```

## State

Classes we define our initial state using the state attribute of the instance and setting it inside the constructor method of the class:
```
With classes we just define properties on the instance without using any React-specific APIs, which is good. 
In ES2015, to use this in sub-classes, we first must call super. In the case of React we also pass the props to the parent.
```
```js
class Button extends React.Component { 
  constructor(props) { 
    super(props) 
 
    this.state = { 
      text: 'Click me!', 
    } 
  } 
 
  render() { 
    return <button>{this.state.text}</button> 
  } 
} 
```

## Autobinding

Autobinding of ```this``` works differently with classes. The result would be a null output in the console when the button is clicked if event handler is not binded with ```this```. This is because our function gets passed to the event handler and we lose the reference to the component.

That does not mean that we cannot use event handlers with classes, we just have to bind our functions manually.
```js
class Button extends React.Component { 
  constructor(props) { 
    super(props) 
    // Performance Benefit over <button onClick={() => this.handleClick()} />
    this.handleClick = this.handleClick.bind(this) 
  } 
 
  handleClick() { 
    console.log(this) 
  } 
 
  render() { 
    return <button onClick={this.handleClick} /> 
  } 
} 
```
## Stateless Functional Components (SFC)
### Context
**Context provides a way to pass data through the component tree without having to pass props down manually at every level.**
In React apps, data is passed from parent to child (top-down) using props. In some cases (e.g. Themes, Local, Authentication, etc), this approach is cubersome and app debugging is troublesome.
Using Context, application share data between components without having to explicily pass a prop throguh every level of the tree. Data is defined at the node of a tree and shared with child nodes.

### Props 
* Components that are not able to receive any props from the parents are not particularly useful.
* stateless functional components can receive props as parameters.

```js
// ES2015 Construct
const Button = ({ text }) => <button>{text}</button> 

Button.propTypes = { 
  text: React.PropTypes.string, 
} 
```
Stateless functional components also receive a second parameter which represents the context:
```js
(props, context) => ( 
    <button>{context.currency}{props.value}</button> 
) 
```


### Lifecycle
* SFC do not provide any lifecycle hooks.
* SFC only implement a render-like method
* SFC is staeless, so ```this``` does not represent component during their execution.
### Event Handlers
No component instance, use eventhandlers with SFC as below -
```js
() => { 
  let input 
 
  const onClick = () => input.focus() 
 
  return ( 
    <div> 
      <input ref={el => (input = el)} /> 
      <button onClick={onClick}>Focus</button> 
    </div> 
  ) 
} 
```

## The state - Stateful React Component (SRC)
* SRC can have an initial state.
* During the lifetime of component, state can be modified multiple times using ```setState```
* Everytime state changes, React renders the component again with new state.
* _React component is similar to state machine_
* setState function is asynchronous.
* setState Method is called with a new state, the object merged into the current state. Example below - 
```js
this.state = { 
  text: 'Click me!', 
}
//And we run setState with a new parameter:
this.setState({ 
  cliked: true, 
}) 
//The resulting state is:
/* 
{ 
  cliked: true, 
  text: 'Click me!', 
} */
```
### Where to use state
* Miminal amount of data needed.
* Only those values, whose change will render the component again.
* Don't keep something in the state, if we don't use it for rendering.