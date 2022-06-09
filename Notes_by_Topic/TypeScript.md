# TYPESCRIPT

## WHAT IS TYPESCRIPT?

- Superset of JavaScript
  - Takes JS and add on top of it
  - Adds *types* to JS using a set of tools called a *type system*
  - Checks for syntax errors before run time

- Adds *static types* to JS
  - JS, by default, is dynamically typed (undefined, null)
  - With statically typed language, *particular type is assigned* when a variable is created
    - Little to no edge cases
      - i.e. checking for data type for a function argument

- TS has to be compiled and turned into JS
  - No runtime environment like Node

### TYPE INFERENCE

- When a variable is declared with an initial value, it can *never be reassigned* a value of a *different data type*

- All *primitive data types* from JS are recognized by TS
  - string
  - number
  - boolean
  - null
  - undefined

## INSTALLATION

- `npm install -g typescript`
  - Installs TS Compiler (TSC)
    - TS files can be fed into it

## COMPILATION

- `tsc filename.ts`
  - Compiles and turn .ts file into .js file as long as there is no error
    - .js file is created with the same filename

- When compiled, by default:
  - variable declaration using var
  - deletes all empty lines and type declaration

- `tsc filename.ts --target es2016`
  - to use let and const when compiling

### COMPILING BY INITIALIZING TS

- `tsc --init` on *top level* folder
  - Creates `tsconfig.json` file
  - Run `tsc` on any level directory within the project and it will look for tsconfig.json file
    - Uses the configurations and compiles all ts files into js while keeping the folder structures

- `tsc --watch` to run tsc on the background *similar to nodemon*
  - Compiles as ts files change

### tsconfig.json

- Customize what rules you want TS compiler to enforce

- `"allowJs": true` to also allow js files to be compiled and placed in outDir

- `"outDir": "./build"` to specify where compiled js (output) files are saved

- `"rootDir": "./src"` to specify where ts files live

## TYPE ANNOTATION/DECLARATION

- Data type can be assigned when a variable is created
  - TS linter throws an error if a different data type is assigned
  - Default for JS is *any* (all data types)

- *Single pipe (|)* can be used to allow for multiple data types

### PRIMITIVES
```ts
// only string
let username: string = 'Alice';
// both string and number
let username: string | number = 'Alice';

username = 'Bob';
username = 42;  // Type 'number' is not assignable to type 'string'.ts(2322)
username = false; // Type 'boolean' is not assignable to type 'string | number'.ts(2322)
```

### ARRAYS

- Assign type annotation followed by `[]`

- Empty array is compatible with any array type

```ts
// only numbers in array
const numbers: number[] = [1, 2, 3];
// both string and number
const numbers: (string | number)[] = [1, 2, 3];

numbers.push(4);
numbers.push('four'); // Argument of type 'string' is not assignable to parameter of type 'number'.ts(2345)

// empty array
let names: string[] = []; // No type errors.
let numbers: number[] = []; // No type errors.

names.push('Isabella');  
numbers.push(30);
```

#### MULTI-DIMENSIONAL ARRAYS

```ts
let arr: string[][] = [['str1', 'str2'], ['more', 'strings']];

let bestNumbers: number[] = [7,77,4];
let numbersMulti: number[][][] = [ [[1],[2,3]], [[7],bestNumbers] ];
```

#### TUPLES

- When an array is typed with elements of specific types
  - Have fixed length and strict ordering of elements
  - Both lengths and the orders of elements are taken into consideration

```ts
let ourTuple: [string, number, string, boolean] = ['Is', 7 , 'our favorite number?' , false];

let numbersTuple: [number, number, number] = [1,2,3,4]; // Type Error! numbersTuple should only have three elements.

let mixedTuple: [number, string, boolean] = ['hi', 3, true] // Type Error! The first elements should be a number, the second a string, and the third a boolean. 
```

- Tuples and arrays do not have compatible types
  - Cannot assign an array to a tuple variable

```ts
let tup: [string, string] = ['hi', 'bye'];
let arr: string[] = ['there','there'];

tup = ['there', 'there']; // No Errors.
tup = arr; // Type Error! An array cannot be assigned to a tuple.
```

### CUSTOM TYPES

#### NUMERIC ENUMS

- To enumerate (limit) all the possible values that a variable could have
  - Useful for assigning constants

- Enum values, by default, are assigned a numerical value according to their listed order
  - The first value is assigned a number 0 and increments
  - Can be assigned a different value

- Enum type can be used in a type annotation
  - Only allows variables declared in this enum

```ts
enum Direction {
  North,  // 0
  South,  // 1
  East,   // 2
  West    // 3
};

let toHome: Direction = Direction.North;
```

#### STRING ENUMS

- Unlike numeric enums, string enums need strings to be written explicitly
  - Typically, capitalization of variable name

- String enums recommended over numeric, because numeric enum variables can be reassigned

