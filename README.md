# Typescript Cheat Sheet
Cheat Sheet for Typescript with the most needed stuff..

# Guides
TypeScript Course for Beginners 2020 - Learn TypeScript from Scratch! (https://www.youtube.com/watch?v=BwuLxPH8IDs)









<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>

# Convert plain js project to typescript
1. npm i -g typescript

2. tsc --init or create tsconfig.json by yourself:
```
{
  "compilerOptions": {
    "noImplicitAny": false,
    "noEmitOnError": true,
    "removeComments": false,
    "sourceMap": true,
    "target": "es5",
    "outDir": "dist"
  },
  "include": [
    "scripts/**/*"
  ]
}
```
- https://learn.microsoft.com/de-de/visualstudio/javascript/compile-typescript-code-npm?view=vs-2022

3. Rename .js files to .ts

4. Add to package.json:
```typescript
"scripts": {
  "build": "tsc --build",
  "clean": "tsc --build --clean"
},
```

5. Run npm run build to veriy that everythin can compile



















<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>

# Dependencies


## express
- https://github.com/CyberT33N/expressjs-cheat-cheat/blob/master/README.md#typescript

<br><br>
<br><br>

## axios
- https://github.com/CyberT33N/axios-cheat-sheet/blob/main/README.md#typescript

<br><br>
<br><br>

## Mongoose
- https://github.com/CyberT33N/mongoose-cheat-sheet/blob/main/README.md#typescript

<br><br>
<br><br>


## MongoDB

<br><br>
<br><br>

### Db
```typescript
import { MongoClient, Db, Collection } from 'mongodb

class MongoUtils {
    // eslint-disable-next-line no-use-before-define
    private static instance: MongoUtils

    private connectionString: string
    private mongoClient: MongoClient

    private dbConn: Db | null
    private collectionConn: Collection | null


    private constructor() {
        this.dbConn = null
        this.collectionConn = null

        this.connectionString = process.env.MONGODB_CONNECTION_STRING
        this.mongoClient = new MongoClient(this.connectionString)
    }

    private async getDbConnection() {
        try {
            const client = await this.mongoClient.connect()
            this.dbConn = client.db(process.env.DB)
        } catch (e) {
            throw new BaseError('Error while try to get MongoDB Connection', e)
        }
    }

   private async getCollectionConn(collectionName: string) {
        const dbConn = await this.getConnection()

        const collectionConn = dbConn.collection(collectionName)
        return collectionConn
    }
}
```
























<br><br>
<br><br>
____________________________________________________________
____________________________________________________________

<br><br>
<br><br>

# Transpiler
<details><summary>Click to expand..</summary>

## tsx


<br><br>
<br><br>

## Top level await example

package.json
```typescript
{
    "type": "module",
    "scripts": {
       "bootstrap": "tsx src/bootstrap.ts"
     }
}
```

<br><br>

tsconfig.json
```typescript
{
  "compilerOptions": {
    "target": "ES2021",
    "module": "ESNext",
    "lib": [
      "dom",
      "dom.iterable",
      "esnext",
      "es2022"
    ],
    "allowJs": true,
   "useUnknownInCatchVariables": true,
    "skipLibCheck": true,
    "allowImportingTsExtensions": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noEmit": true,
    "esModuleInterop": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [
      {
        "name": "next"
      }
    ],
    "baseUrl": ".",
    "paths": {
      "@/*": [
        "./*"
      ]
    }
  },
  "include": [
    "next-env.d.ts",
    "**/*.ts",
    "**/*.tsx",
    ".next/types/**/*.ts"
  ],
  "exclude": [
    "node_modules"
  ]
}
```











<br><br>
<br><br>
<br><br>
<br><br>







## ts-node
- It is more recommended to use tsx

<br><br>
<br><br>

## Top level await example

package.json
```typescript
{
      "type": "module",
       "scripts": {
          "bootstrap": "node --loader ts-node/esm src/bootstrap.ts"
        },
}
```

<br><br>

tsconfig.json
```typescript
{
  "ts-node": {
    "esm": true,
    // Do not forget to `npm i -D tsconfig-paths`
    "require": ["tsconfig-paths/register"],
    // these options are overrides used only by ts-node
    // same as the --compilerOptions flag and the TS_NODE_COMPILER_OPTIONS environment variable
    "compilerOptions": {
      "target": "ES2022",
      "module": "NodeNext",
      "baseUrl": ".",
      "paths": {
        "@/*": ["."]
      }
    }
  },
  "compilerOptions": {
    "target": "ES2021",
    "module": "ESNext",
    "lib": [
      "dom",
      "dom.iterable",
      "esnext",
      "es2022"
    ],
    "allowJs": true,
    "skipLibCheck": true,
    "allowImportingTsExtensions": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noEmit": true,
    "esModuleInterop": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [
      {
        "name": "next"
      }
    ],
    "baseUrl": ".",
    "paths": {
      "@/*": [
        "./*"
      ]
    }
  },
  "include": [
    "next-env.d.ts",
    "**/*.ts",
    "**/*.tsx",
    ".next/types/**/*.ts"
  ],
  "exclude": [
    "node_modules"
  ]
}
```






</details>

























<br><br>
<br><br>
____________________________________________________________
____________________________________________________________

<br><br>
<br><br>

# tsconfig.json (https://www.typescriptlang.org/tsconfig/)
<details><summary>Click to expand..</summary>
    
<br><br>

## Basic Options

<br><br>

### allowImportingTsExtensions (https://www.typescriptlang.org/tsconfig/#allowImportingTsExtensions)
--allowImportingTsExtensions allows TypeScript files to import each other with a TypeScript-specific extension like .ts, .mts, or .tsx.

This flag is only allowed when --noEmit or --emitDeclarationOnly is enabled, since these import paths would not be resolvable at runtime in JavaScript output files. The expectation here is that your resolver (e.g. your bundler, a runtime, or some other tool) is going to make these imports between .ts files work.

```
"allowImportingTsExtensions": true,
```

<br><br>

### target (https://www.typescriptlang.org/tsconfig#target)
```typescript
// Default: ES3
// Allowed: ES3 (default), ES5, ES6/ES2015 (synonymous), ES7/ES2016, ES2017, ES2018, ES2019, ES2020, ESNext
{   "compilerOptions": {"target": "es6"}   }
```


### lib (https://www.typescriptlang.org/tsconfig#lib)
```typescript
// For default lib is disabled and all library components are allowed. If you enabled it then you must specify which exactly you want to allow.
{   "compilerOptions": {"lib": ['dom', 'es6', 'dom.iterable', 'scripthost']}   }
```


### sourceMap (https://www.typescriptlang.org/tsconfig#sourceMap)
```typescript
// Enables the generation of sourcemap files. These files allow debuggers and other tools to display the original TypeScript source code when actually working with the emitted JavaScript files.
{   "compilerOptions": {"sourceMap": true}   }
```


<br />
<br />

#### outDir (https://www.typescriptlang.org/tsconfig#outDir)
```typescript
// Define the output folder of the compiled files - Notice here that folder structure will also be copied not only the files you will compile.
{   "compilerOptions": {"outDir": "./dist"}   }
```


#### rootDir (https://www.typescriptlang.org/tsconfig#rootDir)
```typescript
// Define the input folder of the compiled files. Basicly the same like include
{   "compilerOptions": {"outDir": "./src"}   }
```


<br />
<br />


#### removeComments (https://www.typescriptlang.org/tsconfig#removeComments)
```typescript
// Remove Comments like as example this text here..
{   "compilerOptions": {"removeComments": true}   }
```

<br />
<br />

#### noEmit (https://www.typescriptlang.org/tsconfig#noEmit)
```typescript
// Compile will not create any .js file when noEmit is true. This is usefully when you just want to check the project for errors but do not directly want to convert your .ts files to .js
{   "compilerOptions": {"noEmit": true}   }
```

#### noEmitOnError (https://www.typescriptlang.org/tsconfig#noEmitOnError)
```typescript
/*Do not emit compiler output files like JavaScript source code, source-maps or declarations if any errors were reported.

This defaults to false, making it easier to work with TypeScript in a watch-like environment where you may want to see results of changes to your code in another environment before making sure all errors are resolved.*/
{   "compilerOptions": {"noEmit": true}   }
```

#### downlevelIteration (https://www.typescriptlang.org/tsconfig#downlevelIteration)
```typescript
// Downleveling is TypeScript’s term for transpiling to an older version of JavaScript. This flag is to enable support for a more accurate implementation of how modern JavaScript iterates through new concepts in older JavaScript runtimes.
{   "downlevelIteration": true   }
```


<br />
<br />


#### Include (https://www.typescriptlang.org/tsconfig#include) & Exclude (https://www.typescriptlang.org/tsconfig#exclude)
Exclude will blacklist folder/files from compiling process. Include instead will whitelist them.
<br /><br />
However, notice here that once you use the include element only specified files/folder will get compiled and everything else you did not include there will be not compiled.
```typescript
// node_modules folder should be already ignored for default

{
   "compilerOptions": {},
   "exclude": ['app.ts', 'node_modules'],
   "include": ['services.ts']
}

// exclude any file which ends with .min.js
"exclude": ['*.min.ts']

// exclude any file which ends with .min.js from any folder
"exclude": ['**/*.min.ts']
```




<br />
<br />

## Additional Checks

#### noUnusedLocals (https://www.typescriptlang.org/tsconfig#noUnusedLocals)
```typescript
// check if variables are unused
{   "noUnusedLocals": true   }
```

#### noUnusedParameters (https://www.typescriptlang.org/tsconfig#noUnusedParameters)
```typescript
// check if Parameters are unused
{   "noUnusedParameters": true   }
```

#### noImplicitReturns (https://www.typescriptlang.org/tsconfig#noImplicitReturns)
```typescript
// check if functions always return something
// {   "noImplicitReturns": true   }
function app(num){
  if(num === 13) { return true }
};

```


<br><br>
<br><br>


</details>



























































<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>

# Types
<details><summary>Click to expand..</summary>













<br><br>
<br><br>

## Basic Types
- https://www.typescriptlang.org/docs/handbook/2/everyday-types.html
  

    
<br><br>

## Number
```typescript
const d: number = 3;
```

<br><br>

## String
```typescript
const d: string = 'house';
```

<br><br>

## Boolean
```typescript
const d: boolean = true;
```

<br><br>

## undefined
```typescript
const d: undefined = undefined;
```

<br><br>

## Any
```typescript
// verify if d is any core type (any has no restriction in TS compared to unknown)
const d: any = 'apple';
```

<br><br>

## unknown
```typescript
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

<br><br>

## never
```typescript
function errorMessage(msg: string, code: number): never {
  throw {msg: msg, code: code};
}

errorMessage('no ram', 23);
console.log( 'This log will NEVER come cause errorMessage will throw error and stop the script' );
```

<br><br>

## function
```typescript
function app(){ /*..*/ };

// verify if d is function - method #1
const d: Function = app;

// verify if d is function - method #2
const d: () = app;
```

<br><br>

## Object
```typescript
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

<br><br>

## Array
```typescript
// verify if d is array - method #1
const d: [] = [];

// verify if d is array - method #2
const d: array = [];

// verify that array only contains specific core type
const d: string[] = ['a', 'b'];
```

<br><br>

## Tuple
```typescript
// verify that array only contains specific core type and contains max. 2 elements.
const d: [number, string] = [1, 'b'];
```

<br><br>

## Union
- https://www.typescriptlang.org/docs/handbook/unions-and-intersections.html
```typescript
function padLeft(value: string, padding: string | number) {
  // ...
}
```


<br><br>
<br><br>

## Enum
```typescript
// create const in TS that are later get converted to vanilla JS
enum Role {
    ADMIN = 'cyberjoe', ACCESSCODE = 512, DENYSTATE = false
}

const d = {
  age: 10,
  name: 'Julian',
  role: Role.ADMIN
};
```

<br><br>

## Enum with objects
```typescript
export const PizzaSize = {
    small: { value: 'small', key: 0, size: 25 },
    medium: { value: 'medium', key: 1, size: 35 },
    large: { value: 'large', key: 2, size: 50 },
} as const
```











<br><br>
<br><br>
<br><br>
<br><br>


# Utility Types
- https://www.typescriptlang.org/docs/handbook/utility-types.html

<br><br>

## readonly
- https://www.typescriptlang.org/docs/handbook/utility-types.html#readonlytype
```typesccript
interface Todo {
  title: string;
}
 
const todo: Readonly<Todo> = {
  title: "Delete inactive users",
};
 
```









<br><br>
<br><br>
<br><br>
<br><br>

## Return Types

<br><br>

### void
```typescript
const fn = (): void => {
    console.log('test..')
}

fn()
```

</details>







































<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>

# Error

## Try Catch
- In Typescript the catched error can only be any or unknown. Because you should never use any the only type you can use is `unknown`

[METHOD #1] Define new error variable and cast interface
```
import axios, { AxiosError } from 'axios'

try {
    await axios.get(`${BASE_URL}/base-error?error=true`)
    throw new Error('Base Error Test - This should not be called')
} catch (e: unknown) {
    const { response } = e as AxiosError
    expect(response?.status).to.equal(500)

    expect(response?.data).to.include({
        title: errorTitle,
        environment: process.env.npm_lifecycle_event,
        name: 'BaseError',
        error: `Error: ${errorMessage}`
    })
}
```


[METHOD #2] Check for instance
```typescript
import axios, {AxiosError} from "axios";

try {
  some request
} catch(err) {
 if (err instanceof AxiosError) {
   console.log(error.response);
   if(error.response?.data?.statusCode === 401) {
     logout();
   } 
 } else {
   // it was some other kind of error, handle it appropriately
 } 

```


















<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>


# Abstract Classes
- https://www.tutorialsteacher.com/typescript/abstract-class
- You can not create a new instance of it
- You can create abstract methods only for type declaration
  - abstract methods must then be defined as method in the class which extends from it
  - In the abstratc class you can create normal methods you can call in the class which extends from it
- Usefully when you want to extend multiple class with the abstract class
```typescript
abstract class StreetFighter {
  constructor() {}

  move() {}
  fight() {
    console.log(`${this.name} attack with ${this.getSpecialAttack()}`);
  }

  abstract getSpecialAttack(): string;
  abstract get name(): string;
}

class Ryu extends StreetFighter {
  getSpecialAttack(): string {
    return "Hadoken";
  }
  get name(): string {
    return "Ryu"
  }
}

class ChunLi extends StreetFighter {
  getSpecialAttack(): string {
    return "Lighting Kick";
  }
  get name(): string {
    return "Chun-Li";
  }
}

const ryu = new Ryu();
const chunLi = new ChunLi();

ryu.fight();
chunLi.fight();
```

## Example #2
```typescript
abstract class Person {
    name: string;
    
    constructor(name: string) {
        this.name = name;
    }

    display(): void{
        console.log(this.name);
    }

    abstract find(string): Person;
}

class Employee extends Person { 
    empCode: number;
    
    constructor(name: string, code: number) { 
        super(name); // must call super()
        this.empCode = code;
    }

    find(name:string): Person { 
        // execute AJAX request to find an employee from a db
        return new Employee(name, 1);
    }
}

let emp: Person = new Employee("James", 100);
emp.display(); //James

let emp2: Person = emp.find('Steve');
```














<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>



# Classes
- https://www.typescriptlang.org/docs/handbook/2/classes.html#handbook-content
```typescript
// ==== INTERFACES ====
export interface BaseErrorInterface {
     name: string
     httpStatus: number
     readonly title: string
     readonly e?: Error | null
}

/**
 * Base Error - Default HTTP Status 500
 */
class BaseError extends Error implements BaseErrorInterface {
    httpStatus: number

    constructor(
        readonly title: string,
        readonly e?: Error | null
    ) {
        super(title)
 
        this.name = 'BaseError'
        this.httpStatus = 500
    }
}

export default BaseError
```
- When you define e.g. `public title: string` in your constructor argument it will be synthetic sugar and will do the same as:
  ```typescript
    constructor(
        title: string,
    ) {
        this.title = title
    }
  ```


<br><br>

## Heritage
```typescript
interface Pingable {
  ping(): void;
}
 
class Sonar implements Pingable {
  ping() {
    console.log("ping!");
  }
}
 
```



<br><br>
<br><br>

# Getters & Setters
```typescript
class Thing {
  _size = 0;
 
  get size(): number {
    return this._size;
  }
 
  set size(value: string | number | boolean) {
    let num = Number(value);
 
    // Don't allow NaN, Infinity, etc
 
    if (!Number.isFinite(num)) {
      this._size = 0;
      return;
    }
 
    this._size = num;
  }
}
```





































<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>

# import/export



<br><br>
<br><br>

## Re-export
```typescript
export { BaseErrorInterface } from './BaseError'

# or
export type { BaseErrorInterface } from './BaseError'

```

### Re-export and usage in same file
```typescript
import type { BaseErrorInterface } from './BaseError.d'
export type { BaseErrorInterface }
```


<br><br>
<br><br>

## Single export
- If needed you can create a single file to export your type or interface

a.ts
```typescript
export interface NewPairs {
   address: string,
   created: Date
}
```

b.ts
```typescript
import { NewPairs } from 'test/a'
let FIXT_NewPairs: NewPairs

# You can also rename it by using
import { NewPairs as NewPairsInterface } from 'test/a'
```




<br><br>
<br><br>

## Multiple export
- If needed you can export your interface along with other javascript exports

a.ts
```typescript
export interface NewPairs {
   address: string,
   created: Date
}

const obj = {
    test: true
}

export { obj }
```

b.ts
```typescript
import { NewPairs } from 'test/a'
let FIXT_NewPairs: NewPairs

# You can also rename it by using
import { NewPairs as NewPairsInterface } from 'test/a'
```




























<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>




# Differences Between `interface` and `type`

## Extensibility:

- **Interfaces** can be extended using the `extends` keyword.
- **Type aliases** can be extended using intersection types.

## Declaration Merging:

- **Interfaces** can merge declarations. If you define an interface with the same name multiple times, TypeScript will merge them into a single interface.
- **Type aliases** do not support declaration merging.

## Use Cases:

- **Interfaces** are typically used to define the shape of objects and are often preferred when defining APIs and classes.
- **Type aliases** are more versatile and can be used for complex type definitions, unions, and intersections.







<br><br>
<br><br>





# Interface
- An interface is used to define a structure for an object. Interfaces can describe the properties and methods that an object should have. They are useful for defining contracts within your code and can be extended or implemented by classes.
```typescript
interface User {
  name: string;
  age: number;
  greet(): string;
}

const user: User = {
  name: "Alice",
  age: 30,
  greet() {
    return `Hello, my name is ${this.name}`;
  }
};
```



<br><br>
<br><br>


## Extend Interface
```typescript
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}

const myDog: Dog = { name: "Buddy", breed: "Golden Retriever" };
```



<br><br>
<br><br>


## Use single property of interface
```typescript
interface ErrorDataInterface extends BaseErrorInterface {
    data?: object
}

const test: ErrorDataInterface['data'] = { test: true };
```





<br><br>
<br><br>


## Overwrite specific property in interface
- https://stackoverflow.com/questions/49198713/override-the-properties-of-an-interface-in-typescript
```typescript
// original interface
interface A {
  a: number;
  b: number; // we want string type instead of number
  c: number;
}

// Remove 'b'
type BTemp = Omit<A, 'b' | 'c'>;

// extends A (BTemp) and redefine b
interface B extends BTemp {
  b: string;
  c: boolean;
}

const a: B = {
  a: 5,
  b: 'B'
}
```































<br><br>
<br><br>
<br><br>
<br><br>

# Type
```typescript
type Point = {
  x: number;
  y: number;
};

type Response = string | number | boolean;

const point: Point = { x: 10, y: 20 };
const response: Response = "Success";
```

<br><br>
<br><br<


## Extending a Type Alia
```typescript
type Animal = {
  name: string;
};

type Dog = Animal & {
  breed: string;
};

const myDog: Dog = { name: "Buddy", breed: "Golden Retriever" };
```


















<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>


# Casting

## as
```typescript
let x: unknown = 'hello';
console.log((x as string).length);
```

<br><br>


## <>
```typescript
let x: unknown = 'hello';
console.log((<string>x).length);
```


























<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>

# Generis
- https://www.typescriptlang.org/docs/handbook/2/generics.html#handbook-content
```typescript
function identity<Type>(arg: Type): Type {
  return arg;
}
```
- Will use the argument type and set it aswell as return type. `<Type>` will lock the type and then re-use it that the function is not allowed to work with other types

























<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>

# Comments

<br><br>

## Ignore
```typescript
// @ts-ignore
import ErrorManager from 'ErrorManager'
```

































<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>


# Postfix

## ! (Tell typescript that unknown element will exist in the future)
```typescript
const button = document.querySelector('#header')!;
```

### Classes example
- In this example BalanceManager will be extended from a parent class which will assign this.web3
```typescript
export default class BalanceManager  {
    web3!: Web3

    async getBalance(address: string) {
        const balance = await this.web3.eth.getBalance(address)
        return balance
    }
}
```































<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>

# Check

# Union Types
```typescript
// Check if element has multiple core types
function combine(a: number | string, b: number){ /*..*/ }
combine('Apple', 2);
```



























<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>

# Literal Types
```typescript
// Check if element has specific value
function combine(a: 'Apple' | 'Fish', b: number){ /*..*/ }
combine('Apple', 2);
```



















<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>

# process.env
- https://stackoverflow.com/questions/45194598/using-process-env-in-typescript
  
```shell
npm i --save-dev @types/node
```
  
- Create at your root environment.d.ts
```typescript
export declare global {
    namespace NodeJS {
        interface ProcessEnv {
            [key: string]: string;
        }
    }
}
```














<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>


# d.ts files
- Only for type declaration
- Exported typed are global available in your project
- **In normales cases you write your type definitions in your .ts files. In most cases d.ts files are only used to provide types for the libraries that dont have typescript support or are automatically genered and shipped with the library to provide the typescript support to it**
   - E.g. `tsc example.ts --decleration`
   - This means you can declare your types in your .ts files and then when transpile it the d.ts files will be generated 

















<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>

# Global
- Create at your root global.d.ts
```
interface Window {
    ethereum: any
    VANTA: any
    vantaSession: any
}
```
- Make sure the tsconfig.json has proper sections for include and exclude. Example follows:
    ```typescript
    "include": [
        "src/**/*.ts",
      ],
      "exclude": [
        "node_modules",
        "<node_internals>/**",
        "bin/**"
      ]
    ```














<br><br>
<br><br>

____________________________________________________________
____________________________________________________________

<br><br>

# Type Aliases
```typescript
// create const of specific uniony types
type adminRights = number | 'FOUND'
const d: adminRights = 'FOUND';
```

## Function
```
type Props = {
     params: {
           productId: string
     }
}

/**
 * Renders the page for a specific product ID.
 * @param {Object} props - The component props.
 * @param {Object} props.params - The parameters object containing the product ID.
 * @param {string} props.params.productId - The product ID.
 * @returns {JSX.Element} The rendered page.
 */
export default function ProductsId({ params }: Props) {
    return (
        <>
            <h1>Product Id: { params.productId }</h1>
        </>
    )
}
```









<br><br>
<br><br>

____________________________________________________________
____________________________________________________________

<br><br>
<br><br>

# Function return types and voids
```typescript
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





<br><br>
<br><br>

____________________________________________________________
____________________________________________________________

<br><br>
<br><br>

# Function Types

## Check if element is function with no parameter and check the core type of the return
```typescript
function app(){ return 13 };
const d: () => number = app;
```

## Check if element is function with two parameter
```typescript
function app(name, age){ /*.. no return here .. Thats why we use void in this case!*/ };
const d: (a: number, b: boolean) => void = app;
```

## Callbacks
```typescript
function doHomework(age: number, callback: (a:number) => void) {
  callback(++age);
}

doHomework(21, () = >{
  console.log('Function doHomework() was finished..');
});
```







<br><br>
<br><br>

____________________________________________________________
____________________________________________________________

<br><br>
<br><br>

# Compiling

## Convert single .ts file to .js
```bash
tsc app.ts
```

## Convert all .ts files in folder to .js
```bash
tsc
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

# Enable Watch Node for all files in the folder (recursive)
tsc -w
```




