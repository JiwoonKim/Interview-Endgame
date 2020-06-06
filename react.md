## :star: React Interview Questions & Answers

| No. | Questions |
|:---:|:---|
| :dart:  | __Core React__ |
| 1 | What is React? |
| 2 | What are the major features of React? |
| 3 | What is JSX? |
| 4 | What is a React element? |
| 5 | What is a component? |
| 6 | How is a component rendered to the page? |
| 7 | What are props? |
| 8 | What is a state? |
| 9 | What is the difference between state and props? |
| 10 | Why should state not be updated directly? |
| 11 | What are lifecycle methods? |
| 12 | How does React have a unidirectional data flow? |
| 13 | |
| :rocket:  | __Optimizations__ |
| 1 | What is the VirtualDOM and how does it work? |

### references
  - [React Documentation: Main Concepts](https://reactjs.org/docs/hello-world.html)
  - [Glossary of React Terms Documentation](https://reactjs.org/docs/glossary.html#react-elements)
  - [React Interview Questions List](https://github.com/sudheerj/reactjs-interview-questions#what-is-react)

## :dart: Core React

1. ### What is React?

   React is an __open-source frontend JavaScript library__ used for building user interfaces especially for single page applications. 

2. ### What are the major features of React?

   The major features of React are:

   - It uses __VirtualDOM__ instead RealDOM considering that RealDOM manipulations are expensive.
   - Follows __Unidirectional data flow__ or data binding.
   - Uses __reusable/composable UI components__ to develop the view.
   
3. ### What is JSX?

   JSX is a XML-like __syntax extension to JavaScript__ (acronym for _JavaScript XML_). Basically it just provides syntactic sugar to describe what the UI should look like using a HTML-like template syntax combined with the power of JavaScript.
   
   While React does not require using JSX, it is widely __used as a visual aid when working with UI inside JavaScript code__. It also allows React to show more useful error and warning messages.
   
   > JSX gets compiled to `React.createElement()` calls which return plain JavaScript objects called React elements.

4. ### What is a React element?

   A React element is a __plain object describing what you want to see on the screen__ (i.e. a component instance or DOM node and its desired properties). It contains only information about the component type (for example, a Button), its properties (for example, its color), and any child elements inside it.
   
   
   ```js
   // JSX
   const element = <h1 className="container">Hello, world</h1>;
   
   // ...compiles to element creation calls
   const element = React.createElement(
      'div',
      {className: 'container'},
      'Hello, world'
   )
   
   // ...final result is element
   {
      type: 'h1',
      props: {
        className: 'container',
        children: 'Hello, world',
      }
    }
   ```
   
   Elements were introduced in need of __solving the problem of traditional object-oriented UI programming__ (working with component classes and instances). In the traditional UI model, it was up to the developer to take care of _creating and destroying child component instances, and manually keep them up to date with any new information_. Since the parents needed direct access to the children component instances, it also made it _hard to decouple them in the future_.

   Elements solve these problems since they are __just descriptions and not the actual instances__. They don’t refer to anything on the screen when you create them. You can create them and throw them away, and it won’t matter much. They are easy to traverse, don’t need to be parsed. Since they are just objects, they are __much lighter than the actual DOM elements__, making them cheap to create compared to browser DOM elements.

   Typically, elements are not used directly, but get returned from components. And since an element's type can be a DOM node or a React component, __DOM and component elements are mixed and matched in a single element tree__. This composition structure ensures components can be decoupled from each other.
   
   - reference: https://reactjs.org/blog/2015/12/18/react-components-elements-and-instances.html
   
5. ### What is a component?
 
   React components are __small, reusable pieces of code__ that return a React element to be rendered to the page. They __accept arbitrary inputs (called props) and return React elements__ describing what should appear on the screen.
   
    Components can be defined by two ways: as functions and as ES6 classes.
   
   ```js
   // defined as function                   
   function App(props) {                   
      return <h1>Hello, {props.name}</h1>;
   }
   ```
   ```js
   // defined as ES6 class
   class Welcome extends React.Component {
      render() {
         return <h1>Hello, {this.props.name}</h1>;
      }
   }
   ```
   
6. ### How is a component rendered to the page?
   Components are rendered by using the `ReactDOM.render()` method.
```
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

7. ### What are props?
   Props are __inputs to components__. They are __data passed down from a parent component to a child component__. Since they are read-only, they should note be modified in any way.

8. ### What is a state?
   A state of a component is an __object that holds some information that may change over the lifetime of the component__. State is __used for internal communication inside component__.
   

9. ### What is the difference between state and props?
   Both props and state are plain JavaScript objects. 
   
   While both of them hold information that influences the output of render, they are different in their functionality with respect to component. The differences between the two are:
   - __props are passed from a parent component, but state is managed by the component itself__. 
   - A component __cannot change its props, but it can change its state__. 

10. ### Why should state not be updated directly

11. ### What are lifecycle methods?
    Lifecycle methods are functions executed according to the different phases of a component. It's main purpose is to __add functionality to the different phases of a component__, when it is created, updated, and destroyed.
    
    ![image](https://user-images.githubusercontent.com/29671309/83942527-135cce80-a82f-11ea-8ca2-c38e88583e31.png)
    
    #### Mounting
    when an instance of a component is being created and inserted into the DOM
    - __`constructor()`__: initialize local state and you bind event handlers to component instance
    - __`render()`__: returns React elements
    - React updates DOM & refs
    - __`componentDidMount()`__: execute side-effects (i.e. request data via network, set up subscriptions, call `setState`)
    
    #### Updating
    when a component is being re-rendered due to changes to props or state
    - new props, setState(), forceUpdate() trigger update
    - __`render()`__: returns React elements
    - React updates DOM & refs
    - __`componentDidUpdate()`__: execute side-effects (i.e. request data via network, set up subscriptions, call `setState`)
      - avoid calling `setState()` directly in componentDidUpdate() method since it creates an infinite loop (if necessary, use with condition)
    
    #### Unmounting
    when a component is being removed from the DOM
    - __`componentWillUnmount()`__: cleanup before component is unmounted
      - invalidate timer, cancel network requests and subscriptions
    
12. ### How does React have a unidirectional data flow?
    This is commonly called a “top-down” or “unidirectional” data flow. Any state is always owned by some specific component, and any data or UI derived from that state can only affect components “below” them in the tree.
If you imagine a component tree as a waterfall of props, each component’s state is like an additional water source that joins it at an arbitrary point but also flows down.
To show that all components are truly isolated, 

## :rocket: Optimizations

1. ### What is the VirtualDOM and how does it work?
