---
layout: post
title:  "React Notes: Revisisiting Key React JS Concepts"
categories: React Notes
---

I have learnt React briefly a couple of months ago. It's a good idea to reinforce the fundamentals by revisiting some of the key concepts of this library before diving in deeper.  
Somehow, learning `python` for the pass few months makes me more confident and easier to understand the concepts, syntax as well as the logic.  
Gratitudes to Cem Eygi for brilliant posts so I can understand the concept and mechanism of React JS.

## [Introduction to React JS](https://www.codingdocs.com/introduction-to-react-js/)
* React is a library not a framework
    * frameworks are complete packages, less flexible
    * projects does not depend on libraries

* DOM ([Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction))
    * document: page itself
    * objects: HTML tags
    * model: a tree structure

* React's Virtual DOM:
    * is a copy of the original DOOM
    * only changes parts of the page where changes are made --> much faster
    * instead of traditionally rendering whole page when every single change was made
    * >React DOM compares the element and its children to the previous one, and only applies the DOM updates necessary to bring the DOM to the desired state - [official doc](https://reactjs.org/docs/rendering-elements.html)
    * an example of rendering command: `ReactDOM.render(element, document.getElementById('root));`

* JSX (JavaScript XML) - a syntax extension to JavaScript:
    * 'Tis not JS nor HTML `const element = <h1>Hello!</h1>;`
    * is used to write HTML in JavaScript
    * will be translated by **`Babel`** to normal JavaScript

    ### some rules:
    * 'class' => 'className'
    * 'tabindex' => 'tabIndex'
    * only return a **SINGLE** HTML tag

* Installation:
    * install `Node.js`, [here](https://nodejs.org/en/): 
        >an asynchronous event-driven JavaScript runtime, Node.js is designed to build scalable network applications... [about Node.js](https://nodejs.org/en/about/)
    * `$ npx create-react-app my-app` to create your app
    * `$ cd my-app` go into the project folder
    * `$ npm start` to start serving locally

## [Functional and Class Components](https://www.codingdocs.com/react-js-understanding-functional-class-components/)
Components are reusable parts of the code. You can reuse the same code to generate multiple parts of the website with the same charactoristics for example. It's a bit like CBV in Django, or class in Python. Except in the world of React, the whole website is generated by numerous components. That's probably why it can rerender only parts of the DOM instead of rerendering the whole page causing bad UX.

Basically, you don't have to use Class Components to handle complex logic now. After the introduction of [***`React Hooks`***](https://reactjs.org/docs/hooks-overview.html), functional components can do complex state handling as well. However, it's not mandatory to change old Class compo to func compo. And the Class components will be further supported as well.

The mechanism in React is not terribly difficult. `EveryComponent`(capitalized camelCasely named) is defined/lives in their own file and has their own css file, returns/renders an HTML element in JSX syntax. When you need to use them, import them and call them in the **root file**(`app.js`). And the components are called in HTML tags: `<EveryComponent />`. And they HAVE TO be closed.

### Two equivalent components in function and class
```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### Note:
>Note: Always start component names with a capital letter.  
>React treats components starting with lowercase letters as DOM tags. For example, `<div />` represents an HTML div tag, but <Welcome /> represents a component and requires `Welcome` to be in scope.  
>To learn more about the reasoning behind this convention, please read [JSX In Depth](https://reactjs.org/docs/jsx-in-depth.html#user-defined-components-must-be-capitalized).


## [props, i.e. prpperties](https://www.codingdocs.com/what-is-props-and-how-to-use-it-in-react/)
FACTS:
* props are objects
* props are immutable
* props can ONLY be passed from a parent to a child: a _uni-directional flow_
* props are passed in like this `<ChildCompo text={"a string"} />`

METAPHORS:
* props are like `dict` objects in python, if they are passed in like this `<ChildCompo text={"a string"} />` - a key/value pair, if you `console.log(props)` you'll get `Object { text: "a string"}`
* it's like `context` in django, only `text` doesn't have to be in quotes, it's passed in `html templates` to render, in React world, it's the child component to render itself with the data received, i.e. the props
* it's just like the `context` being accessed in `templates`: you can access the value with `dot notation` in _interpolation_ `{}`: `{ props.text } `, just like django templates in `{{ post.content }}`

THOUGHTS:  
I remember reading more than one post recommending to stick with a language and to code in projects if you want to learn it fast. I think the reason for that is, for a beginner, the only way to truly enter the programming world is to develope a group of nerves which are tuned to respond and process the specific logic which the programmer and programming languages share for problem solving. And you will discover the similarities amongst the different languages and frameworks. Once you get a hang of it, it does get easier so they say. Fingers crossed.

## [state](https://www.codingdocs.com/react-js-understanding-state/)
FACTS:
* a state is for a component ONLY (private), it can NOT be passed to others, however, props CAN
* state lives/is defined in `constructor()` method (if it's a class component):
    ```js
    constructor() {
        this.state = {
            id: 1,
            name: "test"
        };
    }
    ```
    * and later can be accessed `{this.state.id}` or `{this.state.name}`
    * a `constructor()` is like `__init__()` method in python class, which is to initiate the class based object
* state can be changed unlike props, but it can only be changed using `setState()` method and never be reasigned with `=`
    ```js
    this.setState({
        name: "testing state"
    });
    ```
* state should not be overly used for a better performance


## Why `setState()`
Because it's a method to inform the `React VirtualDOM` that a part of the page has been changed. Rerender that part of the page at once. Without it, that part will never change.
>React DOM compares the element and its children to the previous one, and only applies the DOM updates necessary to bring the DOM to the desired state.

## [Diffs between props and state](https://www.freecodecamp.org/news/react-js-for-beginners-props-state-explained/)
* props is passed from parent to child, state is private, meaning can not be accessed by anyone but the component in which it is defined
* props can not be changed, state is all for dynamic rendering
* props can not be changed, state can only be changed with `setState()` method
* props is for passing data from parent to child, state is for managing data privately 

### a good blog to follow: [codingdocs.com](https://www.codingdocs.com/)
### Cem Eygi's Youtube Channel: [Cem Eygi Media](https://www.youtube.com/channel/UC1EgYPCvKCXFn8HlpoJwY3Q?view_as=subscriber) to learn more about CSS, React JS for beginner

---