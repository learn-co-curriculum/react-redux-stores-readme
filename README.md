# Intro To Stores

## Objectives

1. Use stores as part of a Javascript application
2. Explain how to get the state of the store. 
3. Write a `createStore` function to return a store object. 

## Overview

Take a second and think about Twitter. What seems like a simple interface is actually a complex collection of application states. What list of posts should be displayed? Have they been liked? How about starred? How many other users have Retweeted them, or replied? Managing all of these different states is extremely complicated. In this lesson, we'll learn about how Redux makes our lives easier by standardizing how we can manage all of these different pieces of state. 

## Enter the Redux

We've seen how the Flux architecture attempts to deal with all of these state changes. Just like Ruby on Rails is an implementation of the Model-View-Controller architecture, there are many different libraries that implement the Flux architecture. One of the most popular is Redux. Here's Redux creator Dan Abramov discussing the creation of Redux in the documentation: 

> I wrote Redux while working on my React Europe talk called “Hot Reloading with Time Travel”. My goal 	was to create a state management library with minimal API but completely predictable behavior, so it 	is possible to implement logging, hot reloading, time travel, universal apps, record and replay, 	without any buy-in from the developer.

What does that mean? He's discussing state management with predictable behavior. We should have one place to store the state of our application. Any time the state is updated, any view that cares should update accordingly. Let's take a look at how we can build this out ourselves, the Redux way. 

## Go to the Store

Some other Flux implementations create different stores to represent different parts of the application. In Redux, the state of the entire application is represented by a single JavaScript Object. Any piece of state that we need to keep track of, such a list of tweets or the current user, will be a piece of state in this tree. Whether it's a simple application, like a counter, or a really complex application, all of the state that we need to maintain will be in the same object.

Let's imagine a simple counter application. To begin, we'll have one piece of state, our `count`. Let's write a function to create our store called `createStore`.

```javascript
function createStore(){
  let state;
  
  return {
    getState: () => { return state; }
  }
}

const store = createStore();
```

Right now, our store just has one method on it, `getState`, that returns the current state. Notice that there's no way for us to actually change the state. This brings us to the second principle of redux - the only way to change the state of your application is by dispatching actions. For now, the actions that we dispatch will be simple. We'll dispatch a plain old JavaScript object with a type property. Then, our dispatch method can update the state. 

```javascript
function createStore(){
  let state;
  
  const getState = () => { 
    return state; 
  };
  
  const dispatch = (action) => {
   switch(action.type) {
     case 'INCREMENT_COUNT':
      state++;
     case 'DECREMENT_COUNT':
      state--;
  };


  
  return {
    getState: getState,
    dispatch: dispatch
  }
}

const store = createStore();
```

The store has one final responsibility. Once the state changes, we need a way to be able to notify any view who cares to update. This process is called subscribing to the store. We'll create an array of listeners to call whenever an action is dispatched. In more complex React Applications, we'll use the subscribe method to tell our components that they should re-render when there are changes to the state. For this basic counter example, our listeners may simply re-render DOM elements using jQuery or vanilla JavaScript. 

```javascript
function createStore(){
  let state;
  let listeners;
  
  const subscribe = (listener) => {
    listeners.push(listener);
  };
  
  ...
  
  return {
    getState: getState,   
    dispatch: dispatch,
    subscribe: subscribe       
  }
}

const store = createStore();

store.subscribe(() => {
  document.getElementById('count').innerText = store.getState();
})
```

Here, we're assuming we have an element with an id of `count`. We simply update the text of the count element each time an action is dispatched. We just need to call each listener after an action is dispatched.

```javascript
function createStore(){
  let state;
  let listeners = [];
  
  ...
  
  const dispatch = (action) => {
   switch(action.type) {
     case 'INCREMENT_COUNT':
      state++;
     case 'DECREMENT_COUNT':
      state--;
   }
   
   listeners.forEach( listener => listener(); ) 
  };

  ...
  
  return {
    getState: getState,
    dispatch: dispatch,
    subscribe: subscribe
  }
}

const store = createStore();
store.subscribe(() => {
  document.getElementById('count').innerText = store.getState();
})
```

## Conclusion

This is a simple example with only one piece of state, but this flow will be the same for any Redux application. First, we'll create a store to hold the state of our application. We'll subscribe any views that should care about state changes to the store. When we want to update our state, we'll dispatch an action. This process will automatically call each of our listeners and cause our views to re-render. 
 


## Resources

* [Redux Motivation](http://redux.js.org/docs/introduction/Motivation.html)
* [Dan Abramov on Egghead](https://egghead.io/lessons/javascript-redux-implementing-store-from-scratch)

<a href='https://learn.co/lessons/react-redux-intro-to-stores' data-visibility='hidden'>View this lesson on Learn.co</a>

<p class='util--hide'>View <a href='https://learn.co/lessons/react-redux-stores-readme'>Stores Readme</a> on Learn.co and start learning to code for free.</p>