```ts
enum DirectionString {
  North = 'NORTH',
  South = 'SOUTH',
  East = 'EAST',
  West = 'WEST'
};

// numeric enum can be reassigned whereas string enum cannot be
let whichWayToAntarctica: DirectionNumber;
whichWayToAntarctica = 1; // Valid TypeScript code.
whichWayToAntarctica = DirectionNumber.South; // Valid, equivalent to the above line.

let whichWayToAntarctica: DirectionString;
whichWayToAntarctica = '\ (•◡•) / Arbitrary String \ (•◡•) /'; // Type error!
whichWayToAntarctica = 'SOUTH'; // STILL a type error!
whichWayToAntarctica = DirectionString.South; // The only allowable way to do this.
```

#### OBJECTS

- Type annotation for objects looks like an object literal
  - Instead of value after key, type is assigned
  - Both property name and type need to match

- If data types for objects keys are declared, but key-value pairs are not included in the object, TS throws error
  - Property 'age' is missing in type '{ name: string; breed: string; }' but required in type '{ name: string; breed: string; age: number; }'.ts(2741)

- For the other way around:
  - Type '{ name: string; breed: string; age: number; }' is not assignable to type '{ name: string; breed: string; }'.
  Object literal may only specify known properties, and 'age' does not exist in type '{ name: string; breed: string; }'.ts(2322)

```ts
const dog: {
  name: string;
  breed: string;
  age: number;
} = {
  name: 'Bori',
  breed: 'Toy Poodle',
  age: 7,
};
```

#### INTERFACE

- If there are many objects, we would have to do the above for each object

- Solution to this problem is to *create our own new types to TS*
  - When we are typing an object, it is referred to as *interface*
  - All interface starts with a capital letter
  - Use the interface to create objects with the same key-value data types
  - Can be only use to type objects
    - Good to use in object-oriented programs

- To avoid confusion with Classes, name interfaces starting with `I`

- Another issue arises when sending interacting database
  - `id` included when interacting with database
  - Solved by specifying it as optional
    - `?` before colon
    - `id?: number`

```ts
// new type added
interface ITreat {
  name: string;
  tastiness: number;
};

interface IDog {
  id?: number; // optional key-value pair
  name: string;
  breed: string;
  age: number;
  treats: ITreat[]; // nested - array in object
}; 

const dog: IDog = {
  name: 'Bori',
  breed: 'Toy,
    // array allowed for treats
  treats: [
    {
      name: 'kibbles and bits',
      tastiness: 7,
    }
  ]
};

// Dog type accepted in array
const dogs: IDog[] = [];
dogs.push(dog); // array of object created
dogs.push({}); // Argument of type '{}' is not assignable to parameter of type 'Dog'. Type '{}' is missing the following properties from type 'Dog': name, breed, age.ts(2345)
dogs.push(5); // Argument of type 'number' is not assignable to parameter of type 'Dog'.ts(2345)
```

##### INTERFACES WITH CLASSES

- To use interface in class, use `implements` keyword to apply the type from interface to class

```ts
interface Robot {
  about: {
    general: {
      id: number;
      name: string;
    };
  };
  getRobotId: () => string;
}

class OneSeries implements Robot {
  about;
 
  constructor(props: { general: { id: number; name: string; } }) {
    this.about = props;
  }
 
  getRobotId() {
    return `ID: ${this.about.general.id}`;
  }
}
```

##### COMPOSED TYPES/INTERFACES

- For nested interfaces/types, break down into individual types and reference them inside other types

```ts
// written in one interface
interface About {
  general: {
    id: number;
    name: string;
    version: {
      versionNumber: number;
    }
  }
}

// written with composed types
interface About {
  general: General;
}
 
interface General {
  id: number;
  name: string;
  version: Version;
}
 
interface Version {
  versionNumber: number;
}
```

##### EXTENDING INTERFACES

- To copy all the type members from one type into another type
  - Use `extends` keyword

```ts
interface Shape {
  color: string;
}
 
interface Square extends Shape {
  sideLength: number;
}
 
const mySquare: Square = { sideLength: 10, color: 'blue' };
```

##### INDEX SIGNATURES

- When the property names for an object is not known at the compile time, but know what the data will look like in general
  - Ex. Fetching information from an API
  - Include a variable name for the property name

```ts
// what data might look like
{
  'shopping': 150,
  'food': 210,
  'utilities': 100
}

// interface with index signatures
import { getBudgetAsync } from './api';

// Write an interface here
interface Budget {
  [category: string]: number
}

async function getBudget() {
  const result: Budget = await getBudgetAsync();
  console.log(result);
}

getBudget();
```

#### TYPES

- Types are similar to interfaces, but are immutable and cannot be extended
  - Can be used to type objects, primitives and more

