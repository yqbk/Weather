# Redux Thunk

Thunk middleware for Redux.
Wait until request is completed and **afterwards** spread action to reducers.

```javasript
export function fetchUsers() {
    const request = axios.get(...)
    
    return (dispatch) => {
        request.then( ({data}) => {
            dispatch( { 
                type: 'FETCH_PROFILES',
                payload: data
            })
        }
    }
}
```