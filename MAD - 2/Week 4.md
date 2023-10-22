# Live Lecture - Part 1

## Declarative Rendering: 
1. Reactivity: 
	1. Automatically updating the interface based on the data provided.
	2. Focuses on *What needs to be changed* rather than *How to change it*.
	3. The opposite of Declarative is Imperative where you need to tell each and every detail about how to do a job.
 
1. User Interaction:
	1. Servers are usually stateless so they don't really know the state incase the connection breaks, here client stores and maintains the state so that if there is a connection failure and we need to request something to the server then we need not start from the beginning.
	2. Vue - Directives
		1. v-bind (:) is one way binding where our data makes changes to the view.
		2. v-model is two way binding where the our data makes changes to the view and from view we can also make changes to our data model.
  
		> 	This allows human interaction from the view to make changes in the model.
  
		1. v-on (@) is used to bind a specific function to something. Example if we use v-on click then it says that anytime we click that button then it should trigger that function.
  
  3. Conditional Rendering
		1. `v-if="argument"` 
			1. If argument is True then it will literally change the DOM.
		2. `v-show="param"` 
			1. This doesn't really change the DOM but *hides* or *shows* the existing CSS parameters.
  4. Looping
	  1. Iterate over any JS iterable -> Array, Object, String etc.
	  2. Examples:
		  1. `v-for="item in items"` items in array.
		  2. `v-for="value in obj"`
		  3. `v-for="(value, name) in obj"` 
		  4. `v-for="(value, name, index) in obj"` index is numerical index.
5. Loop Keys
	1. Vue needs some way to keep track of what has been modified for complex updates.
	2. This is when Keys comes handy.
	3. This must be unique to each loop element.
	4. If two items have same keys then updating the item with the key will only update the relevant item.
	5. As a rule of thumb we should always provide keys wherever possible.

## ViewModel

### Model / View

- Model:
	- This is the `data` of the application which is usually stored in the server on database.
- View:
	- Displayed to end user (can also be non-human consumer like JSON).
Problem:
	- Sometimes we might need to store some temporary data which we don't necessarily need to store in the Model.
	- For example let's say we are asking user to re-enter their password while creating account. Now we need to store this re-entered password somewhere but not in the Model else it'll be redundant.

### ViewModel

- This is an additional `Pattern` which creates a model with additional data / derived data.
- Vue doesn't strictly associate with the MVVM pattern but 
- To solve the above problem we can use v-model to store the `confirmPassword` as a part of the ViewModel and it doesn't have to be stored in the `Data`.

``` html
<template>
  <div>
    <input v-model="user.password" type="password" placeholder="Password">
    <input v-model="confirmPassword" type="password" placeholder="Confirm Password">
    <button @click="registerUser">Register</button>
  </div>
</template>
```

```vue
<script>
export default {
  data() {
    return {
      user: {
        username: '',
        password: ''
      },
      confirmPassword: ''
    };
  },
  methods: {
    registerUser() {
      if (this.user.password === this.confirmPassword) {
        // Passwords match, proceed with registration
        // You can now use this.user.username and this.user.password to register the user.
      } else {
        // Passwords don't match, show an error message or take appropriate action.
      }
    }
  }
}
</script>
```

### MVC vs MVVM

- Our approach shouldn't be *either MVC or MVVM*.

#### Controller:
- Convey actions to model.
- Call appropriate view based on inputs and model.
#### ViewModel:
- Create framework for data binding.
- Can still use controllers to invoke actions.

## Computed Properties

- Computed properties are used in Vue.js to define data properties that depend on other data properties.
- These are cached and recalculated only when their dependencies change, optimizing performance.
- These are ideal for synchronous operations, for asynchronous operations we use methods or watchers.
- Computed `setter` are also possible.
- 

> - In synchronous operations, tasks are executed one after the other in a sequential manner.
> - In asynchronous operations, tasks are executed independently, and the program doesn't wait for a task to complete before moving on to the next one.

## Components

### Reusable

- We can use components to reuse our code into multiple places within our application.
- It reduces code duplication.
- Makes it easier to maintain consistency.
- Makes it more readable.

### Vue Component Structure

- **Properties:** These are passed down from parents to the child and we can customize each child instance.
- **Data:** Individual data of the child also the it's own watchers, computed properties.
- **Templates:** It tells the code how to render. We can also render functions.

### Templates

- Templates format is similar to Jinja syntax.
- It also has safety features 

### Slots

This allows us to pass content into a component from it's parent component. 


# Components in Vue Js


