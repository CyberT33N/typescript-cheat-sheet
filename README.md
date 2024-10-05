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

# Operator

## typeof
- https://www.typescriptlang.org/docs/handbook/2/typeof-types.html
```typescript
let s = "hello";
let n: typeof s;
```

## keyof
- https://www.typescriptlang.org/docs/handbook/2/keyof-types.html
- The keyof operator takes an object type and produces a string or numeric literal union of its keys. The following type P is the same type as type P = "x" | "y":
```typescript
type Point = { x: number; y: number };
type P = keyof Point;
```





















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

# Compile

<br><br>

## Compile in Runtime
```typescript
// Kompiliere .ts Datei zur Laufzeit zu .js (CJS)
const compiledPath = tsFilePath.replace(/\.ts$/, '.cjs')
const compiledDir = path.dirname(compiledPath)
console.log('Compiled path:', compiledPath)
console.log('Compiled dir:', compiledDir)
execSync(`tsup ${tsFilePath} --outDir ${compiledDir}`)
```



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





<br><br>
<br><br>

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
<details><summary>Click to expand..</summary>
  
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


## Merge Interfaces
```typescript
interface IFooBar extends IFoo, IBar {}
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


## Merge interfaces and pick conflicting properties
- Sometimes you want to merge interfaces which have the same properties but with different values e.g. like default values
```typescript
export interface BaseErrorMiddlewareInterface extends Pick<BaseErrorInterface, 'httpStatus' | 'name'>,
    Omit<ErrorResponseInterface, 'httpStatus' | 'name'> {}
```






<br><br>
<br><br>


## Get key of type
```typescript
interface Accessor {
    key<K extends keyof Config>(k: K): Config[typeof k];
}

```








</details>

































<br><br>
<br><br>
<br><br>
<br><br>

# Type

<details><summary>Click to expand..</summary>
  
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
<br><br>


## Dynamic generate Type

<br><br>


### Auto generate type
```typescript
type MapSchemaTypes = {
  string: string;
  integer: number;
  // others?
}

type MapSchema<T extends Record<string, keyof MapSchemaTypes>> = {
  -readonly [K in keyof T]: MapSchemaTypes[T[K]]
}

const personSchema = { name: 'string', age: 'integer' } as const;
type Person = MapSchema<typeof personSchema>;
```

<br><br>


### Type is defined in object
```typescript
const schema = {
    name: { 
        type: String,
        required: true,
        unique: true,
        index: true
    },
    decimals: { type: BigInt, required: true }
}

type MongooseSchemaInterface = {
    [K in keyof typeof schema]: MongooseSchemaType<typeof schema[K]['type']>;
};

const test: MongooseSchemaInterface = {
    name: 123 // <-- Will not work
}
```

<br><br>
<br><br>


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

# Function Types

<br><br>

## Check if element is function with no parameter and check the core type of the return
```typescript
function app(){
    return 13
};

const d: () => number = app;
```

<br><br>

## Check if element is function with two parameter
```typescript
function app(name, age){
    /*.. no return here .. Thats why we use void in this case!*/
};

const d: (a: number, b: boolean) => void = app;
```

<br><br>

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
<br><br>

## Conditional Types
- https://www.typescriptlang.org/docs/handbook/2/conditional-types.html
```typescript
interface Animal {
  live(): void;
}
interface Dog extends Animal {
  woof(): void;
}
 
type Example1 = Dog extends Animal ? number : string;
        
type Example1 = number
 
type Example2 = RegExp extends Animal ? number : string;
```





<br><br>
<br><br>

## infer
- Conditional types provide us with a way to infer from types we compare against in the true branch using the infer keyword. For example, we could have inferred the element type in Flatten instead of fetching it out “manually” with an indexed access type:
```typescript
# Example #1
type Flatten<Type> = Type extends Array<infer Item> ? Item : Type;

# Example #2
type SchemaValue<T> = T extends { type: infer U } ? MongooseSchemaType<U> : MongooseSchemaType<T>;
```
- So basiclly we detect the type of a value and then re-use it inside of our extends conditon. **You can only use infer with extends**























<br><br>
<br><br>
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
- 
<br><br>
<br><br>

## Pick
- https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys
```typescript
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}
 
