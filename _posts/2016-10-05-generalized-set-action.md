---
title: Generalized Set Action for Redux Reducer
published: true
---
Redux is a popular framework for writing React app. After using it for a while, I noticed the code I wrote contains a lot of boilerplates, especially when it comes to reducer. This issue can be mitigated by using Lodash. This article shows how to use Lodash to write concise and flexible reducer.

<!-- more -->

When I was writing a redux reducer for a user profile form. The code I wrote was:

```javascript
switch (action.type) {
  case 'SET_FIRST_NAME':
    return {
      ...state,
      firstName: action.value,
    }
  case 'SET_LAST_NAME':
    return {
      ...state,
      lastName: action.value,
    }
  case 'SET_EMAIL':
    return {
      ...state,
      email: action.value,
    }
  case 'SET_PHONE_NUMBER':
    return {
      ...state,
      phoneNumber: action.value,
    }
    // ...
}
```

I realized some code in the switch block is repeating itself.

So I come up with another method to reduce the repeated code. This method require Lodash or a similar equivalent library.

```javascript
switch (action.type) {
  case 'SET': {
    const newState = _.clone(state);
    return _.set(newState, action.path, action.value);
  }
}
```

The key to implement this approach is the set function provided by lodash

```javascript
_.set = (object, path, value) => {/* ... */}

var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.set(object, 'a[0].b.c', 4);
console.log(object.a[0].b.c);
// => 4

_.set(object, ['x', '0', 'y', 'z'], 5);
console.log(object.x[0].y.z);
```

Now I can do the same thing with my new action.

```javascript
store.dispatch({
  type: 'SET',
  path: 'firstName', // or 'lastName', 'email', 'address.province'
  value,
})
```

It's worth to point out that other Lodash functions can also be exploited to combine with redux reducer.
