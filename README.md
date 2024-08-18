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
```javascript
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

# Core Types

<br><br>

## Number
```javascript
const d: number = 3;
```

<br><br>

## String
```javascript
const d: string = 'house';
```

<br><br>

## Boolean
```javascript
const d: boolean = true;
```

<br><br>

## undefined
```javascript
const d: undefined = undefined;
```



<br><br>

## Any
```javascript
// verify if d is any core type (any has no restriction in TS compared to unknown)
const d: any = 'apple';
```

<br><br>

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


<br><br>


## never
```javascript
function errorMessage(msg: string, code: number): never {
  throw {msg: msg, code: code};
}

errorMessage('no ram', 23);
console.log( 'This log will NEVER come cause errorMessage will throw error and stop the script' );
```


<br><br>

## function
```javascript
function app(){ /*..*/ };

// verify if d is function - method #1
const d: Function = app;

// verify if d is function - method #2
const d: () = app;
```

<br><br>

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

<br><br>

## Array
```javascript
// verify if d is array - method #1
const d: [] = [];

// verify if d is array - method #2
const d: array = [];

// verify that array only contains specific core type
const d: string[] = ['a', 'b'];
```

<br><br>

## Tuple
```javascript
// verify that array only contains specific core type and contains max. 2 elements.
const d: [number, string] = [1, 'b'];
```

<br><br>

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






















<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>

# import/export

<br><br>
<br><br>

## Single file

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

# Dependencies






<br><br>
<br><br>
<br><br>
<br><br>


## Mongoose
- https://github.com/CyberT33N/mongoose-cheat-sheet/blob/main/README.md#typescript



<br><br>
<br><br>
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


# Postfix

## ! (Tell typescript that unknown element will exist in the future)
```javascript
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
```javascript
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
```javascript
// Check if element has specific value
function combine(a: 'Apple' | 'Fish', b: number){ /*..*/ }
combine('Apple', 2);
```



















<br>
<br>
____________________________________________________________
____________________________________________________________
<br>
<br>

# process.env
- https://stackoverflow.com/questions/45194598/using-process-env-in-typescript
  
```shell
npm i --save-dev @types/node
```
  
- Create at your root environment.d.ts
```javascript
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




<br />
<br />

____________________________________________________________
____________________________________________________________

<br />
<br />

# tsconfig.json (https://www.typescriptlang.org/tsconfig/)

## Basic Options

#### target (https://www.typescriptlang.org/tsconfig#target)
```javascript
// Default: ES3
// Allowed: ES3 (default), ES5, ES6/ES2015 (synonymous), ES7/ES2016, ES2017, ES2018, ES2019, ES2020, ESNext
{   "compilerOptions": {"target": "es6"}   }
```


#### lib (https://www.typescriptlang.org/tsconfig#lib)
```javascript
// For default lib is disabled and all library components are allowed. If you enabled it then you must specify which exactly you want to allow.
{   "compilerOptions": {"lib": ['dom', 'es6', 'dom.iterable', 'scripthost']}   }
```


#### sourceMap (https://www.typescriptlang.org/tsconfig#sourceMap)
```javascript
// Enables the generation of sourcemap files. These files allow debuggers and other tools to display the original TypeScript source code when actually working with the emitted JavaScript files.
{   "compilerOptions": {"sourceMap": true}   }
```


<br />
<br />

#### outDir (https://www.typescriptlang.org/tsconfig#outDir)
```javascript
// Define the output folder of the compiled files - Notice here that folder structure will also be copied not only the files you will compile.
{   "compilerOptions": {"outDir": "./dist"}   }
```


#### rootDir (https://www.typescriptlang.org/tsconfig#rootDir)
```javascript
// Define the input folder of the compiled files. Basicly the same like include
{   "compilerOptions": {"outDir": "./src"}   }
```


<br />
<br />


#### removeComments (https://www.typescriptlang.org/tsconfig#removeComments)
```javascript
// Remove Comments like as example this text here..
{   "compilerOptions": {"removeComments": true}   }
```

<br />
<br />

#### noEmit (https://www.typescriptlang.org/tsconfig#noEmit)
```javascript
// Compile will not create any .js file when noEmit is true. This is usefully when you just want to check the project for errors but do not directly want to convert your .ts files to .js
{   "compilerOptions": {"noEmit": true}   }
```

#### noEmitOnError (https://www.typescriptlang.org/tsconfig#noEmitOnError)
```javascript
/*Do not emit compiler output files like JavaScript source code, source-maps or declarations if any errors were reported.

This defaults to false, making it easier to work with TypeScript in a watch-like environment where you may want to see results of changes to your code in another environment before making sure all errors are resolved.*/
{   "compilerOptions": {"noEmit": true}   }
```

#### downlevelIteration (https://www.typescriptlang.org/tsconfig#downlevelIteration)
```javascript
// Downleveling is TypeScript’s term for transpiling to an older version of JavaScript. This flag is to enable support for a more accurate implementation of how modern JavaScript iterates through new concepts in older JavaScript runtimes.
{   "downlevelIteration": true   }
```


<br />
<br />


#### Include (https://www.typescriptlang.org/tsconfig#include) & Exclude (https://www.typescriptlang.org/tsconfig#exclude)
Exclude will blacklist folder/files from compiling process. Include instead will whitelist them.
<br /><br />
However, notice here that once you use the include element only specified files/folder will get compiled and everything else you did not include there will be not compiled.
```javascript
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
```javascript
// check if variables are unused
{   "noUnusedLocals": true   }
```

#### noUnusedParameters (https://www.typescriptlang.org/tsconfig#noUnusedParameters)
```javascript
// check if Parameters are unused
{   "noUnusedParameters": true   }
```

#### noImplicitReturns (https://www.typescriptlang.org/tsconfig#noImplicitReturns)
```javascript
// check if functions always return something
// {   "noImplicitReturns": true   }
function app(num){
  if(num === 13) { return true }
};

```


<br />
<br />

