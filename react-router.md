# React-router

## History

Tiny JavaScript extra package that manages urls of the web browser.
- It watches URLs for changes
- It has ability to update it over time

## React-Router

Takes a new URL from history and updates react components.

### Types of history tracking
1. browserHistory - analyze the whole URL
2. hashHistory - analyze URL after `#` sign
3. memoryHistory - don't use URLs at all


### Example 
```javascript
import React from 'react';
import { Route, IndexRoute } from 'react-router';

import App from './components/app';

<Route path="/" component={ App }/>
```
google.com/  ⇒  renders App

### Nested route

When we have nested routes (here greeting inside the app)
```javascript
<Route path="/" component={ App }>
    <Route path="greet" component={Greeting}/>
  </Route>
```
child component (Greeting) is passed to parent component (App) as `this.props.children`


## Index route

Index route is used when no child matches the URL.

```javascript
  <Route path="/" component={App}>
    <IndexRoute component={PostsIndex}/>
    <Route path="greet" component={Greeting} />
  </Route>
```

## Get request using axios


1. In `src\index.js` 
```javascript
import promise from 'redux-promise'

const createStoreWithMiddleware = applyMiddleware(promise)(createStore);
```

2. In `actions\index.js`
```javascript
import axios from 'axios'

export const FETCH_POSTS = 'FETCH_POSTS'

const ROOT_URL = 'http://reduxblog.herokuapp.com/api'
const API_KEY = '?key=yqbk'

export function fetchPosts() {
  const request = axios.get(`${ROOT_URL}/posts${API_KEY}`)
  return {
    type: FETCH_POSTS,
    payload: request
  }
}
```

## React lifecycle methods

`componentWillMount` is lifecycle method that is used whenever our component is about to be created for the**first time**.

```javascript
  componentWillMount() {
    console.log('test')
  }
```

## Link component

Links are React components that behave as a real links.

```javascript
import { Link } from 'react-router'
```

```javascript
render() {
  return (
      <div>
        <div className="text-xs-right">
          <Link to="/posts/new" className="btn btn-primary">
            Add a Post
          </Link>
        </div>
        List of blog posts.
      </div>
    )
  }
```


## Redux-Form

Package for managing form state in Redux.


```javascript
import { reducer as formReducer } from 'redux-form'

const rootReducer = combineReducers({
  form: formReducer
});
```

```javascript
import React, { Component } from 'react'
import { reduxForm } from 'redux-form'

class PostsNew extends Component {
  render() {
    return (
      <div>Create Form</div>
    )
  }
}

export default reduxForm({
  form: 'PostsNewForm',
  fields: ['title', 'categories', 'content']
})(PostsNew)
```

`{...object}` decompose given object into separate keys and values. Example:
```javasript
input type="text" className="form-control" {...title}/>
```

## reduxForm and difference

`connect`: 
- first argument is `mapStateToProps`, 
- 2nd is `mapDispatchToProps`

`reduxForm`: 
- 1st is form config, 
- 2nd is `mapStateTopProps`, 
- 3rd is `mapDispatchToProps`

## Form validation

1. Create `validate` fucntion:

```javascript
function validate(values) {
  const errors = {}

  if (!values.title) {
    // saved under title.error in the form
    errors.title = 'Enter a username'
  }

  return errors
}
```

2. Bind `validate` function with form:

```javasript
export default reduxForm({
  form: 'PostsNewForm',
  fields: ['title', 'categories', 'content'],
  validate
}, null, { createPost } )(PostsNew)
```

3. Use in the form:

```javasript
        <div className="form-group">
          <label>Title</label>
          <input type="text" className="form-control" {...title}/>
          <div className="text-help">
            {title.touched ? title.error : ''}
          </div>
        </div>
```

4. Add bootstrap styling to form:

```javascript
        <div className={`form-group ${title.touched && title.invalid ? 'has-danger' : '' }`}>
```
