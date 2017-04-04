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