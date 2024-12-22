# Comprehensive TypeScript Tutorial

TypeScript is a strongly-typed superset of JavaScript that adds optional static typing and other powerful features. Developed and maintained by Microsoft, it is designed to make development more robust and efficient. This tutorial will walk you through the core concepts and practical usage of TypeScript.

---

## Table of Contents

- [Introduction to TypeScript](#introduction)
- [Basic TypeScript Syntax](#basic-typescript-syntax)
- [Conditionals](#conditionals)
- [Loops](#loops)
- [Advanced TypeScript Features](#advanced-typescript-features)
- [Working with Classes and Objects](#working-with-classes-and-objects)
- [Modules and Namespaces](#modules-and-namespaces)
- [TypeScript in Practice](#typescript-in-practice)
- [Debugging and Best Practices](#debugging-and-best-practices)
- [Common Pitfalls and How to Avoid Them](#common-pitfalls-and-how-to-avoid-them)
- [Playground](https://www.typescriptlang.org/play/)
---

## Introduction

### What is TypeScript?
TypeScript extends JavaScript by adding static types. This means you can specify the type of variables, function parameters, and return values, allowing for better tooling and fewer runtime errors. TypeScript code compiles to plain JavaScript, so it works wherever JavaScript runs.

### Benefits of Using TypeScript
- **Improved Code Quality:** TypeScript helps catch errors during development.
- **Better Tooling:** Enhanced autocomplete, navigation, and refactoring.
- **Scalability:** Makes maintaining large codebases easier.
- **Interoperability:** Works seamlessly with JavaScript and popular frameworks like React, Angular, and Node.js.

### Setting Up Your Environment
1. Install Node.js if you haven’t already.
2. Install TypeScript globally using npm:
   ```bash
   npm install -g typescript
   ```
3. Verify installation:
   ```bash
   tsc --version
   ```
4. Initialize a TypeScript project:
   ```bash
   tsc --init
   ```
5. Write your first `.ts` file and compile it to JavaScript:
   ```bash
   tsc file.ts
   ```

---

## Basic TypeScript Syntax

### Variables and Types

**Variables**
TypeScript provides various built-in types, such as `number`, `string`, `boolean`, `array`, and `tuple`.

```typescript
let age: number = 25;
let name: string = "Alice";
let isDeveloper: boolean = true;
let hobbies: string[] = ["coding", "reading"];
```

**Tuple**
```typescript
// Define a tuple with a string and a number
let person: [string, number];

// Initialize the tuple
person = ["Alice", 30];

console.log(`Name: ${person[0]}`); // Output: Name: Alice
console.log(`Age: ${person[1]}`); // Output: Age: 30

//Optional Elements
// A tuple where the last element is optional
let product: [string, number, string?];

product = ["Laptop", 1500];
console.log(product); // Output: ['Laptop', 1500]

product = ["Laptop", 1500, "Electronics"];
console.log(product); // Output: ['Laptop', 1500, 'Electronics']

// Rest Elements
// A tuple with rest elements
let coordinates: [number, number, ...number[]];

coordinates = [10, 20];
console.log(coordinates); // Output: [10, 20]

coordinates = [10, 20, 30, 40];
console.log(coordinates); // Output: [10, 20, 30, 40]

//Destructuring
let user: [string, number] = ["Alice", 25];

// Destructuring the tuple
let [name, age] = user;

console.log(`Name: ${name}`); // Output: Name: Alice
console.log(`Age: ${age}`);   // Output: Age: 25
```

**Types**

**Union Types**
```typescript
type Status = "success" | "failure" | "pending";

let requestStatus: Status = "success";
```

**Intersection Types**
```typescript
type Identifiable = { id: string };
type Timestamped = { createdAt: Date };

type Record = Identifiable & Timestamped;

const record: Record = {
    id: "123",
    createdAt: new Date()
};
```

**Utility Types**
```typescript
type User = {
    name: string;
    age: number;
    email: string;
};

type UserWithoutEmail = Omit<User, "email">;

const user: UserWithoutEmail = {
    name: "Alice",
    age: 25
};
```

**Defining Aliases for Primitives or Functions**
```typescript
type Age = number;

const myAge: Age = 30;

type Greet = (name: string) => string;

const greet: Greet = (name) => `Hello, ${name}`;
```

**Immutable Types**
```typescript
type Point = {
    readonly x: number;
    readonly y: number;
};

const p: Point = { x: 10, y: 20 };
// p.x = 30; // Error: Cannot assign to 'x' because it is a read-only property
```

### Map
```typescript
// Create a new Map
const myMap = new Map<string, number>();

// Add key-value pairs
myMap.set("Alice", 25);
myMap.set("Bob", 30);
myMap.set("Charlie", 35);

// Access a value by key
console.log(myMap.get("Alice")); // Output: 25

// Check if a key exists
console.log(myMap.has("Bob")); // Output: true

// Delete a key-value pair
myMap.delete("Charlie");
console.log(myMap.has("Charlie")); // Output: false

// Get the size of the Map
console.log(myMap.size); // Output: 2
```

### Functions and Parameters
Functions can have typed parameters and return types.

```typescript
function add(a: number, b: number): number {
  return a + b;
}

function greet(name: string, isMorning: boolean = true): string {
  return isMorning ? `Good morning, ${name}!` : `Hello, ${name}!`;
}
```

**First-Class Functions**
```typescript
const greet = (name: string): string => `Hello, ${name}!`;

const greeter = greet;
console.log(greeter("Alice")); // Output: Hello, Alice!
```

**Higher-Order Functions**
```typescript
const applyFunction = (fn: (x: number) => number, value: number): number => {
    return fn(value);
};

const double = (x: number): number => x * 2;

console.log(applyFunction(double, 5)); // Output: 10
```

**Anonymous Functions**
```typescript
const numbers = [1, 2, 3, 4];

// Use an anonymous function with type inference
const doubled = numbers.map((num) => num * 2);

console.log(doubled); // Output: [2, 4, 6, 8]
```

**Pure Functions**
```typescript
const pureAdd = (a: number, b: number): number => a + b;

console.log(pureAdd(2, 3)); // Output: 5
```

**Immutability**
```typescript
const addToArray = (arr: readonly number[], value: number): number[] => {
    return [...arr, value]; // Returns a new array instead of modifying the original
};

const nums: readonly number[] = [1, 2, 3];
const newNums = addToArray(nums, 4);

console.log(newNums); // Output: [1, 2, 3, 4]
console.log(nums);    // Output: [1, 2, 3]
```

**Functional Composition**
```typescript
const double = (x: number): number => x * 2;
const increment = (x: number): number => x + 1;

const compose = (f: (x: number) => number, g: (x: number) => number) => {
    return (x: number): number => f(g(x));
};

const doubleAfterIncrement = compose(double, increment);

console.log(doubleAfterIncrement(3)); // Output: 8
```

**Map, Filter, Reduce**
```typescript
const numbers = [1, 2, 3, 4, 5];

// Double each number
const doubled = numbers.map((num) => num * 2);

// Filter out odd numbers
const evenNumbers = doubled.filter((num) => num % 2 === 0);

// Sum all numbers
const sum = evenNumbers.reduce((acc, num) => acc + num, 0);

console.log(sum); // Output: 12
```

**Currying**
```typescript
const add = (a: number) => (b: number) => a + b;

const addFive = add(5);

console.log(addFive(3)); // Output: 8
```

**Type Guards for Functional Programming**
```typescript
const filterStrings = (items: (string | number)[]): string[] => {
    return items.filter((item): item is string => typeof item === "string");
};

const mixed = ["hello", 42, "world", 99];
const strings = filterStrings(mixed);

console.log(strings); // Output: ['hello', 'world']
```

**Recursive Functions**
```typescript
const factorial = (n: number): number => {
    return n === 0 ? 1 : n * factorial(n - 1);
};

console.log(factorial(5)); // Output: 120
```

**Functional Libraries**
You can integrate libraries like Ramda, Lodash, or fp-ts to write more advanced functional code in TypeScript.

Example with fp-ts:
```typescript
import { pipe } from "fp-ts/function";
import * as A from "fp-ts/Array";

const numbers = [1, 2, 3, 4, 5];

const result = pipe(
    numbers,
    A.map((x) => x * 2),
    A.filter((x) => x > 5)
);

console.log(result); // Output: [6, 8, 10]
```

### Interfaces and Type Aliases
Interfaces and type aliases allow you to define custom types.

```typescript
interface Person {
  name: string;
  age: number;
  isEmployed?: boolean; // Optional property
}

type Coordinates = [number, number];

const person: Person = {
  name: "Bob",
  age: 30,
};
```

## Conditionals

**if-else Conditional**
```typescript
let age: number = 18;

if (age >= 18) {
    console.log("You are eligible to vote.");
} else {
    console.log("You are not eligible to vote.");
}
```

**if-else if Ladder**
```typescript
let score: number = 75;

if (score >= 90) {
    console.log("Grade: A");
} else if (score >= 80) {
    console.log("Grade: B");
} else if (score >= 70) {
    console.log("Grade: C");
} else {
    console.log("Grade: F");
}
```

**switch Statement**
```typescript
let day: string = "Tuesday";

switch (day) {
    case "Monday":
        console.log("Start of the work week!");
        break;
    case "Friday":
        console.log("Last day of the work week!");
        break;
    case "Saturday":
    case "Sunday":
        console.log("It's the weekend!");
        break;
    default:
        console.log("It's a regular weekday.");
}
```

**Ternary Operator**
```typescript
let isMember: boolean = true;
let discount: number = isMember ? 10 : 0;

console.log(`Your discount is ${discount}%`);
```

**Using Enums with Conditionals**
```typescript
enum Role {
    Admin,
    User,
    Guest
}

let currentRole: Role = Role.User;

if (currentRole === Role.Admin) {
    console.log("Welcome Admin! You have full access.");
} else if (currentRole === Role.User) {
    console.log("Welcome User! You have limited access.");
} else {
    console.log("Welcome Guest! Please log in.");
}
```

**Type Guards with Conditionals**
```typescript
function printLength(input: string | number): void {
    if (typeof input === "string") {
        console.log(`The length of the string is ${input.length}`);
    } else {
        console.log(`The number is ${input}`);
    }
}

printLength("TypeScript"); // Output: The length of the string is 10
printLength(42);           // Output: The number is 42
```

## Loops
**Iterating Through a Map**

```typescript
for (const [key, value] of myMap) {
   console.log(`${key}: ${value}`);
}
// Output:
// Alice: 25
// Bob: 30
```

```typescript
myMap.forEach((value, key) => {
   console.log(`${key}: ${value}`);
});
// Output:
// Alice: 25
// Bob: 30
```

### Iterating through Arrays

**Filtering an Array**

```typescript
const numbers = [1, 2, 3, 4, 5, 6];

// Filter even numbers
const evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // Output: [2, 4, 6]
```

**Filtering an Array**
```typescript
const names = ["Alice", "Bob", "Charlie"];

// Convert names to uppercase
const upperCaseNames = names.map(name => name.toUpperCase());
console.log(upperCaseNames); // Output: ["ALICE", "BOB", "CHARLIE"]
```

**Reducing an Array**
```typescript
const numbers = [1, 2, 3, 4, 5];

// Sum all numbers
const sum = numbers.reduce((accumulator, current) => accumulator + current, 0);
console.log(sum); // Output: 15
```

**Combining filter and map**
```typescript
const numbers = [1, 2, 3, 4, 5, 6];

// Get squares of even numbers
const evenSquares = numbers
        .filter(num => num % 2 === 0) // Filter even numbers
        .map(num => num * num);       // Square each number
console.log(evenSquares); // Output: [4, 16, 36]
```

**Processing an Array of Objects**
```typescript
const users = [
   { name: "Alice", age: 25 },
   { name: "Bob", age: 30 },
   { name: "Charlie", age: 35 },
];

// Get names of users older than 28
const namesOfOlderUsers = users
        .filter(user => user.age > 28)  // Filter users by age
        .map(user => user.name);        // Extract names
console.log(namesOfOlderUsers); // Output: ["Bob", "Charlie"]
```

**Java-Like Sorted Streams**
```typescript
const numbers = [5, 3, 8, 1, 4];

// Sort and double the numbers
const sortedDoubles = numbers
    .sort((a, b) => a - b) // Sort in ascending order
    .map(num => num * 2);  // Double each number
console.log(sortedDoubles); // Output: [2, 6, 8, 10, 16]
```

**Grouping Similar to Java Streams**
```typescript
const users = [
    { name: "Alice", age: 25 },
    { name: "Bob", age: 30 },
    { name: "Charlie", age: 25 },
];

// Group users by age
const groupedByAge = users.reduce((group, user) => {
    const ageGroup = group[user.age] || [];
    ageGroup.push(user);
    group[user.age] = ageGroup;
    return group;
}, {} as { [key: number]: typeof users });

console.log(groupedByAge);
// Output:
// {
//   25: [{ name: "Alice", age: 25 }, { name: "Charlie", age: 25 }],
//   30: [{ name: "Bob", age: 30 }]
// }
```

## Advanced TypeScript Features

### Generics
Generics enable you to create reusable components.

```typescript
function identity<T>(value: T): T {
  return value;
}

let stringIdentity = identity<string>("hello");
let numberIdentity = identity<number>(42);
```

### Enums
Enums define a set of named constants.

```typescript
enum Direction {
  Up,
  Down,
  Left,
  Right,
}

let move: Direction = Direction.Up;
```

### Utility Types
TypeScript includes utility types such as `Partial`, `Pick`, and `Omit`.

```typescript
interface Task {
  id: number;
  title: string;
  completed: boolean;
}

const update: Partial<Task> = {
  completed: true,
};
```

---

## Working with Classes and Objects

### Classes and Inheritance
TypeScript supports object-oriented programming.

```typescript
class Animal {
  constructor(public name: string) {}

  makeSound(): void {
    console.log("Some generic sound");
  }
}

class Dog extends Animal {
  makeSound(): void {
    console.log("Woof!");
  }
}
```

### Access Modifiers
Access modifiers include `public`, `private`, and `protected`.

```typescript
class Car {
  private engine: string;

  constructor(engine: string) {
    this.engine = engine;
  }

  start(): void {
    console.log(`Engine ${this.engine} started`);
  }
}
```

### Abstract Classes and Interfaces
Abstract classes define blueprints for derived classes.

```typescript
abstract class Shape {
  abstract calculateArea(): number;
}

class Circle extends Shape {
  constructor(public radius: number) {
    super();
  }

  calculateArea(): number {
    return Math.PI * this.radius ** 2;
  }
}
```

---

## Modules and Namespaces

### Import and Export
Organize code using ES6 modules.

```typescript
// math.ts
export function add(a: number, b: number): number {
  return a + b;
}

// app.ts
import { add } from "./math";
console.log(add(2, 3));
```

### Namespaces
Group related functionality using namespaces.

```typescript
namespace Utils {
  export function log(message: string): void {
    console.log(message);
  }
}

Utils.log("Hello from namespace");
```

---

## TypeScript in Practice

### Integration with JavaScript Libraries
Use `@types` packages for type definitions.

```bash
npm install --save-dev @types/lodash
```

### TypeScript and React
TypeScript enhances type safety in React components.

```tsx
import React from "react";

type Props = {
  name: string;
  age?: number;
};

const Greeting: React.FC<Props> = ({ name, age }) => (
  <div>
    Hello, {name}! {age && `You are ${age} years old.`}
  </div>
);
```

### Setting Up a TypeScript Project
1. Create a `tsconfig.json` file:
   ```bash
   tsc --init
   ```
2. Configure the compiler options in `tsconfig.json`.
3. Compile and run your TypeScript code:
   ```bash
   tsc && node dist/index.js
   ```

---

## Debugging and Best Practices

### Debugging TypeScript Code
Use source maps to debug TypeScript in modern browsers.

```json
{
  "compilerOptions": {
    "sourceMap": true
  }
}
```

### Linting and Formatting
Use tools like ESLint and Prettier to maintain code quality.

```bash
npm install --save-dev eslint prettier
```

### Writing Clean TypeScript Code
- Use descriptive variable names.
- Avoid `any` unless necessary.
- Prefer interfaces over type aliases for object types.

---

## Common Pitfalls and How to Avoid Them

1. **Overusing `any`:** Stick to specific types for better type safety.
2. **Ignoring Type Errors:** Always address errors instead of suppressing them.
3. **Complex Union Types:** Simplify where possible to enhance readability.

---

TypeScript is a powerful tool for modern development, and mastering it can significantly improve your coding efficiency and reliability. This guide provides a solid foundation, but the best way to learn is by practicing and building projects. Happy coding!

