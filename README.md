# Typescript Cheat Sheet
Cheat Sheet for Typescript with the most needed stuff..

# Guides
TypeScript Course for Beginners 2020 - Learn TypeScript from Scratch! (https://www.youtube.com/watch?v=BwuLxPH8IDs)



<br />
<br />

____________________________________________________________

<br />
<br />

# Core Types

## Number
```javascript
const d: number = 3;
```

## String
```javascript
const d: string = 'house';
```

## Boolean
```javascript
const d: boolean = true;
```

## Object
```javascript
// verify if d is object - method #1
const d: {} = {};

// verify if d is object - method #2
const d: object = {};

// verify object elements type
const d: {age: number, name: string} = {
  age: 10,
  name: 'Julian'
};
```

## Array
```javascript
// verify if d is array - method #1
const d: [] = [];

// verify if d is array - method #2
const d: array = [];

// verify that array only contains specific core type
const d: string[] = ['a', 'b'];
```

## Tuple
```javascript
// verify that array only contains specific core type and contains max. 2 elements.
const d: [number, string] = [1, 'b'];
```

## Enum
```javascript
// create const in TS that are later get converted to vanilla JS
enum Role {ADMIN = 'cyberjoe', ACCESSCODE = 512, DENYSTATE = false}
const d = {
  age: 10,
  name: 'Julian',
  role: Role.ADMIN
};
```

## Any
```javascript
// verify if d is anything
const d: any = 'apple';
```


<br />
<br />

____________________________________________________________

<br />
<br />

# Union Types
```javascript
// Check if element has multiple core types
function combine(a: number | string, b: number){
}
combine('Apple', 2);
```
