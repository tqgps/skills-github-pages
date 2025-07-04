# JavaScript Tutorial: From Beginner to Advanced

## Table of Contents
1. [Introduction to JavaScript](#introduction)
2. [Setting Up Your Environment](#setup)
3. [Basic Syntax and Variables](#basics)
4. [Data Types](#data-types)
5. [Operators](#operators)
6. [Control Structures](#control-structures)
7. [Functions](#functions)
8. [Objects and Arrays](#objects-arrays)
9. [Advanced Functions](#advanced-functions)
10. [Asynchronous JavaScript](#async)
11. [DOM Manipulation](#dom)
12. [Error Handling](#error-handling)
13. [Modern JavaScript (ES6+)](#modern-js)
14. [Best Practices](#best-practices)
15. [Practice Exercises](#exercises)

---

## Introduction to JavaScript {#introduction}

JavaScript is a versatile, high-level programming language that's essential for web development. It runs in browsers, servers (Node.js), and many other environments.

### What You'll Learn
- Core JavaScript concepts and syntax
- How to manipulate web pages
- Asynchronous programming
- Modern JavaScript features
- Best coding practices

---

## Setting Up Your Environment {#setup}

### Option 1: Browser Console
1. Open any web browser
2. Press F12 or right-click → "Inspect"
3. Go to the "Console" tab
4. Start typing JavaScript!

### Option 2: Node.js (Recommended)
1. Install Node.js from [nodejs.org](https://nodejs.org/)
2. Open terminal/command prompt
3. Type `node` and press Enter
4. You're now in the Node.js REPL!

### Option 3: Online Editors
- [CodePen](https://codepen.io/)
- [JSFiddle](https://jsfiddle.net/)
- [Replit](https://replit.com/)

---

## Basic Syntax and Variables {#basics}

### Your First JavaScript Code
```javascript
// This is a comment
console.log("Hello, World!");

/* This is a 
   multi-line comment */
```

### Variables
JavaScript has three ways to declare variables:

```javascript
// var - function-scoped (avoid in modern JS)
var oldWay = "I'm old school";

// let - block-scoped, can be reassigned
let age = 25;
age = 26; // This works

// const - block-scoped, cannot be reassigned
const name = "Alice";
// name = "Bob"; // This would cause an error
```

### Variable Naming Rules
- Must start with a letter, underscore (_), or dollar sign ($)
- Can contain letters, numbers, underscores, and dollar signs
- Case-sensitive
- Cannot use reserved words (like `let`, `function`, `class`)

```javascript
// Good variable names
let userName = "john_doe";
let $element = document.getElementById("myId");
let _private = "secret";

// Bad variable names (will cause errors)
// let 123abc = "invalid";
// let let = "reserved word";
```

---

## Data Types {#data-types}

JavaScript has dynamic typing - variables can hold different types of data.

### Primitive Data Types

```javascript
// Number
let integer = 42;
let decimal = 3.14;
let scientific = 2.5e6; // 2,500,000

// String
let singleQuotes = 'Hello';
let doubleQuotes = "World";
let templateLiteral = `Hello ${singleQuotes}!`; // Template literals

// Boolean
let isTrue = true;
let isFalse = false;

// Undefined
let notDefined;
console.log(notDefined); // undefined

// Null
let empty = null;

// Symbol (ES6+)
let sym = Symbol('id');

// BigInt (ES2020+)
let bigNumber = 123456789012345678901234567890n;
```

### Type Checking
```javascript
let value = 42;
console.log(typeof value); // "number"

value = "Hello";
console.log(typeof value); // "string"

value = true;
console.log(typeof value); // "boolean"

value = null;
console.log(typeof value); // "object" (this is a known quirk!)

value = undefined;
console.log(typeof value); // "undefined"
```

### Type Conversion
```javascript
// String to Number
let str = "123";
let num1 = Number(str);        // 123
let num2 = parseInt(str);      // 123
let num3 = parseFloat("3.14"); // 3.14
let num4 = +str;              // 123

// Number to String
let num = 123;
let str1 = String(num);       // "123"
let str2 = num.toString();    // "123"
let str3 = num + "";          // "123"

// Boolean Conversion
let bool1 = Boolean(1);       // true
let bool2 = Boolean(0);       // false
let bool3 = Boolean("");      // false
let bool4 = Boolean("hello"); // true
```

---

## Operators {#operators}

### Arithmetic Operators
```javascript
let a = 10;
let b = 3;

console.log(a + b);  // 13 (addition)
console.log(a - b);  // 7  (subtraction)
console.log(a * b);  // 30 (multiplication)
console.log(a / b);  // 3.333... (division)
console.log(a % b);  // 1  (remainder/modulo)
console.log(a ** b); // 1000 (exponentiation)

// Increment and Decrement
let count = 5;
count++;    // count is now 6
count--;    // count is now 5
++count;    // count is now 6
--count;    // count is now 5
```

### Comparison Operators
```javascript
let x = 5;
let y = "5";

console.log(x == y);  // true (loose equality)
console.log(x === y); // false (strict equality)
console.log(x != y);  // false (loose inequality)
console.log(x !== y); // true (strict inequality)
console.log(x > 3);   // true
console.log(x < 3);   // false
console.log(x >= 5);  // true
console.log(x <= 5);  // true
```

### Logical Operators
```javascript
let a = true;
let b = false;

console.log(a && b); // false (AND)
console.log(a || b); // true (OR)
console.log(!a);     // false (NOT)

// Short-circuit evaluation
let result = a && "Hello"; // "Hello"
let result2 = b || "Default"; // "Default"
```

### Assignment Operators
```javascript
let x = 10;

x += 5;  // x = x + 5  (15)
x -= 3;  // x = x - 3  (12)
x *= 2;  // x = x * 2  (24)
x /= 4;  // x = x / 4  (6)
x %= 4;  // x = x % 4  (2)
```

---

## Control Structures {#control-structures}

### Conditional Statements

#### if/else
```javascript
let age = 18;

if (age >= 18) {
    console.log("You are an adult");
} else if (age >= 13) {
    console.log("You are a teenager");
} else {
    console.log("You are a child");
}

// Ternary operator (shorthand)
let status = age >= 18 ? "adult" : "minor";
console.log(status);
```

#### switch
```javascript
let day = "Monday";

switch (day) {
    case "Monday":
        console.log("Start of the work week");
        break;
    case "Tuesday":
    case "Wednesday":
    case "Thursday":
        console.log("Midweek");
        break;
    case "Friday":
        console.log("TGIF!");
        break;
    case "Saturday":
    case "Sunday":
        console.log("Weekend!");
        break;
    default:
        console.log("Invalid day");
}
```

### Loops

#### for loop
```javascript
// Basic for loop
for (let i = 0; i < 5; i++) {
    console.log("Count: " + i);
}

// for...of loop (for arrays)
let fruits = ["apple", "banana", "orange"];
for (let fruit of fruits) {
    console.log(fruit);
}

// for...in loop (for objects)
let person = { name: "John", age: 30, city: "New York" };
for (let key in person) {
    console.log(key + ": " + person[key]);
}
```

#### while loop
```javascript
let count = 0;
while (count < 3) {
    console.log("Count: " + count);
    count++;
}

// do...while loop
let num = 0;
do {
    console.log("Number: " + num);
    num++;
} while (num < 3);
```

#### Loop Control
```javascript
// break - exits the loop
for (let i = 0; i < 10; i++) {
    if (i === 5) {
        break; // Stop the loop when i is 5
    }
    console.log(i);
}

// continue - skips to next iteration
for (let i = 0; i < 5; i++) {
    if (i === 2) {
        continue; // Skip when i is 2
    }
    console.log(i);
}
```

---

## Functions {#functions}

### Function Declaration
```javascript
function greet(name) {
    return "Hello, " + name + "!";
}

let message = greet("Alice");
console.log(message); // "Hello, Alice!"
```

### Function Expression
```javascript
let greet = function(name) {
    return "Hello, " + name + "!";
};

console.log(greet("Bob")); // "Hello, Bob!"
```

### Arrow Functions (ES6+)
```javascript
// Basic arrow function
let greet = (name) => {
    return "Hello, " + name + "!";
};

// Simplified arrow function
let greet2 = name => "Hello, " + name + "!";

// Multiple parameters
let add = (a, b) => a + b;

// No parameters
let sayHello = () => "Hello!";

console.log(add(5, 3)); // 8
console.log(sayHello()); // "Hello!"
```

### Default Parameters
```javascript
function greet(name = "World") {
    return "Hello, " + name + "!";
}

console.log(greet());        // "Hello, World!"
console.log(greet("Alice")); // "Hello, Alice!"
```

### Rest Parameters
```javascript
function sum(...numbers) {
    let total = 0;
    for (let number of numbers) {
        total += number;
    }
    return total;
}

console.log(sum(1, 2, 3, 4, 5)); // 15
```

### Function Scope
```javascript
let globalVar = "I'm global";

function example() {
    let localVar = "I'm local";
    console.log(globalVar); // Can access global
    console.log(localVar);  // Can access local
}

example();
// console.log(localVar); // Error: localVar is not defined
```

---

## Objects and Arrays {#objects-arrays}

### Objects
```javascript
// Object literal
let person = {
    name: "John",
    age: 30,
    city: "New York",
    greet: function() {
        return "Hello, I'm " + this.name;
    }
};

// Accessing properties
console.log(person.name);        // "John"
console.log(person["age"]);      // 30
console.log(person.greet());     // "Hello, I'm John"

// Adding properties
person.job = "Developer";
person["salary"] = 75000;

// Deleting properties
delete person.city;

// Object methods
let keys = Object.keys(person);
let values = Object.values(person);
let entries = Object.entries(person);

console.log(keys);    // ["name", "age", "greet", "job", "salary"]
console.log(values);  // ["John", 30, function, "Developer", 75000]
```

### Arrays
```javascript
// Array literal
let fruits = ["apple", "banana", "orange"];

// Array constructor
let numbers = new Array(1, 2, 3, 4, 5);

// Accessing elements
console.log(fruits[0]);    // "apple"
console.log(fruits.length); // 3

// Adding elements
fruits.push("grape");      // Add to end
fruits.unshift("mango");   // Add to beginning

// Removing elements
let lastFruit = fruits.pop();      // Remove from end
let firstFruit = fruits.shift();   // Remove from beginning

// Finding elements
let index = fruits.indexOf("banana");
let hasApple = fruits.includes("apple");

// Array methods
let upperFruits = fruits.map(fruit => fruit.toUpperCase());
let longFruits = fruits.filter(fruit => fruit.length > 5);
let totalLength = fruits.reduce((sum, fruit) => sum + fruit.length, 0);

console.log(upperFruits);  // ["APPLE", "BANANA", "ORANGE"]
console.log(longFruits);   // ["banana", "orange"]
console.log(totalLength);  // 17
```

### Nested Objects and Arrays
```javascript
let company = {
    name: "Tech Corp",
    employees: [
        { name: "Alice", position: "Developer" },
        { name: "Bob", position: "Designer" },
        { name: "Charlie", position: "Manager" }
    ],
    headquarters: {
        address: "123 Main St",
        city: "San Francisco",
        country: "USA"
    }
};

console.log(company.employees[0].name); // "Alice"
console.log(company.headquarters.city); // "San Francisco"
```

---

## Advanced Functions {#advanced-functions}

### Higher-Order Functions
```javascript
// Function that takes another function as parameter
function processArray(arr, callback) {
    let result = [];
    for (let item of arr) {
        result.push(callback(item));
    }
    return result;
}

let numbers = [1, 2, 3, 4, 5];
let doubled = processArray(numbers, x => x * 2);
console.log(doubled); // [2, 4, 6, 8, 10]
```

### Closures
```javascript
function outerFunction(x) {
    // This is the outer function's scope
    
    function innerFunction(y) {
        // This inner function has access to x
        return x + y;
    }
    
    return innerFunction;
}

let addFive = outerFunction(5);
console.log(addFive(3)); // 8

// Practical example: Counter
function createCounter() {
    let count = 0;
    
    return {
        increment: () => ++count,
        decrement: () => --count,
        getCount: () => count
    };
}

let counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.getCount());  // 2
```

### Callback Functions
```javascript
function fetchData(callback) {
    // Simulate async operation
    setTimeout(() => {
        let data = { name: "John", age: 30 };
        callback(data);
    }, 1000);
}

fetchData(function(data) {
    console.log("Received data:", data);
});
```

---

## Asynchronous JavaScript {#async}

### Promises
```javascript
// Creating a promise
let myPromise = new Promise((resolve, reject) => {
    let success = true;
    
    if (success) {
        resolve("Operation successful!");
    } else {
        reject("Operation failed!");
    }
});

// Using a promise
myPromise
    .then(result => console.log(result))
    .catch(error => console.error(error));

// Chaining promises
fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

### Async/Await
```javascript
// Async function
async function fetchUserData() {
    try {
        let response = await fetch('https://api.example.com/user');
        let userData = await response.json();
        return userData;
    } catch (error) {
        console.error('Error fetching user data:', error);
        throw error;
    }
}

// Using async function
async function displayUser() {
    try {
        let user = await fetchUserData();
        console.log('User:', user);
    } catch (error) {
        console.log('Could not display user');
    }
}
```

### setTimeout and setInterval
```javascript
// setTimeout - runs once after delay
setTimeout(() => {
    console.log("This runs after 2 seconds");
}, 2000);

// setInterval - runs repeatedly
let intervalId = setInterval(() => {
    console.log("This runs every 1 second");
}, 1000);

// Clear interval after 5 seconds
setTimeout(() => {
    clearInterval(intervalId);
    console.log("Interval cleared");
}, 5000);
```

---

## DOM Manipulation {#dom}

### Selecting Elements
```javascript
// By ID
let element = document.getElementById('myId');

// By class name
let elements = document.getElementsByClassName('myClass');

// By tag name
let paragraphs = document.getElementsByTagName('p');

// Query selector (CSS selectors)
let firstDiv = document.querySelector('div');
let allDivs = document.querySelectorAll('div');
let specificElement = document.querySelector('.myClass #myId');
```

### Modifying Elements
```javascript
let element = document.getElementById('myElement');

// Change content
element.textContent = 'New text content';
element.innerHTML = '<strong>New HTML content</strong>';

// Change attributes
element.setAttribute('class', 'newClass');
element.src = 'newImage.jpg';

// Change style
element.style.color = 'blue';
element.style.fontSize = '20px';
element.style.backgroundColor = 'yellow';

// Add/remove classes
element.classList.add('newClass');
element.classList.remove('oldClass');
element.classList.toggle('active');
```

### Creating and Removing Elements
```javascript
// Create new element
let newDiv = document.createElement('div');
newDiv.textContent = 'Hello, World!';
newDiv.classList.add('myClass');

// Add to DOM
document.body.appendChild(newDiv);

// Remove element
let elementToRemove = document.getElementById('removeMe');
elementToRemove.parentNode.removeChild(elementToRemove);
// Or in modern browsers:
// elementToRemove.remove();
```

### Event Handling
```javascript
// Add event listener
let button = document.getElementById('myButton');

button.addEventListener('click', function() {
    console.log('Button clicked!');
});

// Arrow function event handler
button.addEventListener('click', () => {
    console.log('Button clicked with arrow function!');
});

// Event object
button.addEventListener('click', function(event) {
    console.log('Event type:', event.type);
    console.log('Target element:', event.target);
    event.preventDefault(); // Prevent default behavior
});

// Common events
document.addEventListener('DOMContentLoaded', () => {
    console.log('DOM is ready!');
});

window.addEventListener('load', () => {
    console.log('Page fully loaded!');
});
```

---

## Error Handling {#error-handling}

### try/catch/finally
```javascript
try {
    // Code that might throw an error
    let result = riskyOperation();
    console.log(result);
} catch (error) {
    // Handle the error
    console.error('An error occurred:', error.message);
} finally {
    // This always runs
    console.log('Cleanup operations');
}
```

### Throwing Custom Errors
```javascript
function divide(a, b) {
    if (b === 0) {
        throw new Error('Division by zero is not allowed');
    }
    return a / b;
}

try {
    let result = divide(10, 0);
    console.log(result);
} catch (error) {
    console.error('Error:', error.message);
}
```

### Error Types
```javascript
try {
    // Different types of errors
    throw new Error('General error');
    throw new TypeError('Type error');
    throw new ReferenceError('Reference error');
    throw new SyntaxError('Syntax error');
} catch (error) {
    console.log('Error type:', error.constructor.name);
    console.log('Error message:', error.message);
}
```

---

## Modern JavaScript (ES6+) {#modern-js}

### Destructuring
```javascript
// Array destructuring
let numbers = [1, 2, 3, 4, 5];
let [first, second, ...rest] = numbers;
console.log(first);  // 1
console.log(second); // 2
console.log(rest);   // [3, 4, 5]

// Object destructuring
let person = { name: 'John', age: 30, city: 'New York' };
let { name, age, city } = person;
console.log(name); // 'John'
console.log(age);  // 30

// Renaming variables
let { name: fullName, age: years } = person;
console.log(fullName); // 'John'
console.log(years);    // 30
```

### Spread Operator
```javascript
// Array spread
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let combined = [...arr1, ...arr2];
console.log(combined); // [1, 2, 3, 4, 5, 6]

// Object spread
let obj1 = { a: 1, b: 2 };
let obj2 = { c: 3, d: 4 };
let combined = { ...obj1, ...obj2 };
console.log(combined); // { a: 1, b: 2, c: 3, d: 4 }

// Function arguments
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}
console.log(sum(1, 2, 3, 4, 5)); // 15
```

### Template Literals
```javascript
let name = 'Alice';
let age = 30;

// Template literal with expressions
let message = `Hello, my name is ${name} and I am ${age} years old.`;
console.log(message);

// Multi-line strings
let multiLine = `
    This is a
    multi-line
    string.
`;
console.log(multiLine);
```

### Classes
```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    greet() {
        return `Hello, I'm ${this.name}`;
    }
    
    getAge() {
        return this.age;
    }
    
    // Static method
    static species() {
        return 'Homo sapiens';
    }
}

// Inheritance
class Student extends Person {
    constructor(name, age, grade) {
        super(name, age);
        this.grade = grade;
    }
    
    study() {
        return `${this.name} is studying`;
    }
}

let student = new Student('Bob', 20, 'A');
console.log(student.greet()); // "Hello, I'm Bob"
console.log(student.study()); // "Bob is studying"
```

### Modules (ES6)
```javascript
// math.js
export function add(a, b) {
    return a + b;
}

export function subtract(a, b) {
    return a - b;
}

export default function multiply(a, b) {
    return a * b;
}

// main.js
import multiply, { add, subtract } from './math.js';

console.log(add(5, 3));        // 8
console.log(subtract(5, 3));   // 2
console.log(multiply(5, 3));   // 15
```

---

## Best Practices {#best-practices}

### Code Style
```javascript
// Use meaningful variable names
let userAge = 25;           // Good
let a = 25;                 // Bad

// Use const by default, let when reassignment is needed
const PI = 3.14159;         // Good
let currentUser = 'John';   // Good

// Use semicolons
let message = 'Hello';      // Good
let message = 'Hello'       // Works but not recommended

// Use === instead of ==
if (value === 5) {          // Good
    // ...
}

if (value == 5) {           // Bad
    // ...
}
```

### Function Guidelines
```javascript
// Keep functions small and focused
function calculateTax(income) {
    return income * 0.15;
}

// Use descriptive function names
function getUserById(id) {  // Good
    // ...
}

function getData(x) {       // Bad
    // ...
}

// Return early to avoid deep nesting
function processUser(user) {
    if (!user) {
        return null;
    }
    
    if (!user.isActive) {
        return null;
    }
    
    // Process active user
    return processActiveUser(user);
}
```

### Error Handling
```javascript
// Always handle errors
async function fetchData() {
    try {
        let response = await fetch('/api/data');
        return await response.json();
    } catch (error) {
        console.error('Failed to fetch data:', error);
        throw error;
    }
}

// Validate inputs
function divide(a, b) {
    if (typeof a !== 'number' || typeof b !== 'number') {
        throw new TypeError('Both arguments must be numbers');
    }
    
    if (b === 0) {
        throw new Error('Division by zero is not allowed');
    }
    
    return a / b;
}
```

---

## Practice Exercises {#exercises}

### Exercise 1: Basic Calculator
Create a calculator that can perform basic arithmetic operations.

```javascript
// Your solution here
function calculator(num1, operator, num2) {
    // Implement the calculator logic
}

// Test cases
console.log(calculator(5, '+', 3));  // Should return 8
console.log(calculator(10, '-', 4)); // Should return 6
console.log(calculator(6, '*', 2));  // Should return 12
console.log(calculator(15, '/', 3)); // Should return 5
```

### Exercise 2: Array Manipulation
Create functions to manipulate arrays.

```javascript
// Function to find the largest number in an array
function findLargest(numbers) {
    // Your code here
}

// Function to remove duplicates from an array
function removeDuplicates(arr) {
    // Your code here
}

// Test cases
console.log(findLargest([1, 5, 3, 9, 2])); // Should return 9
console.log(removeDuplicates([1, 2, 2, 3, 3, 3, 4])); // Should return [1, 2, 3, 4]
```

### Exercise 3: Object Manipulation
Work with objects and their properties.

```javascript
// Create a function that counts properties in an object
function countProperties(obj) {
    // Your code here
}

// Create a function that merges two objects
function mergeObjects(obj1, obj2) {
    // Your code here
}

// Test cases
let person = { name: 'John', age: 30, city: 'New York' };
console.log(countProperties(person)); // Should return 3

let obj1 = { a: 1, b: 2 };
let obj2 = { c: 3, d: 4 };
console.log(mergeObjects(obj1, obj2)); // Should return { a: 1, b: 2, c: 3, d: 4 }
```

### Exercise 4: Async Practice
Practice with asynchronous JavaScript.

```javascript
// Create a function that simulates an API call
function simulateAPICall(data, delay = 1000) {
    // Return a promise that resolves after the delay
    // Your code here
}

// Use async/await to handle the API call
async function handleAPICall() {
    // Your code here
}

// Test the function
handleAPICall();
```

### Exercise 5: DOM Manipulation
Create a simple interactive element.

```html
<!DOCTYPE html>
<html>
<head>
    <title>DOM Exercise</title>
</head>
<body>
    <button id="colorButton">Change Color</button>
    <div id="colorDiv" style="width: 100px; height: 100px; background-color: red;"></div>
    
    <script>
        // Your JavaScript code here
        // Make the button change the div's color randomly when clicked
    </script>
</body>
</html>
```

---

## Solutions to Exercises

### Solution 1: Basic Calculator
```javascript
function calculator(num1, operator, num2) {
    switch (operator) {
        case '+':
            return num1 + num2;
        case '-':
            return num1 - num2;
        case '*':
            return num1 * num2;
        case '/':
            if (num2 === 0) {
                throw new Error('Division by zero is not allowed');
            }
            return num1 / num2;
        default:
            throw new Error('Invalid operator');
    }
}
```

### Solution 2: Array Manipulation
```javascript
function findLargest(numbers) {
    if (numbers.length === 0) {
        return undefined;
    }
    return Math.max(...numbers);
}

function removeDuplicates(arr) {
    return [...new Set(arr)];
    // Alternative: return arr.filter((item, index) => arr.indexOf(item) === index);
}
```

### Solution 3: Object Manipulation
```javascript
function countProperties(obj) {
    return Object.keys(obj).length;
}

function mergeObjects(obj1, obj2) {
    return { ...obj1, ...obj2 };
    // Alternative: return Object.assign({}, obj1, obj2);
}
```

### Solution 4: Async Practice
```javascript
function simulateAPICall(data, delay = 1000) {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve(`API Response: ${data}`);
        }, delay);
    });
}

async function handleAPICall() {
    try {
        console.log('Making API call...');
        let result = await simulateAPICall('Hello from API');
        console.log(result);
    } catch (error) {
        console.error('API call failed:', error);
    }
}
```

### Solution 5: DOM Manipulation
```html
<script>
document.getElementById('colorButton').addEventListener('click', function() {
    const colors = ['red', 'blue', 'green', 'yellow', 'purple', 'orange'];
    const randomColor = colors[Math.floor(Math.random() * colors.length)];
    document.getElementById('colorDiv').style.backgroundColor = randomColor;
});
</script>
```

---

## Next Steps

Congratulations on completing this JavaScript tutorial! Here's what you can do next:

1. **Practice More**: Build small projects like a to-do list, calculator, or simple game
2. **Learn Frameworks**: Explore React, Vue.js, or Angular for frontend development
3. **Backend Development**: Learn Node.js for server-side JavaScript
4. **Advanced Topics**: Study design patterns, testing, and performance optimization
5. **Build Projects**: Create a portfolio of JavaScript projects

### Recommended Resources
- [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [JavaScript.info](https://javascript.info/)
- [freeCodeCamp](https://www.freecodecamp.org/)
- [Eloquent JavaScript](https://eloquentjavascript.net/)

Happy coding! 🚀