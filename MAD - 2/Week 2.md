# Lecture 1: Introduction to JavaScript Collections

## Key Takeaways

- **JavaScript Collections:** This allows us to group different types of objects together including arrays, objects, maps and sets.
- **Mixed Data Types:** JavaScript arrays can contain mixed data types, making then similar to Python lists.
- **Array Operations:** Common operations of arrays
	- Accessing individual elements.
	- Finding the length of the array.
	- Iterating through it's elements.
- **Iteration and Iterables:** JavaScript offers iterable objects like maps, sets, weak maps and also DOM tree. These allows us to work with collections of data and iterate through their elements.
- **Functional Programming:** JavaScript allows functional programming concepts, including passing function as arguments.
- **Destructuring:** This allows us to split arrays into multiple values, useful for named arguments.

```
// Example 1: Destructuring an array
const numbers = [1, 2, 3];
const [a, b, c] = numbers;

console.log(a); // Output: 1
console.log(b); // Output: 2
console.log(c); // Output: 3
```

- **Generators:** Generators in JS yield values and enable cooperative concurrency. We will be reading more about them in concepts like parallelism. 
- **Managing Arrays:** We can manage JS arrays by assigning `null` to clear their contents. Additionally, unlike python we can directly set the length of an array and for the extra indices JS will assign them `null` values.

# Lecture 2: Basic Calculator