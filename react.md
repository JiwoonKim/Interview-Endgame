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
| 10 | Why should state not be modified directly? |
| 11 | What are the benefits of batching setState calls? |
| 12 | How does React have a unidirectional data flow? |
| 13 | What are lifecycle methods? |
| 14 | What is the difference between controlled and uncontrolled components? |
| 15 | What is the benefit of using composition over inheritance in React? |
| 16 | |
| :anchor: | __Hooks__ |
| 1 | What are hooks and why are they used? |
| 2 | How does the useEffect hook work? |
| :rocket:  | __Optimizations__ |
| 1 | What is the VirtualDOM and how does it work? |
| 2 | What are "key" props and what is the benefit of using them in arrays of elements? |
| 3 | What is memoization and how does it improve the performance in React? |

### references
  - [React Documentation: Main Concepts](https://reactjs.org/docs/hello-world.html)
  - [Glossary of React Terms Documentation](https://reactjs.org/docs/glossary.html#react-elements)
  - [React Interview Questions List](https://github.com/sudheerj/reactjs-interview-questions#what-is-react)

## :dart: Core React

1. ### What is React?

   React is an open-source __frontend JavaScript library used for building user interfaces__ especially for single page applications. 

2. ### What are the major features of React?

   The major features of React are:

   - It uses [__VirtualDOM__](#what-is-the-virtualdom-and-how-does-it-work) instead RealDOM considering that RealDOM manipulations are expensive.
   - Follows [__Unidirectional data flow__](#how-does-react-have-a-unidirectional-data-flow) or data binding.
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
   Props are __inputs to components__. They are __data passed down from a parent component to a child component__. Since they are read-only, they should not be modified in any way.

8. ### What is a state?
   A state of a component is an __object that holds some information that may change over the lifetime of the component__. State is __used for internal communication inside component__.
   
9. ### What is the difference between state and props?
   Both props and state are plain JavaScript objects. 
   
   While both of them hold information that influences the output of render, they are different in their functionality with respect to component. The differences between the two are:
   - __props are passed from a parent component, but state is managed by the component itself__. 
   - A component __cannot change its props, but it can change its state__. 

10. ### Why should state not be modified directly?
    Modifying state directly is problematic since __it does not trigger re-rendering of a component__. Tt is recommended to initialize `this.state` only in the constructor and use `setState()` for updating instead.
    
    ```js
    // React MERGES the object provided into the current state
    this.setState({ message: 'Hello World' })
    ```
    
    The beauty of using `setState()` is that it allows us to __let React know that the component state has changed__. This way the component knows it should re-render, because its state has changed and its UI will most likely also change. This is much __more performant than continuously checking changes in an object__ for whether a property has changed (known as "dirty checking"). By using the built-in `setState`, React already knows because it is notified of what changes should be implemented.
    
    - reference: https://learn.co/lessons/react-updating-state

11. ### What are the benefits of batching setState calls?
    React may __batch multiple setState() calls into a single update for performance__ since setState always triggers a re-render of the component. So even if a child and parent component each call setState() when handling a single event, the child component will not be re-rendered twice. No matter how many setState() calls in how many components you do inside a React event handler, they will produce only a single re-render at the end of the event.
    
    - reference: https://github.com/facebook/react/issues/11527#issuecomment-360199710
    
12. ### How does React have a unidirectional data flow?
    __Data flows downwards in React's component tree__. _State is always owned and contained within a specific component_, and _any data or UI derived from that state can only affect component below them in the tree_.
    
    State is local or encapsulated to a component. It is not accessible to any component other than the one that owns and sets it. The only __way to share data is to pass its state down as props to its child components__, which is why the data flow is depicted as _top-down_ or _unidirectional_. This is why sharing state is accomplished by moving it up to the closest common ancestor of the components that need it, called _lifting state up_. 

13. ### What are lifecycle methods?
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
      
14. ### What is the difference between controlled and uncontrolled components?
    React has two different approaches __to dealing with form inputs__:
    
    - __Controlled Component__: _form data is handled by a React component_. When a user enters data into a controlled component a _change event handler is triggered and your code decides whether the input is valid_ (by re-rendering with the updated value). If you do not re-render then the form element will remain unchanged.
    - __Uncontrolled Component__: _works like form elements do outside of React_. When a user inputs data into a form field (an input box, dropdown, etc) the updated information is _reflected without React needing to do anything_ (since HTML Form elements such as `<input>`, `<textarea>`, `<select>` naturally keep its own internal state). However, this also means that you can’t force the field to have a certain value.
    
    In most cases, it is recommended to use controlled components.
    
15. ### What is the benefit of using composition over inheritance in React?
    __Props and composition are a more flexible and safe way to reuse code between components__. Since components can accept aribitrary props (including primitive values, React elements, or functions), it is possible __to customize a component's look and behavior by using props and composition__. 
    Examples of using props and composition to reuse code between components:
    1. Containment: use the `props.children` to create generic components accepting arbitrary elements
    ```jsx
    function Box(props) {
      return <div>{props.children}</div>
    }
    function HelloBox() {
      return (
        <Box>
          <h1>Hello, world</h1>
          <p>This is React working under the hood</p>
        </Box>
      )
    }
    ```
    2. Specialization: use specific value for props to make special cases of a generic component
    ```jsx
    function Box(props) {
      return (
        <div>
          <h1>{props.title}<h2>
          <p>{props.description}</p>
        </div>
    }
    function HelloBox() {
      return (
        <Box title="Hello, world" description="React in the works" />
      )
    }
    ```
    
    This is a much flexible approach than using inheritance to extend components since components are not coupled.
    
    - cf. inheritance depicts a _is-a_ relationship, while composition depicts a _has-a_ relationship.
    

## :anchor: Hooks

1. ### What are hooks
   Hooks are __functions that let you “hook into” React state and lifecycle features from function components__. Hooks don’t work inside classes — they let you use React without classes.
   
   

## :rocket: Optimizations

1. ### What is the VirtualDOM and how does it work?

2. ###
   Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity:
   A “key” is a special string attribute you need to include when creating arrays of elements. Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside an array to give the elements a stable identity.
Keys only need to be unique among sibling elements in the same array. They don’t need to be unique across the whole application or even a single component.
Don’t pass something like Math.random() to keys. It is important that keys have a “stable identity” across re-renders so that React can determine when items are added, removed, or re-ordered. Ideally, keys should correspond to unique and stable identifiers coming from your data, such as post.id.
 If you choose not to assign an explicit key to list items then React will default to using indexes as keys.
   https://reactjs.org/docs/lists-and-keys.html#keys
