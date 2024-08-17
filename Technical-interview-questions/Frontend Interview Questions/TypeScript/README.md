# TypeScript Interview Questions

## 1. What is TypeScript?
TypeScript is a statically typed superset of JavaScript that compiles to plain JavaScript. It offers better tooling at development time (like autocomplete and error checking) and helps to write more robust code.

## 2. How do you install TypeScript?
You can install TypeScript globally using npm:

```bash
npm install -g typescript
```

## 3. How do you compile a TypeScript file?
You can compile a TypeScript file using the tsc command followed by the filename:


```bash
tsc filename.ts
```

## 4. How do you declare a variable in TypeScript?
You can declare a variable using `let`, `const`, or `var`, followed by the type annotation.

**Example:**

```typescript
let name: string = "Alice";
const age: number = 30;
```

## 5. What are interfaces in TypeScript?
An interface defines the structure of an object, specifying what properties and methods it should contain.

**Example:**

```typescript
interface Person {
    name: string;
    age: number;
}

const person: Person = {
    name: "Alice",
    age: 30
};
```


## 6. How do you create a function in TypeScript?
You can define a function with type annotations for the parameters and return type.

**Example:**

```typescript
function greet(name: string): string {
    return `Hello, ${name}!`;
}

console.log(greet("Alice")); // Output: Hello, Alice!
```

## 7. What are generics in TypeScript?
Generics allow you to create reusable components that can work with any data type.

**Example:**

```typescript
function identity<T>(arg: T): T {
    return arg;
}

const output = identity<string>("Hello, World!");
```


## 8. How do you use Union types?
Union types allow a variable to hold different types.

**Example:**

```typescript
function printId(id: number | string) {
    console.log(`Your ID is: ${id}`);
}

printId(101); // Output: Your ID is: 101
printId("202"); // Output: Your ID is: 202
```

## 9. What are Enums in TypeScript?
Enums are a way to define named constants, which can be numeric or string-based.

**Example:**

```typescript
enum Color {
    Red,
    Green,
    Blue
}

let c: Color = Color.Green;
console.log(c); // Output: 1
```

## 10. How do you handle optional properties in TypeScript?
You can use the `?` operator in an interface to denote optional properties.

**Example:**

```typescript
interface User {
    id: number;
    name: string;
    age?: number; // optional
}

const user: User = {
    id: 1,
    name: "Alice"
};
```
## 11 What is Type Assertion?
Type assertion is a way to inform the TypeScript compiler about the type of a variable.

**Example:**

```typescript
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;
```

## 12. How do you create a class in TypeScript?
You can define a class using the class keyword, including properties and methods.

**Example:**

```typescript
class Animal {
    name: string;

    constructor(name: string) {
        this.name = name;
    }

    speak(): void {
        console.log(`${this.name} makes a noise.`);
    }
}

const dog = new Animal("Dog");
dog.speak(); // Output: Dog makes a noise.
```

### 13. What are type aliases?
Type aliases allow you to create a new name for a type.

**Example:**

```typescript
type StringOrNumber = string | number;

let value: StringOrNumber;
value = "Hello";  // valid
value = 123;      // valid
```


## 14. How do you define a tuple in TypeScript?
A tuple is an array with a fixed number of elements where each element can have a different type.

**Example:**

```typescript
let user: [string, number] = ["Alice", 30];
```

## 14. What are the differences between interface and type?
- Both can define object shapes.
- Interfaces can be extended while types cannot be extended (but can use intersection).
- Types can represent any type, including primitives, unions, and tuples.

**Example:**

```typescript
interface Person {
    name: string;
}

type User = {
    name: string;
    age: number;
};

// Extending an interface
interface Employee extends Person {
    role: string;
}

// Using intersection with types
type Admin = User & { admin: boolean };
```

## 15. How do you implement inheritance in TypeScript classes?
You can use the `extends` keyword to inherit from a base class.

**Example:**

```typescript
class Animal {
    constructor(public name: string) {}

    speak(): void {
        console.log(`${this.name} makes a noise.`);
    }
}

class Dog extends Animal {
    speak(): void {
        console.log(`${this.name} barks.`);
    }
}

const dog = new Dog("Rex");
dog.speak(); // Output: Rex barks.
```

## 16. What is the never type?
The never type represents values that never occur. It is used for functions that throw exceptions or never return.


**Example:**

```typescript
function error(message: string): never {
    throw new Error(message);
}
```

## 17. How do you use decorators in TypeScript?
Decorators are special annotations that can be attached to classes, methods, or properties. They can be used to modify the behavior of the class or method.


**Example:**

```typescript
function log(target: any, propertyName: string, descriptor: PropertyDescriptor) {
    const originalMethod = descriptor.value;

    descriptor.value = function(...args: any[]) {
        console.log(`Calling ${propertyName} with`, args);
        return originalMethod.apply(this, args);
    };
}

class Calculator {
    @log
    add(a: number, b: number): number {
        return a + b;
    }
}

const calc = new Calculator();
calc.add(2, 3); // Logs: Calling add with [2, 3]
```
