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

# Lecture 2: JavaScript Collections - Iterations & Destructuring

## Loops

### for loop

- This is the same old traditional way of iterating through a iterable or collection for a said number of times.
- The `for` loop in python is very similar to this.

```js
for (let i = 0; i < array.length; i++) {
  // Access array[i] and perform operations
}
```

### `for of` loop

- The `for...of` loop is designed specifically for iterating over iterable objects like arrays, strings, and sets.
- It's similar to `for ... in` in python.

```js
for (const item of array) {
  // Access 'item' and perform operations
}
```

### `for in` loop

- The `for...in` loop iterates over the properties of an object (keys).
- It's suitable for objects and not recommended for arrays.
- It is similar to `for ... in obj.keys()`.

```js
for (const key in object) {
  // Access 'key' and object[key] and perform operations
}
```

### `forEach()` Method:

- The `forEach()` method is available on arrays and allows you to execute a function for each element in the array.

```js
array.forEach((item) => {
  // Access 'item' and perform operations
});
```

> - Regular indexing is used for direct access to elements in arrays.
	- **for...in** is used for iterating over object properties.
	- **for...of** is used for iterating over elements in iterable objects like arrays.
	- **forEach()** is a method for iterating through arrays with a function.

> - **of** also iterates over empty arrays which has undefined values.
> - **in** does not iterate over empty arrays and only shows array element which has values.

> - we can iterate over objects within {} using object.entries() normally using **in** or destruct it using [key, value] when using **of**
> - we can also iterate over object using object.values() normally using **of**.

### Spreading

- ...x will literally add all array elements as regular elements in the new array.
- Only using x will add the entire array as a single elements in the array

```javascript
let x = [1,2,3]
let y = [0, ...x, 4]
console.log(y)

//output
// [0,1,2,3,4]
```

```JavaScript
let x = [1,2,3]
let y = [0, x, 4]
console.log(y)

//output
// [0,[1,2,3],4]
```

## Arrays

### Array `find()` Method:

- Used for searching and retrieving the first element in an array that satisfies a provided testing function.

``` js
const numbers = [10, 20, 30, 40, 50];
const result = numbers.find((number) => number > 25);

console.log(result); // Output: 30 (the first element greater than 25)

```


### Array `filter()` Method:

- Used for creating a new array with all elements that pass a provided testing function.

```js
// Example array of objects representing books
const books = [
  { title: 'The Great Gatsby', author: 'F. Scott Fitzgerald', genre: 'Fiction' },
  { title: 'To Kill a Mockingbird', author: 'Harper Lee', genre: 'Fiction' },
  { title: '1984', author: 'George Orwell', genre: 'Dystopian' },
  { title: 'The Hobbit', author: 'J.R.R. Tolkien', genre: 'Fantasy' },
  { title: 'The Catcher in the Rye', author: 'J.D. Salinger', genre: 'Fiction' },
];

// Using filter to find all books in the 'Fiction' genre
const fictionBooks = books.filter((book) => book.genre === 'Fiction');

console.log(fictionBooks);
```

### Array `map()` Method

- Used for creating a new array by applying a function to each element in an existing array.
- Preserves the original array, as map() does not modify it.
- Can return different values based on conditions defined in the callback function.

```js
// Example: Mapping an array of numbers to their squares
const numbers = [1, 2, 3, 4, 5];
const squaredNumbers = numbers.map((number) => number * number);
// squaredNumbers now contains [1, 4, 9, 16, 25]
```

```js
// Example: Mapping an array of numbers to even/odd labels using a ternary operator
const numbers = [1, 2, 3, 4, 5];
const result = numbers.map((number => number % 2 === 0 ? `${number} is even` : `${number} is odd`));
// result now contains ["1 is odd", "2 is even", "3 is odd", "4 is even", "5 is odd"]
```


### Array `reduce()` Method:

- Used for reducing an array to a single value by applying a function to each element.
- The original array remains unchanged.

**Syntax**:

- `array.reduce(callback(accumulator, element), initialValue)`
- `callback`: Function to apply to each array element and the accumulator.
- `accumulator`: The accumulated result of the previous iterations.
- `element`: Current element being processed.
- `initialValue` (optional): The initial value of the accumulator.

```js
// Example: Summing an array of numbers using reduce
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((accumulator, number) => accumulator + number, 0);
// sum now contains 15 (the sum of the numbers)
```

### Array `sort()` Method:

- Used for sorting the elements of an array in place and returning the sorted array.
- Modifies the original array.

**Syntax**:

- `array.sort(compareFunction)`
- `compareFunction` (optional): A function that defines the sort order. If omitted, the elements are sorted as strings (*Lexical Sorting*).

```js
// Example: Sorting an array of numbers without a compare function
const numbers = [3, -1, 4, -9, 5, -2, 6, 1];
numbers.sort();
// numbers now contains [-1, -2, -9, 1, 3, 4, 5, 6]
```

```js
// Example: Sorting an array of numbers in ascending order
const numbers = [3, -1, 4, -9, 5, -2, 6, 1];
numbers.sort((a, b) => a - b);
// numbers now contains [-9, -2, -1, 1, 3, 4, 5, 6]
```


