---
layout: post
subtitle: Typescript for a developer
categories: markdown
title: Learn Typescript in 15 minutes
date: '2022-03-14'
tags: [typescript, ts, web development]
draft: false
summary: After reading this article you will know more than enough typescript to start writing production applications, assuming you already know javascript. This article is framework agnostic and covers the core of the language. This can be used as a Typescript quick starter or a quick refresher. This article assumes you already know javascript
images: []
# layout: PostLayout
canonicalUrl:
---

---

After reading this article you will know more than enough typescript to start writing production applications, assuming you already know javascript. This article is framework agnostic and covers the core of the language. This can be used as a Typescript quick starter or a quick refresher. You can find the code for this article in [this code-sandbox](https://codesandbox.io/s/learn-typescript-in-10-minutes-0s50q?file=/src/index.ts).

## What and Why of Typescript

Typescript is a superset of Javascript. This means whatever javascript you write is still valid typescript. How is typescript is different then? Typescript extends javascript by adding types, features which are yet not in javascript and a few other utilities. End of the day typescript compiles to javascript. In simple even you write typescript, javascript is what shipped to the browser.

### Why do we even need typescript, javascript isn't enough?

Let me explain through an example:
You wrote a sum function:

```js
const sum = (a, b) => a + b
```

Whenever you call the sum function with two number arguments it will work fine. But, what if you pass a string and a number or both strings or even number and an object? This is not a problem if your project is just a couple of lines of codes and only one or two people are working on it. But what if your product is a few thousand lines of code or even be it in some hundreds. Add a few more people working on the project and using the sum function. All of them may not know the internals of the function. Now one of them can call the function with wrong types of arguments. This will result in unexpected results. May lead to terrible experience if this gets pushed to production.

The issue in the scenario above can be caught earlier with typescript. Typescript will complain you if you are trying to pass a string to a declaration of types of number.

Let us see the equivalent typescript declaration of sum function in typescript

```js
const sum = (a: number, b: number) => a + b
// Now if you try to pass a non-number value to a or b typescript will complain
const s1 = sum(3, 5)
// works
const s2 = sum(2, '33')
// Error
// Argument of type '"33"' is not assignable to parameter of type 'number'
```

Typescript requires some setup and config to work for a real project but to follow this article you can use either of the following links

- [Codesandbox link (Contains all code examples, Fork the sandbox and play around)](https://codesandbox.io/s/learn-typescript-in-10-minutes-0s50q?file=/src/index.ts)
- https://www.typescriptlang.org/play

## Types 101: the basics of types in typescript

In a simple term, You can think of typescript types as the type of the variable. It can be defined explicitly (by you) or can be inferred implicitly from the assignment (by the compiler).

Syntax (explicit types):

```js
// declaration:type = assignmet; (assignment is optional for let, var)
// const someConst: string = 'some const';
// let someNumber:number = 44;
// examples:
// here the type of num varialbe is number, you cannot assign other types to the variable num.
let num: number = 44
// valid
num = 8595
// invalid
num = '333'
// valid
num = 3445.88
// One more example
let str: string = 'hello, I can only be a string'
// valid
str = 'Just another string'
// invalid
str = 22
// one more exaple with only declaration but no assignmet
let someNumber: number
// valid
someNumber = 55
// invalid
someNumber = 'I am not a number'
// invalid
someNumber = '333'
// valid
someNumber = Infinity
```

```js
Syntax (Implicit types):
// following line declares a variable implicitNum, type of number and assigns 44 to it. The value assigned to it is a number, so typescript automatically determines the type of the variable. This is the type inference.
let implicitNum = 44;
// valid
implicitNum = 66;
// invalid
implicitNum = 'Not allowed';
```

### As we are familiar with the types, now let us learn the most basic types in typescript:

- Boolean
- Number
- String
- Array

```js
// Boolean
const alwaysTrue: boolean = true
let onlyBool: boolean = true
// valid
onlyBool = false
// invalid
onlyBool = 'true'
// Following operation is invalid because + operator is only defined for string and numbers
const addition = alwaysTrue + onlyBool
// Number
const againSomeNum = 55
let someNumberAgain = 66
// invalid
someNumberAgain = '44'
// valid
someNumberAgain = 365
// String
let someStrAgain = 'Yes, this is a string'
// valid
someStrAgain = 'ok, valid'
// invalid
someStrAgain = 4345
someStrAgain = true
// Array
// There are two ways to declare an array
// normal array syntax --
const someArray: number[] = [1, 2, 3, 4, 5]
// valid
someArray.push(34546)
// invalid
someArray.push('ok')
someArray.push(true)
// Generic array syntax --
const oneMoreArray: Array<number> = [34, 35, 23, 21]
// valid
oneMoreArray.push(4354)
oneMoreArray.push(34.234)
// invalid
oneMoreArray.push('not valid!')
```

### Some more basic types in typescript

#### Any

It is the easiest way to get started with typescript. It is a supertype to all type in typescript. Any is a way to opt-out of type checking. So, you can assign a value of any type to this type of variable and vice-versa.
This can be the only friend of you when you are just trying to get started with typescript. But don't stay around with the guy, as he is going to spoil you. Other types are more loyal and hence trustworthy.

```js
// Any
let assignAnything:any = 44;
assignAnything = 'Assign string';
assignAnything = true;
assignAnything = false;
assignAnything = [35, 45, 44];
let arrayOfAnyType: any[] = [454, 435, 'string also', false];
// You can even access properties on an non object variable
// Even the code below fails, typescript doesn't complain
assignAnything.sayHello();
// Assin to any type of variable Quite risky, right?
let strictlyNumber:number = 66;
const anAnyTypeOfVariable: any = 'Not a number, but can be assigned to number';
// valid
strictlyNumber = anAnyTypeOfVariable;
Unknown
Unknown type is similar to any, you can assign any type of value to an unknown type of variable. But the difference between any and unknown is that you can't assign an unknown type of value to other types of variables except to type any.
// Unknown
let unknownVariable:unknown = 44;
assignAnything = 'Assign string';
assignAnything = true;
assignAnything = false;
assignAnything = [35, 45, 44];
let unknownArray: unknown[] = [454, 435, 'string also', false];
// You cannot access properties on an unknown type of vlaue
// invalid
unknownVariable.sayHello();
// Cannot assign to other types
let someStrictNumber:number = 66;
const unknownValueAgain: unknown = 'Not a number, but can be assigned to number';
// invalid
someStrictNumber = unknownValueAgain;
// but can assign to any type
let someAnyTypeVariable: any = [34, 5];
let someUnknownVariable:unknown = 'unknown value';
// valid
someAnyTypeVariable = someUnknownVariable;
```

#### Null and Undefined

The behaviour of Null and Undefined types depends on a flag ( - strictNullCheck) passed to the compiler. It is recommended to set this flag to true. When the flag is not set Null and Undefined are sub-types of all other types. You can assign them to any variables of all other types. But when the ( - strictNullCheck) flag is set Null and Undefined can be assigned only to their respective type, any and unknown types. And undefined can also be assigned to void type.

```js
// Null
let nullValue: null = null
// ivalid
nullValue = 33
let someNumberA: number = 333
someNumberA = nullValue
// valid
let anyValueA: any = 354
anyValueA = nullValue
let unknowValueA: unknown = 3543
unknowValueA = nullValue
// Undefined
let undefinedValueA: undefined = undefined
// invalid
undefinedValueA = 33
let someNumberB: number = 333
someNumberB = undefinedValueA
// valid
let anyValueB: any = 354
anyValueA = undefinedValueA
let unknowValueB: unknown = 3543
unknowValueA = undefinedValueA
```

#### Void

Type Void is used for declaring return type of functions which returns nothing or void but finishes execution.

```js
// The example will be more clear once we learn type function. Here, the function greets return type is void. In simple its return value doesn't matter.
function greet(name: string): void {
  console.log(`hello ${name}`)
  // even this function is returning nothing explicitly, it is returning undefined implicityly. We already know undefined is assignable to void. So, this is valid
}
// void keyword in javascript discards the value returned. so the following declaration is totaly valid
function discardTheReturnValue(name: string): void {
  console.log(`hello ${name}`)
  return void 333
}
```

#### Never

Never type is used to declare the return type of functions which never returns (runs infinitely or throws an error). Never can be assigned to any type but no type can be assigned to never (even any is not assignable to never).

```js
// Never
// Both functions below never returns
function throwSomeError():never {
throw new Error('I am only throwing error');
}
function neverReturn():never {
while(true) {}
}
Enum
Enums are a way to give names and organise numeric values. You can define an enum with possible numeric values (with their names) and access them with object-like dot notation.
// Enum
enum Fruit {
Apple,
Orange,
Melon,
}
let f: Fruit = Fruit.Apple;
console.log(f === 0) // true
console.log(f === Fruit.Apple) // true
console.log(f === Fruit.Orange) // false
```

## More complex types and typecasting in typescript

By now you should be able to create types for primitive declaration. Time to dwell into more types.

### Object

There are many ways to declare the type for an object.

```js
// Object
// 1. object type (Not recommended)
// can be used to type anything except number, string, boolean, symbol, null, or undefined.
let someObj: object
someObj = {
  someNo: 123,
  someString: 'hi there!',
  sayHi: () => {
    console.log('Hi')
  },
}
// valid (these can lead to bugs, that is exactly why this approach is not recommended)
someObj = []
someObj = () => {
  console.log('another function')
}
// invalid
someObj = 2354
// 2. Adhoc object declaration: An actual object like structure describing properties and methods
let anotherObject: { someNo: number, someString: string, sayHi: () => void } = {
  someNo: 345,
  someString: 'hi',
  sayHi: () => {
    console.log('hi')
  },
}
// invalid
anotherObject = []
anotherObject = () => {
  console.log('this is also invalid')
}
anotherObject.somethingNotInType = 'Invalid, because the property is not in type'
anotherObject.someNo = 'Invalid, someNo is of type number'
```

We will learn more ways to type an object in the next sections.

### Function

There are many ways to declare (type) a function as well.

```js
// Function
// 1. Function type (doesn't care about args and return types)
let someTypedFunction: Function = () => {
  console.log('Any function could have been assigned to this variable')
}
someTypedFunction = (a: number, b: number) => {
  const sum: number = a + b
  return sum
}
// valid, because the type doesn't care about the args and return types.
someTypedFunction()
// invalid
someTypedFunction = 3545
// 2. Explicit (Adhoc) function type declaration
// Here, we declare the arguments inside the function declaration parenthesis
// Name of the arguments in the declaration and in the types does not have to match
// Return type is declared after the fat arrow (=>)
// eg: function below takes two argument, both of type number
// Returns a number
// You can only assign a function which matches this signature
let someAnotherTypeFunction: (arg1: number, arg2: number) => number = (a, b) => {
  return a + b
}
// valid
someAnotherTypeFunction(44, 22)
// invalid
someAnotherTypeFunction(34, '345')
const returnedValue: string = someAnotherTypeFunction(345, 346)
someAnotherTypeFunction = () => {
  console.log('Invalid, this does not match the type declaration')
}
// valid
// You can always use less parameters then decalared
someAnotherTypeFunction = () => {
  return 3545
}
// Invalid
// You cannot use more parameters than declared in the type
someAnotherTypeFunction = (a, b, c) => {
  return a + b + c
}
// valid
someAnotherTypeFunction = (nameDoesNotMatter1, nameDoesNotMatter2) => {
  return nameDoesNotMatter1 * nameDoesNotMatter1
}
```

### Class

Class is a new feature in javascript. To understand the concept of Classes well it requires the understanding of Object-Oriented programming. For now, let's see a simple class declaration.

```js
// Class
class Person {
  // property type declaration
  name: string
  age: number = 0
  // just like a simple function declaration right?
  // But it implicitly returns the instance of the class -- type of class
  // the Person in this case
  constructor(name: string, age: number) {
    // valid
    this.name = name
    this.age = age
    // invalid, the property type is not declared
    this.wow = 'wow!'
  }
  // just like a normal function again
  setAge: (age: number) => void = (age) => {
    this.age = age
  }
  sayHi() {
    console.log(`Hi, ${this.name}`)
  }
}
// user2 is a type of Person
let user2: Person = new Person('User 2', 34)
// user1 is also of type Person, implicitly set by the compiler
let user1 = new Person('User 1', 35)
// invalid
user1 = 'invalid, users type is Person'
```

Class is a fairly big concept in typescript. I would recommend you to check out the documentation for classes in typescript official documentation.

#### Type assertions

There are times when you will run into scenarios, such as some declaration of typeA needs to be used with some different declaration of typeB.

```js
// Type assertions (also referd as typecasting sometimes) ---------
const someUnknownType: unknown = 'I am of type unknown';
// inside some block you know that the type of the variable is string
// Now even if you know the type complier is still unaware of this
// so accessing string methods on the variable is still invalid
someUnknownType.toLowerCase();
// Don't worry, You can still assert the type or tell the compiler that I know what I am doing
// type of the varialbe is actually a string
// and then you are allowed to access string methods
(someUnknownType as string).toLowerCase();
// Here is the syntax for typecasting
// 1. as keyword -->  someTypeA as someTypeB
// example
const unknownTypeA: unknown = 354;
const someNumberC: number = unknownTypeA as number;
// 2. angular brackets -->  <someTypeB>someTypeA
// the syntax above changes the type of someTypeA to someTypeB
const unknowTypeB: unknown = [35, 345];
const someArrayType: number[] = <number[]>unknowTypeB;
```

Remember all this casting is only happening on the type and not on the actual value. Let's clear with an example

```js
let someNumberType: number = 34546;
const someUnknownValue: unknown = 'This is unknown';
// vlaue of someUnknownValue is not converted to number, only the type has changed here.
someNumberType = someUnknownValue as number;
console.log('typeof stil returns string -', typeof someNumberType);
```

**This may lead to bugs. This is why assertions are not recommended.**

## Reuse and compose types with Type, Interface, union and Intersection

You know enough typescript by now to get going. But in real application code, you will have many declarations with the same types. Primitive type declarations are easy just one word, very less chance of two mismatching types. But what about the other types, like the functions or the objects? What if you have 100s of objects of the same type? What if you have many functions receiving the same types of callback functions? Do you declare ad-hoc types everywhere? What if your declarations are messed up somehow?
**Don't worry! Typescript has already thought about this. It provides us with the type and interface declarations which can be re-used.**

### Type

Type keyword allows you to create your own types composing other types.

```js
// Type
// simplest types
type JustNumber = number
// Now JustNumber can be used as a type
// anywhere we refer to JustNumber it will refer to a type assigned to it
// number in this example
let someNumberConst: JustNumber = 98798
someNumberConst = 3498
// invalid
someNumberConst = 'Invalid, string cannot be assigned to type of JustNumber'
// type doesn't has to be this simple. Remember the object declarations
// Now the type declaration can be re-used
type SomePerson = {
  name: string,
  age: number,
  favColors: string[],
  sayHi: () => void,
}
const person1: SomePerson = {
  name: 'Person 1',
  age: 45,
  favColors: ['blue', 'pink', 'purple', 'red', 'black', 'white'],
  sayHi: () => console.log('hi'),
}
const person2: SomePerson = {
  name: 'Person 1',
  age: 78,
  favColors: ['blue', 'pink', 'purple', 'red', 'black', 'white'],
  sayHi: () => console.log('hi'),
}
// It is not restricted to only objects. Look at the function declaration below
type BinaryOperatorOnNumber = (a: number, b: number) => number
const add: BinaryOperatorOnNumber = (a, b) => a * b
// argument name does not needs to be exact only the type and sequence matters
const multiply: BinaryOperatorOnNumber = (num1, num2) => num1 * num2
```

### Interface

Just like the Type, interfaces also allows us to create re-usable types. Interfaces are used to define the structure (type) of variables or values.

```js
// Interface
// basic syntax
// interface interfaceName {
// ... properties
// }
interface DifferentPerson {
  name: string;
  age: number;
}
const p3: DifferentPerson = {
  name: 'p3',
  age: 23,
}
// interfaces can be extended
// the new interface will have new properties defined as well as
// properties from the old declarations
interface Teacher extends DifferentPerson {
  teaches: string;
}
// Now Teacher has all of the DifferentPersons fields as well as new fields defined
const t1: Teacher = {
  name: 'Some teacher',
  age: 325,
  teaches: 'typescript',
}
// interface can also be used to define function types
// The earlier sum function declaration can be done with intefaces
interface Sum {
  (a: number, b: number): number;
}
const addNumbers: Sum = (a, b) => a + b
```

And there are some more ways to reuse code

### Union

What if you need to create a type which is one of many already declared. That is where Union types come to help you.

```js
// Union
// syntax --
// typeA | typeB | typeC
// As you can see symbol '|' is used to do an union.
// a string or a number can be assigned to the variable input
let input: string | number = 44
input = 55
input = 'this also valid'
// invalid
input = true
// the types don't need to be so simple
type A = {
  a: string,
  b: string,
}
type B = {
  c: string,
  d: string,
}
// either a value of type A or B can be assigned to the below declaration
type AOrB = A | B
const onlyA: A = {
  a: 'a',
  b: 'b',
}
const onlyB: B = {
  c: 'c',
  d: 'd',
}
let aOrB: AOrB = onlyB
aOrB = onlyA
// Not valid
aOrB = {
  notValid: 'Yes this is not valid',
}
```

### Intersection

Intersection combines multiple types into one single type.

```js
// Intersection
// syntax
// typeA & typeB & typeC
// '&' symbol is used to combine two types which creates a new type
// with all the types of typeA, typeB and typeC combined.
type SomeA = {
  a: string,
}
type SomeB = {
  b: string,
}
// Now only a value having all the fields declared in SomeA
// and SomeB combined can be assigned to following declaration
type SomeTypeAAndB = SomeA & SomeB
const SomeAAndBValue: SomeTypeAAndB = {
  a: 'This comes from the first declaration',
  b: 'This comes from the second declaration',
}
// invalid
const oneMore: SomeTypeAAndB = {
  // invalid
  d: 'd is not defined in any of two types combined',
}
```

### Generics

Generics are used to defines types without associating the declarations to a specific type. `Array<T>` is one of an example of Generics. Here the T denotes a type. Let us implement a type for an array of any of typed type.

```js
// Generics
// As we know arrays are just object with numbered index and a lenght properties defined (simplified for this example)
// We can pass a type T which will be the type of the value on a variable of type CustomArray,
// except lenght, lenght is always number
interface CustomArray<T> {
  [key: number]: T;
  length: number;
}
// We can pass any type to the CustomArray and the passed type will act as the type of the elements on
// the declared array
const b: CustomArray<number> = [5, 3, 246, 76]
const c: CustomArray<string> = ['allowed', 'allowed']
```