type TodoPreview = Pick<Todo, "title" | "completed">;
 
const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
};
```


<br><br>
<br><br>



## Omit
- https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys
```typescript
interface Todo {
  title: string;
  description: string;
  completed: boolean;
  createdAt: number;
}
 
type TodoPreview = Omit<Todo, "description">;
 
const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
  createdAt: 1615544252770,
};
 
```


<br><br>
<br><br>


## Record
- https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeys-type
- Constructs an object type whose property keys are Keys and whose property values are Type. This utility can be used to map the properties of a type to another type.
```typescript
type CatName = "miffy" | "boris" | "mordred";
 
interface CatInfo {
  age: number;
  breed: string;
}
 
const cats: Record<CatName, CatInfo> = {
  miffy: { age: 10, breed: "Persian" },
  boris: { age: 5, breed: "Maine Coon" },
  mordred: { age: 16, breed: "British Shorthair" },
};
 
cats.boris;
```

### Allows object with any nested typed
- If you would use this interface then you could not use `const res: NestedData = test.data.nestedObject` because object does not allows nested properties:
```typescript
interface NestedData {
  data: object;
}
```
  - For thise case you must use Record
  ```typescript
  interface NestedData {
    data: Record<string, any>;
  }
  ```



<br><br>
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

<br><br>

## Try Catch
- In Typescript the catched error can only be any or unknown. Because you should never use any the only type you can use is `unknown`

<br><br>

[METHOD #2 RECOMMENDED] Check for instance
```typescript
it('should throw an error when initializing connection with mongoose fails', async () => {
    try {
        await Object.getPrototypeOf(mongooseUtils).init()
        assert.fail('This line should not be reached')
    } catch (err) {
        if (err instanceof BaseError) {
            const typedErr: IBaseError = err 
            expectTypeOf(typedErr).toEqualTypeOf<IBaseError>()

            expect(typedErr.error?.message).toBe(expectedErrorMessage)
            expect(typedErr.message).toBe(
                '[ModelManager] - Error while initializing connection with MongoDB'
            )

            return
        }

        assert.fail('This line should not be reached')
    }
})
```
- Update: TypeScript 4.4 provides a config flag --useUnknownInCatchVariables to let catch-variables default to type unknown. This is also automatically enabled with the --strict flag.


<br><br>
<br><br>


[METHOD #2] Define new error variable and cast interface
- **If you write integration tests you can use casting with as. However, with unit tests this is not recommended because you overwrite the actually types and you are not able anymore to make type checks**
```typescript
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
























<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>



# Functions

<br><br>

## Assign Interface to Arguments
```typescript
// Option #1
function createPerson(person: Person) { /* ... */ }

// Option #1
function createPerson({name, age}: Person) { /* ... */ }
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
- **When you create a class then Typescript will autmatically creae a type that you can re-use your class in another file as class and as type. However, this will only work for the class defined types and for the extended classes. It will not implement your Interface types even whn you use `immplements`. This means if needed you need to export the interface aswell if it is maybe different to the class itself**
  - **When to Use a Class as a Type?** If you only need the functionality of your standalone class and it will not be extended by other classes and its types without any further implementations or structures, it is perfectly fine to use the class itself as a type. This saves you additional boilerplate code. However, if not you should create a own interface




- When you define e.g. `public title: string` in your constructor argument it will be synthetic sugar and will do the same as:
  ```typescript
    constructor(
        title: string,
    ) {
        this.title = title
    }
  ```












<br><br>
<br><br>




## Abstract Classes
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

## dynamic import
- You can only do:
```typescript
import { type IApple } from './Apple.ts'
```

but not:
```typescript
const { type IApple } = await import('./Apple.ts')
```


<br><br>
<br><br>

## Re-export
```typescript
# Method #1
export type { BaseErrorInterface } from './BaseError'

# Method #2
export {
    AnyOtherCLass
    default as BaseError,
    type BaseErrorInterface
} from './BaseError'

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

# Generics
- https://www.typescriptlang.org/docs/handbook/2/generics.html#handbook-content
```typescript
function identity<Type>(arg: Type): Type {
  return arg;
}
```
- Will use the argument type and set it aswell as return type. `<Type>` will lock the type and then re-use it that the function is not allowed to work with other types


