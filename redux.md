# Redux

### Predictable state container for javascript applications.


**Application state is something _totally_ different than component state!**

Collection of all data to describe the app. App state container.

React represents the views which translates the application data into something that can be displayed on the screen and user can interact with.

Centralize all the application data into single object.

**Redux = application level state.**

### Reducer - a function that returns the piece of application state.

**Containers - smart components that connect React with Redux**

## Use containers

1. import ```connect``` from react-redux. This is the glue between React and Redux. They are separate libraries. 
2. ```connect``` takes a function and a component and produces a container. The container is a component that is aware of the state that is contained by Redux.
3. ```mapStateToProps``` is a special key here. It takes **an application state** as an argument and it returns **an object**. 
4. Object that is returned will be available to our component as ```this.props```.

### Reducer

1. Reducer is a function that returns an object or a list o objects. 
2. ```rootReducer``` combines all reducers using ```combineReducers``` function. Single objects returned from reducers are represented as **keys** in a **global state object** of our application.


## Action and action creators
1. User performs an action ie. click on 2nd book from the list
2. _Action creator_ returns an action
3. Action is automatically sent to all reducers
4. _Action Reducers_ can perform a change of its state depending on action type
5. All reducers process the action and return new state
6. If state chas been changed, rerender involved components


template of Action reducer:
```javascript
export function actionCreator(element) {
    
    return {
        type: 'TYPE_OF_ACTION',
        payload: element //optional field
    }
}
```

State argument is not application state, only the state this reducer is responsible for.

state = null means setting **initial state** of reducer to null not to be ```undefinied```
```javascript
export default function(state = null, action) {
  switch(action.type) {
    case 'ACTION_NAME':
      return action.payload
  }
  // if action type not appiled to this reducer return previous state without change
  return state;

}
```


------
## Rule of thumb

If you ever passing a callback around as a function and the callback has reference to this, **you need to bind it to the context**.


## axios

Library for making AJAX requests from the browser.



# Redux - connecting with container

Do not export container by default - use `connect` instead!

```javascript
function mapStateToProps(state) {
  // Whatever is returned will show up as props
  // inside of BookList
  return {
    books: state.books
  };
}

// With ES6 syntax
function mapStateToProps({ weather }) {
  return { weather }
}

// Anything returned from this  function will end up as props
// on te BookList container
function mapDispatchToProps(dispatch) {
  // Whenever selectBook is called, the result should be passed to
  // to all of our reducers
  return bindActionCreators({ selectBook: selectBook}, dispatch)
}


// Promote BookList from a component to a container - it needs to know
// about this new dispatch method, selectBook. Make it available
// as a prop.
export default connect(mapStateToProps, mapDispatchToProps)(BookList);
```

## refs

```javascript
<div ref="map" />
```
can be accessed in the code by `this.refs.map`


## redux middleware

`redux-promise` allows to wait until request (promise) is finished before forwarding it to appropriate reducer.
