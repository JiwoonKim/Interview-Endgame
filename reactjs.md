## :star: React Interview Questions & Answers

| No. | Questions |
|:---:|:---|
| :dart:  | __Core React__ |
| 1 | What is React? |
| 2 | What are the major features of React? |
| :rocket:  | __Optimizations__ |
| 1 | What is the VirtualDOM and how does it work? |


## :dart: Core React

1. ### What is React?

   React is an __open-source frontend JavaScript library__ used for building user interfaces especially for single page applications. 

2. ### What are the major features of React?

   The major features of React are:

   - It uses __VirtualDOM__ instead RealDOM considering that RealDOM manipulations are expensive.
   - Follows __Unidirectional data flow__ or data binding.
   - Uses __reusable/composable UI components__ to develop the view.
   
3. ### What is JSX and why is it used?

   JSX is a XML-like __syntax extension to JavaScript__ (acronym for _JavaScript XML_). Basically it just provides syntactic sugar to describe what the UI should look like using a HTML-like template syntax combined with the power of JavaScript.
   
   JSX gets compiled to `React.createElement()` calls which return plain JavaScript objects called React elements.
   
   While React does not require using JSX, it is widely used as a visual aid when working with UI inside JavaScript code. It also allows React to show more useful error and warning messages.

4. ### What is a React element?

   A React element is a __plain object__ _describing what you want to see on the screen_ (i.e. a component instance or DOM node and its desired properties). It contains only information about the component type (for example, a Button), its properties (for example, its color), and any child elements inside it.
   
   
   ```js
   const element = <h1>Hello, world</h1>;
   ```
   
   Elements were introduced in need of solving the problem of traditional object-oriented UI programming (working with component classes and instances). In this traditional UI model, it was up to the developer to take care of creating and destroying child component instances, and manually keep them up to date with any new information. Since the parents needed direct access to the children component instances, it also made it hard to decouple them in the future.

   Elements solve these problems since they are __just descriptions and not the actual instances__. They don’t refer to anything on the screen when you create them. You can create them and throw them away, and it won’t matter much. They are easy to traverse, don’t need to be parsed. Since they are just objects, they are __much lighter than the actual DOM elements__, making them cheap to create compared to browser DOM elements.

   It’s just an __immutable description object__ with two fields: type: (string | ReactClass) and props: Object1. 

React DOM takes care of updating the DOM to match the React elements.

   Typically, elements are not used directly, but get returned from components.
   
   - https://reactjs.org/blog/2015/12/18/react-components-elements-and-instances.html
   

## :rocket: Optimizations

1. ### What is the VirtualDOM and how does it work?