<br><br>
<br><br>

## Generic types
```typescript
type ApiResponse<T> = {
  data: T
  isError: boolean
}

type UserResponse = ApiResponse<{ name: string; age:number }>

const response: UserResponse = {
  data: {
    name: 'dennis',
    age: 12
  },
  isError: true
}
```



<br><br>
<br><br>

## Setting default
- If you define a default in your type then there is no need to define the argumentm in the generic.
```typescript
type ApiResponse<T = { name: 'default' }> = {
  data: T
  isError: boolean
}

const response: ApiResponse = {
  data: {
    name: 'dennis'
  },
  isError: true
}
```




<br><br>
<br><br>

## Passing object to generic
- Using typeof allows us to pass an object or other data types (https://www.typescriptlang.org/docs/handbook/2/typeof-types.html)
```typescript
 type MongooseSchemaInterface<Schema> = {
     [K in keyof Schema]: SchemaValue<Schema[K]>
 }

const schema = {
    // ==== GENERAL ====
    name: { 
        type: Number,
        required: true,
        unique: true,
        index: true
    },
    avatar: {
        type: [String],
        default: []
    },
    decimals: { type: BigInt, required: true }
}

const userSchema = new mongoose.Schema<MongooseSchemaInterface<typeof schema>>(schema)
```




<br><br>
<br><br>

## Extend

<br><br>

### Extend from specific type
- Extending will say that the generic will be always from this type
```typescript
// You can also use default here if you want e<T extends object = { name: 'default' }>
type ApiResponse<T extends object> = {
  data: T
  isError: boolean
}

type UserResponse = ApiResponse<{ name: string; age:number }>

const response: UserResponse = {
  data: {
    name: 'dennis'
  },
  isError: true
}
```





<br><br>

### Extend with condition
```typescript
type MongooseSchemaType<T> = 
    T extends typeof String ? mongoose.Schema.Types.String :
    T extends typeof Number ? mongoose.Schema.Types.Number :
    T extends typeof Boolean ? mongoose.Schema.Types.Boolean :
    never;
```
- It will check if `T` is typeof something and extend from your given values or go to he next condition
























<br><br>
<br><br>
____________________________________________________________
____________________________________________________________
<br><br>
<br><br>

# Tests

<br><br>

## Test private Methods 

<br><br>


### Example #1
- Get Prototype
- **Notice that you will create a new object here which does not include properties from your created instance**
```typescript
class Example {
    private privateMethod() {}
    public test() {}
}

describe() {
    it('test', () => {
        const example = new Example();
        const exampleProto = Object.getPrototypeOf(example);

        exampleProto.privateMethod();
    })
}
```

<br><br>


### Example #2
- Type cast
```typescript
describe('getConnection', () => {
  it.only('should return a valid mongoose connection', async() => {
      const conn = await (<any>mongooseUtils).getConnection()
  
      expect(conn).toBeTruthy()
      expect(conn).toBeInstanceOf(mongoose.Connection)
  })
})

describe('getInstance()', () => {
        let initStub: sinon.SinonStub

        beforeEach(() => {
            initStub = sinon.stub((<any>ModelManager).prototype, 'init').resolves()
        })

        afterEach(() => {
            initStub.restore()
        })

        it.only('should create new instance', async() => {
            const modelManager = await ModelManager.getInstance()

            expect(initStub.calledOnce).toBe(true)
            expect(modelManager.models).toEqual([])
        })
    })
```

<br><br>

### Example #3
- Casting
```typescript
beforeEach(() => {
    initStub = sinon.stub(ModelManager.prototype, 'init' as keyof ModelManager).resolves()
})
```


<br><br>
<br><br>

### Example #4 - Reflect

<br><br>

#### Get Property
```typescript
 it.only('should create new instance', async() => {
    const mongooseUtils = await MongooseUtils.getInstance()

    expect(initStub.calledOnce).toBe(true)
    expect(Reflect.get(mongooseUtils, 'connectionString')).toBe(process.env.MONGODB_CONNECTION_STRING)
})
```

<br><br>

#### Call private method
```typescript
const initMethod: Function = Reflect.get(modelManager, 'init');
await initMethod.call(modelManager);               
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


