```ts
type Person = { name: string, age: number };

let aCompany: {
  companyName: string, 
  boss: Person, 
  employees: Person[], 
  employeeOfTheMonth: Person,  
  moneyEarned: number
};
```

#### GENERIC TYPES

- Generics are ways to create collections of types using `<T>`
  - <T> can be substituted with some type
    - T is a type placeholder


```ts
type Family<T> = {
  parents: [T, T], mate: T, children: T[]
};

let aStringFamily: Family<string> = {
  parents: ['stern string', 'nice string'],
  mate: 'string next door', 
  children: ['stringy', 'stringo', 'stringina', 'stringolio']
}; 
```

### FUNCTIONS

- Interested in *parameters* and *return value*

- If function does not return anything, use `void` as type
  - Same as `undefined` in JS

- For a parameter assigned a default value
  - TS will infer the variable type to be the same as the default value's type
  - `undefined` can also be passed in (i.e. no argument)

- *Explicit* return types
  - What type a function returns
  - Add type annotation after the function's closing ()

- *Void* return type
  - Use void return type for functions that do not return anything

```ts
// after (), specify data type for return value
// also accepts optional argument
// order is important when using optional argument
// putting age? first would throw an error
const sayHello = (name: string, age?: number, treat?: ITreat): string => {
  return `Hello there, ${name}`;
};

// const sayHello = (name: string, age?: number, treat?: ITreat): void => {
//   // return `Hello there, ${name}`;
// };

// sayHello(); // Expected 1 arguments, but got 0.ts(2554)
sayHello('Alice');
// need to include age even if it is optional to include treat as argument
sayHello('Jeffery', 22, { name: 'kibbles and bits', tastiness: 7 })


// to assign type for callback function
const higherOrderFunction = (num: number, callback: (anyNum: number) => string): void => {
  const returnVal = callback(num); // return from callback is a string so the value of returnVal is a string
};

higherOrderFunction(42, (num: number) => { return 'hello' });
```

#### GENERIC FUNCTIONS

```ts
function getFilledArray<T>(value: T, n: number): T[] {
  return Array(n).fill(value);
}

getFilledArray<string>('cheese', 3)
// ['cheese', 'cheese', 'cheese']
```

- Declare type for T when invoking the function
  - Ensures the value and the returned array have the same type T

#### FUNCTIONS DOCUMENTATION

```ts
  /**
   * Returns the sum of two numbers.
   *
   * @param x - The first input number
   * @param y - The second input number
   * @returns The sum of `x` and `y`
   *
   */
  function getSum(x: number, y: number): number {
    return x + y;
  }
```

### UNION TYPES

- Unions allow to define multiple allowed type members
  - Separate each type member with `|`
  - Each type in union is a *type member*

```ts
let ID: string | number;
 
// number
ID = 1;
console.log(`The ID is ${ID}.`); // The ID is 1
 
// or string
ID = '001';
console.log(`The ID is ${ID}.`); // The ID is 001

function getMarginLeft(margin: string | number) {
  return { 'marginLeft': margin };
}
```

- For type members in a union, TS only allows to use the common methods and properties that all members of the union share

```ts
const batteryStatus: boolean | number = false;
 
batteryStatus.toString(); // No TypeScript error since both boolean and number share the .toString() method
batteryStatus.toFixed(2); // TypeScript error
```

#### TYPE NARROWING

- TS understands how the code will execute at runtime so it can infer more specific types while writing code

- *Type narrowing* is when TS can figure out what type a variable can be at a given point in the code

- *Type guard* is a conditional that checks if a variable is a certain type
  - To perform different logic for different types
  - `if...else` can be used as well

```ts
function getMarginLeft(margin: string | number) {
  // margin may be a string or number here
 
  // narrowed the type inside the type guard to only be a string
  if (typeof margin === 'string') {
    // margin must be a string here
    return margin.toLowerCase();
  } else { // if margin is number
    return `${margin}px`;
  }

  margin.toLowerCase(); // error => toLowerCase cannot be used on number type
}
```

##### USING IN OPERATOR WITH TYPE GUARDS

- `in` operator checks if a property exists on an object itself or anywhere within its prototype chain
  - Check if a property exists using conditional

```ts
type Cat = {
  name: string;
  run: () => string;
}

type Fish = {
  name: string;
  swim: () => string;
}

const siameseCat = { 
  name: 'Proxie', 
  run: () => 'pitter pat'
}

const bettaFish = { 
  name: 'Neptune', 
  swim: () => 'bubble blub'
}

function move(pet: Cat | Fish) {
  if ('run' in pet) {
    return pet.run();
  }

  if ('swim' in pet) {
    return pet.swim();
  }
}

console.log(move(siameseCat)) // pitter pat
```


#### LITERAL TYPES

- To create distinct states within a program

```ts
type Color = 'green' | 'yellow' | 'red';
 
function changeLight(color: Color) {
  // ...
}
```