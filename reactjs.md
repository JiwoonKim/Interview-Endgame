## :star: React Interview Questions & Answers

| No. | Questions |
|:---:|:---|
| :dart:  | __Core React__ |
| 1 | What is React? |
| 2 | What are the major features of React? |
| 3 | What is JSX? |
| 4 | What is a React element? |
| 5 | What is a component? |
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
   
3. ### What is JSX?

   JSX is a XML-like __syntax extension to JavaScript__ (acronym for _JavaScript XML_). Basically it just provides syntactic sugar to describe what the UI should look like using a HTML-like template syntax combined with the power of JavaScript.
   
   While React does not require using JSX, it is widely __used as a visual aid when working with UI inside JavaScript code__. It also allows React to show more useful error and warning messages.
   
   > + JSX gets compiled to `React.createElement()` calls which return plain JavaScript objects called React elements.

4. ### What is a React element?

   A React element is a __plain object describing what you want to see on the screen__ (i.e. a component instance or DOM node and its desired properties). It contains only information about the component type (for example, a Button), its properties (for example, its color), and any child elements inside it.
   
   
   ```js
   // JSX syntax
   const element = <h1>Hello, world</h1>;
   
   // React element (described as object)
   {
      type: 'h1',
      props: {
        className: 'container',
        children: 'Hello, world',
      }
    }
   ```
   
   Elements were introduced in need of __solving the problem of traditional object-oriented UI programming__ (working with component classes and instances). In this traditional UI model, it was up to the developer to take care of _creating and destroying child component instances, and manually keep them up to date with any new information_. Since the parents needed direct access to the children component instances, it also made it _hard to decouple them in the future_.

   Elements solve these problems since they are __just descriptions and not the actual instances__. They don’t refer to anything on the screen when you create them. You can create them and throw them away, and it won’t matter much. They are easy to traverse, don’t need to be parsed. Since they are just objects, they are __much lighter than the actual DOM elements__, making them cheap to create compared to browser DOM elements.

   Typically, elements are not used directly, but get returned from components. And since an element's type can be a DOM node or a React component, __DOM and component elements are mixed and matched in a single element tree__. This composition structure ensures components are decoupled from each other.
   
   - https://reactjs.org/blog/2015/12/18/react-components-elements-and-instances.html
   
5. ### What is a component?

   

## :rocket: Optimizations

1. ### What is the VirtualDOM and how does it work?
