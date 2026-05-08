\*\*\*Title: TypeScript Generics :- Write Once, Use Everywhere

\*\*\*Introduction
Have you ever written the same function twice just because the data type was different? Generics solve that. They let you write a function or component once and use it with any type — without losing type safety. Let's break it down simply.

\*\*\*The Problem Without Generics
Say you want a function that returns the first item of an array.

function getFirstNumber(arr: number[]): number {
return arr[0];
}

function getFirstString(arr: string[]): string {
return arr[0];
}

These two functions do the exact same thing. The only difference is the type. That's repetition — and it gets worse as your project grows.
You might think: "Just use any!"

function getFirst(arr: any[]): any {
return arr[0];
}

But now TypeScript has no idea what type comes out. You've lost all the benefits of TypeScript.

\*\*\*Generics to the Rescue
A generic function uses a type parameter (usually written as <T>) as a placeholder for the actual type.

function getFirst<T>(arr: T[]): T | undefined {
return arr[0];
}

const firstNum = getFirst([10, 20, 30]); // Type: number
const firstStr = getFirst(["a", "b", "c"]); // Type: string

TypeScript figures out the type automatically based on what you pass in. One function, any type, full safety.

\*\*\*Generic Interfaces
You can use generics in interfaces too. A common example is wrapping API responses:

interface ApiResponse<T> {
data: T;
status: number;
message: string;
}

interface User {
id: number;
name: string;
}

const response: ApiResponse<User> = {
data: { id: 1, name: "Alice" },
status: 200,
message: "OK",
};

console.log(response.data.name); // "Alice" — TypeScript knows the type

\*\*\*Generic Constraints
Sometimes you want T to only accept types that have certain properties. Use extends for that.

function logLength<T extends { length: number }>(item: T): void {
console.log(item.length);
}

logLength("Hello"); // 5
logLength([1, 2, 3]); // 3
logLength(42);

\*\*\*Generic Classes
Generics also work great for classes — like a simple typed stack:
class Stack<T> {
private items: T[] = [];

push(item: T): void {
this.items.push(item);
}

pop(): T | undefined {
return this.items.pop();
}
}

const numStack = new Stack<number>();
numStack.push(1);
numStack.push("hi"); // ❌ Error: string not allowed (caught at compile time)

const strStack = new Stack<string>();
strStack.push("hello");

\*\*\*Conclusion
Generics might look scary at first with all the <T> symbols, but the idea is simple: write the logic once, let TypeScript handle the types.
Key things to remember:

<T> is just a placeholder that gets replaced with a real type when you use the function
TypeScript usually infers T automatically — you don't always have to write it
Use extends when you need T to have specific properties

Once you get comfortable with generics, you'll use them all the time. They're one of the most useful parts of TypeScript.