Certainly! Here are notes on object and array destructuring with appropriate examples:

### Object Destructuring:

- **Basic Syntax**:

  ```javascript
  const person = { name: 'John', age: 30 };
  const { name, age } = person;
  ```

  - Extracts `name` and `age` properties from the `person` object and assigns them to variables with the same names.
  - `name` will be `'John'`, and `age` will be `30`.

- **With Renaming**:

  ```javascript
  const student = { firstName: 'Alice', lastName: 'Johnson' };
  const { firstName: first, lastName: last } = student;
  ```

  - Renames the properties while destructuring.
  - `first` will be `'Alice'`, and `last` will be `'Johnson'`.

- **Default Values**:

  ```javascript
  const product = { name: 'Laptop', price: 1000 };
  const { name, stock = 10 } = product;
  ```

  - Provides a default value for `stock` in case it doesn't exist in `product`.
  - `name` will be `'Laptop'`, and `stock` will be `10`.

### Array Destructuring:

- **Basic Syntax**:

  ```javascript
  const colors = ['red', 'green', 'blue'];
  const [firstColor, secondColor] = colors;
  ```

  - Extracts the values at positions 0 and 1 from `colors`.
  - `firstColor` will be `'red'`, and `secondColor` will be `'green'`.

- **Ignoring Elements**:

  ```javascript
  const numbers = [1, 2, 3, 4, 5];
  const [first, , third] = numbers;
  ```

  - Ignores the second element in the array.
  - `first` will be `1`, and `third` will be `3`.

- **Rest Operator**:

  ```javascript
  const numbers = [1, 2, 3, 4, 5];
  const [first, ...rest] = numbers;
  ```

  - Uses the rest operator to capture all elements after the first one.
  - `first` will be `1`, and `rest` will be `[2, 3, 4, 5]`.

Destructuring simplifies the process of extracting values from objects and arrays, making your code more concise and readable. It is commonly used when working with API responses, function arguments, and various data structures in JavaScript.


# Modularity

- ES6 modules are the modern standard for managing asynchronous modules.
- Node is a command line interface for JavaScript.
- npm (Node Package Manager) is a versatile tool for managing JavaScript modules.
- **Modules** in JavaScript are organized libraries of modules and functions.

Certainly! Here are quick revision notes on JavaScript modularity using ES6 modules in bullet points:

### Exporting from a Module:

- Use the `export` keyword to export functions, variables, or objects.
- Functions and variables can be explicitly marked for export.

Example:
```javascript
// math.js
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}
```

### Importing into Another Module:

- Use the `import` statement to import functions, variables, or objects from another module.
- You can use imported items as if they were defined in the current module.

Example:
```javascript
// main.js
import { add, subtract } from './math.js';

const result1 = add(5, 3);
const result2 = subtract(10, 4);
```

### Default Exports:

- You can export a single value or function as the default export using `export default`.

Example:
```javascript
// utility.js
export default function greet(name) {
  return `Hello, ${name}!`;
}
```

- Import the default export without curly braces, using the name you choose.

Example:
```javascript
// main.js
import greet from './utility.js';

const greeting = greet('Alice');
```

Certainly! Objects are a fundamental data structure in JavaScript, allowing you to store and manipulate data in a structured way. Here are some key points about objects in JavaScript:

## Objects
### Creating Objects:

- Objects are collections of key-value pairs.
- You can create an object using object literals:

```javascript
const person = {
  name: 'John',
  age: 30,
  job: 'Engineer'
};
```

### Accessing Properties:

- You can access object properties using dot notation or bracket notation:

```javascript
const name = person.name; // Dot notation
const age = person['age']; // Bracket notation
```

### Adding and Modifying Properties:

- You can add new properties or modify existing ones:

```javascript
person.location = 'New York'; // Adding a property
person.age = 31; // Modifying a property
```

### Object Methods:

- Objects can contain functions, which are called methods:

```javascript
const car = {
  make: 'Toyota',
  model: 'Camry',
  start: function() {
    console.log('Engine started.');
  }
};
car.start(); // Calling the method
```

### Object Destructuring:

- You can easily extract values from objects using destructuring:

```javascript
const { name, age } = person;
```

### Object Keys and Values:

- You can get the keys and values of an object using `Object.keys()` and `Object.values()`:

```javascript
const keys = Object.keys(person);
const values = Object.values(person);
```

### Object Iteration:

- You can iterate over object properties using `for...in` or `Object.entries()`:

```javascript
for (const key in person) {
  console.log(`${key}: ${person[key]}`);
}

// Or with Object.entries()
for (const [key, value] of Object.entries(person)) {
  console.log(`${key}: ${value}`);
}
```


### JavaScript `call` Method (Simplified):

- The `call` method is like a helper that lets you use a function in different ways.
- It helps you change the context, or the special `this` value, for a function.
- If you don't use `call` correctly, you might get unexpected results like `NaN`.
- You can use `call` to pass arguments to a function one by one.
- Example: If you have a function `add` that needs a `this` value (like an object) and arguments, you can do it like this:

  ```javascript
  const result = add.call(obj, arg1, arg2);
  ```

- Setting the right `this` value with `call` is important to make sure your function works as expected.