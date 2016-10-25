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

Some other Flux implementations create different stores to represent different parts of the application. In Redux, the state of the entire application is represented by a single JavaScript Object. 

1. Talk about how the store in redux is a single state tree. 
2. Discuss that the store is a plain old JavaScript Object. 


3. Build out a basic `store` object with a `getState` method. 
4. Add the `dispatch` method. 
5. Add `subscribe` and apply the listeners.

## Resources

* [Redux MOtivation](http://redux.js.org/docs/introduction/Motivation.html)

<a href='https://learn.co/lessons/react-redux-intro-to-stores' data-visibility='hidden'>View this lesson on Learn.co</a>
