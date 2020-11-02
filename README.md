# Typescript Cheat Sheet
Cheat Sheet for Typescript with the most needed stuff..

# Guides
TypeScript Course for Beginners 2020 - Learn TypeScript from Scratch! (https://www.youtube.com/watch?v=BwuLxPH8IDs)



<br />
<br />

____________________________________________________________
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

## undefined
```javascript
const d: undefined = undefined;
```






<br />
<br />

## Any
```javascript
// verify if d is any core type (any has no restriction in TS compared to unknown)
const d: any = 'apple';
```
## unknown
```javascript
// https://youtu.be/BwuLxPH8IDs?t=7883
let userInput: unknown;
let userName: string;

// If userInput would be a number instead of 'Max' and userName would not be inside of the if State then we would get a TS error because userName must be string. Please check 'TS Error' example below. TS will detect if states!
userInput = 'Max';
if(typeof userInput === 'string') {
   userName = userInput
}

// TS Error
userInput = 3;
userName = userInput
```


<br />
<br />



## never
```javascript
function errorMessage(msg: string, code: number): never {
  throw {msg: msg, code: code};
}

errorMessage('no ram', 23);
console.log( 'This log will NEVER come cause errorMessage will throw error and stop the script' );
```


<br />
<br />


## function
```javascript
function app(){ /*..*/ };

// verify if d is function - method #1
const d: Function = app;

// verify if d is function - method #2
const d: () = app;
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


<br />
<br />

____________________________________________________________
____________________________________________________________

<br />
<br />

# Union Types
```javascript
// Check if element has multiple core types
function combine(a: number | string, b: number){ /*..*/ }
combine('Apple', 2);
```



<br />
<br />

____________________________________________________________
____________________________________________________________

<br />
<br />

# Literal Types
```javascript
// Check if element has specific value
function combine(a: 'Apple' | 'Fish', b: number){ /*..*/ }
combine('Apple', 2);
```




<br />
<br />

____________________________________________________________
____________________________________________________________

<br />
<br />

# Type Aliases
```javascript
// create const of specific uniony types
type adminRights = number | 'FOUND'
const d: adminRights = 'FOUND';
```



<br />
<br />

____________________________________________________________
____________________________________________________________

<br />
<br />

# Function return types and voids
```javascript
// check if returned value is specific core type
function combine(a: 'Apple' | 'Fish', b: number): boolean{
  if( b === 1 ) return true;
};
combine('Apple', 2);

// check if there is any return in function
function combine(a: 'Apple' | 'Fish', b: number): void{
  console.log( 'We do not return here..' );
};
combine('Apple', 2);
```

<br />
<br />

____________________________________________________________
____________________________________________________________

<br />
<br />

# Function Types

## Check if element is function with no parameter and check the core type of the return
```javascript
function app(){ return 13 };
const d: () => number = app;
```

## Check if element is function with two parameter
```javascript
function app(name, age){ /*.. no return here .. Thats why we use void in this case!*/ };
const d: (a: number, b: boolean) => void = app;
```

## Callbacks
```javascript
function doHomework(age: number, callback: (a:number) => void) {
  callback(++age);
}

doHomework(21, () = >{
  console.log('Function doHomework() was finished..');
});
```



<br />
<br />

____________________________________________________________
____________________________________________________________

<br />
<br />

# Compiling

## Convert single .ts file to .js
```bash
tsc app.ts
```

<br />
<br />


## Watch Node (Automatically convert .ts file to .js when .ts was edited and saved)

#### single file
```bash
# Method #1
tsc app.ts --watch

# Method #2
tsc app.ts -w
```

#### all files in project
```bash
# This will use all .ts files in the root folder (recursive) where the command was run
tsc --init

# You could run now aswell the tsc command to compile all .ts files to .js or as usually manually edit and save the .ts files
```
