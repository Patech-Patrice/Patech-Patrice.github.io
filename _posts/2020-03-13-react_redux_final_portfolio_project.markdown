---
layout: post
title:      "React Redux Final Portfolio Project"
date:       2020-03-13 20:03:19 -0400
permalink:  react_redux_final_portfolio_project
---


The final project for  Flatiron School  was to build a simple app in React using create react app.  I decided to build a bucket list destination app to showcase some of the places that I would like to visit before I kick the bucket.   This project had quite a few moving parts, and in this blog, I will discuss Redux, one of the libraries I used to accomplish completing this task.  The requirements of the  project were to:

* Code in ES6 as much as possible.
* Use the create-react-app generator to start the project.
* Include one HTML page to render the react-redux application.
* Have 2 container components, 5 stateless components, and 3 routes.
* Application must make use of react-router and proper RESTful routing.
* Use Redux middleware to respond to and modify state change.
* Make use of async actions to send data to and receive data from the server.
* Must build a backend API using Rails which should handle data persistence.  
* Must use fetch within actions to GET and POST data from the API without the use of jQuery methods.
* Client-side app(React) should handle the display of data with minimal data manipulation.


**What is Redux?**

Redux is a predictable state container for JavaScript apps that makes managing the state(data that can change from time to time) of your application simpler.  This allows you to display data to your users as well as helps you manage how you respond to user actions.  However, redux is more than just state management,  with a major focus on the inner workings of the app itself.  The state of the app is determined by what is displayed on the user interface.

There are three factors of data needed in order to manage state in an app:

*  Changing data
*  Fetching and storing data
*  Assigning data to UI elements

Using redux does come with a few rules that developers must abide by, but these rules are worth it because they allow redux to power at its full potential.  


**Where to setup Redux?**

There are a few ways in which a store can be set-up.  The store can be created inside of the index.js file, or inside of a separate file called store.js and imported inside of the index.js file.  I chose to create my store inside of  index.js.  Below is an example of how to set up a store in React.


```
import React from 'react';
import ReactDOM from 'react-dom';
import {createStore, applyMiddleware, compose, combineReducers} from 'redux';
import  thunk  from 'redux-thunk';
import { Provider } from 'react-redux';
import destinationReducer from './reducers/destinationReducer.js';
import attractionReducer from './reducers/attractionReducer.js';
import commentReducer from './reducers/commentReducer.js';
import { BrowserRouter as Router } from 'react-router-dom';

import App from './App';

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;

const reducer = combineReducers({
    destination: destinationReducer,
    attraction: attractionReducer,
    comment: commentReducer
})
let store = createStore(reducer, composeEnhancers(applyMiddleware(thunk)))


ReactDOM.render(
<Provider store={store}>
 <Router>
  <App />
 </Router>
</Provider>
, 
document.getElementById('root'));

export default store;
```


Overall this project was challenging yet fun to create.  Learning the fundamentals of redux and state management has been valuable in teaching me the required knowledge needed in order for me to not only build web apps, but cross platform apps as well.  I plan to utilize what I have learned here, and apply it to a React Native app that I am currently working on.  I am grateful to Flatiron for this amazing journey, and look forward to applying what I have I learned everyday in the future upon graduation.


