\*\*Title: Any vs unknown in TypeScript: Understanding Type Safety and Type Narrowing

\*\*Introduction:

TypeScript is designed to make JavaScript safer by adding a strong type system. One of its biggest advantages is catching errors before the code runs. However, not all TypeScript types provide the same level of safety.

Two commonly discussed types are any and unknown. At first glance, they may seem similar because both can hold any kind of value. But in reality, they behave very differently.

The any type removes TypeScript protection completely, while unknown keeps safety checks in place. This is why any is often called a type safety hole, and unknown is considered the safer alternative for unpredictable data.

\*\*The Problem with any
When you use any, TypeScript stops checking your code. It just trusts you blindly.

function printName(data: any) {
console.log(data.name.toUpperCase());
}

printName(42); //Crashes at runtime!

typeScript showed zero errors here. But when the code runs, it crashes. That's the danger — any hides your mistakes instead of catching them.

\*\*unknown is the Safer Choice
unknown also accepts any type of value, but it won't let you use that value without checking what it is first.

function printName(data: unknown) {
console.log(data.name); //Error: Object is of type 'unknown'
}

This error is a good thing! TypeScript is telling you: "Check what this is before you use it."

\*\*Type Narrowing
Type narrowing is how you tell TypeScript what type something actually is, so you can safely use it.

\*\*Using typeof
function handleInput(value: unknown) {
if (typeof value === "string") {
console.log(value.toUpperCase()); //Safe, TypeScript knows it's a string
} else if (typeof value === "number") {
console.log(value.toFixed(2)); //Safe, TypeScript knows it's a number
}
}

handleInput("hello"); // HELLO
handleInput(3.14159); // 3.14

\*\*Using instanceof
function handleError(error: unknown) {
if (error instanceof Error) {
console.log(error.message); //Safe
} else {
console.log("Something went wrong");
}
}

\*\*Custom Type Guard (for objects)
When you're dealing with an object (like API data), you can write a function to check its shape:
interface User {
name: string;
email: string;
}

function isUser(data: unknown): data is User {
return (
typeof data === "object" &&
data !== null &&
"name" in data &&
"email" in data
);
}

function greetUser(data: unknown) {
if (isUser(data)) {
console.log(`Hello, ${data.name}!`); //Safe
} else {
console.log("Not a valid user.");
}
}

greetUser({ name: "Alice", email: "alice@example.com" }); // Hello, Alice!
greetUser("random string"); // Not a valid user.

\*\*Conclusion
any feels convenient but it breaks the whole point of using TypeScript. unknown is the right tool when you don't know what type something is — it forces you to check first, so your code doesn't blow up at runtime.
