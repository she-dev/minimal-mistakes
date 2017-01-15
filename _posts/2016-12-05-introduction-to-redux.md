---
title: Introduction to Redux
excerpt: Quick introduction to Redux - a predictable state container for JavaScript apps.
modified: 2017-01-14
header:
tags:
---

What is Redux? From its [website](http://redux.js.org/):

> Redux is a predictable state container for JS apps. It helps you
> write applications that behave consistently, run in different
> environments (client, server, and native), and are easy to test.

That means we can use Redux to manage our React Native application's state!
But why would we use that? After all, we can control our state with our different components' states.
Well, using Redux we remove responsibility to manage the state from our components and manage the app state as a whole. Components don’t need to know how states change, they just know they need to dispatch an action.
Redux scales well. That's great for adding complexity to your application without adding complexity to your code because of the way Redux behaves, changing state in a predictable manner. 

#### How it works

Redux has a concept of *immutable state*. The only way to change the state is by dispatching an action. *Actions* are objects and the only requirement is that they have a *type* property with a value different of undefined.

The function that receives the actions is called *reducer*. It decides how to modify the state of the app depending on the type of action received. Then it produces a new object with the new state. Remember the state object is never modified, we always have to return a new object when the state is changed.

In Redux the *store* holds our application state, lets us dispatch actions to modify the state and it's the place where the reducer (or reducers) that will tell how the state will be updated have to be specified.

#### Redux and React

Here's an example of how to use Redux with our React Native apps. In this app each piece of content is represented by a library. It works by sending the id of the library the user clicked. This id is received and the row with the id of the correspondent content is expanded.
The full code of this app is available on [Github](https://github.com/she-dev/TechStack).

![TechStack app demo](http://i.imgur.com/kF4f96T.gif)

##### Use of store and provider

~~~javascript
const App = () => {
	return (
		<Provider store={createStore(reducers)}>
			<View>
				<LibraryList />
			</View>
		</Provider>
	);
};
~~~

Provider comes from [react-redux](https://github.com/reactjs/react-redux) library to integrate React and Redux.

##### Action
~~~javascript
export const selectLibrary = (libraryId) => {
  return {
    type: 'select_library',
    payload: libraryId
  };
};
~~~

##### Calling the action
~~~javascript
render() {
  return (
    <TouchableWithoutFeedback
      onPress={() => this.props.selectLibrary(id)}
    />  
  );
}
~~~

selectLibrary action is available at this.props because the actions are connected via *mapStateToProps*, which is subject for another post.

##### Reducer
~~~javascript
export default (state = null, action) => {
  switch (action.type) {
    case 'select_library':
      return action.payload;
    default:
      return state;
  }
};
~~~
There's only one action and its type is *select_library*. If a different *action.type* is received the reducer will return the current state of the app as default.

So, what did you think of Redux? It may sound complicated with all these new words but it makes life a lot simpler when your app grows in complexity. Let me know your experience with it if you decide to give Redux a try.
