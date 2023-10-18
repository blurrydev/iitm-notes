# Live Lecture

## Declarative Rendering: 
1. Reactivity: 
	1. Automatically updating the interface based on the data provided.
	2. Focuses on *What needs to be changed* rather than *How to change it*.
	3. The opposite of Declarative is Imperative where you need to tell each and every detail about how to do a job.
2. User Interaction:
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
		  4. `v-for="(value, name, index) in obj"`