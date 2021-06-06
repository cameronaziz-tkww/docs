# 🌀 Typescript Style Guide
  - [Typings](#typings)
    - [External](#external)
    - [Internal](#internal)
  - [Filenames](#filenames)
  - [Semicolons](#semicolons)
  - [Quotes](#quotes)
  - [Spaces](#spaces)
  - [References](#references)
    - [Primatives](#primatives)
    - [Objects](#objects)
    - [Arrays](#arrays)
    - [Tuples](#tuples)
    - [Enums](#enums)
  - [Special Types](#special-types)
    - [Unknown](#unknown)
    - [Any](#any)
    - [Void](#void)
    - [Never](#never)
  - [Interfaces & Types](#interfaces--types)
  - [Functions](#functions)
  - [Optional](#optional)
  - [ReadOnly](#readonly)
  - [Generics](#generics)
  - [Type Guards](#type-guards)
## Typings
### External
- Typings are sometimes packaged with node modules, in this case you don't need to do anything
- Use @types for all external library declarations not included in node_modules
- Packages that do not have types defined, create the module in `types/thirdParty`

```typescript
// types/thirdParty/externalLibraryName
declare module 'external-library-name' {
  interface NamedExportParams {
    a: string;
  }

  interface DefaultExportParams {
    b: boolean;
  }


  const namedExport = (params: NamedExportParams) => {};

  export default (params: DefaultExportParams) => {};;
}
```

### Internal
- Create declaration files .d.ts for your interfaces instead of putting them in your .ts files

## Filenames
* Name files with `camelCase`, e.g. `index.ts`, `actionCreators.ts`, `myComponent.tsx`
* Files with a React component need the filetype `.tsx`
* Every folder should have a root `index.ts[x]`. This file is often used to export sibling files for easy import

## Semicolons
* Yup. Use them. Don't argue
```typescript
// Good
interface Foo {
  a: name;
}

type Bar = string | number;

// Bad
interface Baz {
  a: name
}

interface Qux {
  a: name;
}; // There should not be a semicolon at the end of the interface

type Quux = string | number
```

## Quotes
* Use single quotes unless double quotes are required
```typescript
interface Foo {
  'a-b': string;
  static: 'word';
  "can't": never; // This will error if it is single quoted
}

interface Bar {
  "a-b": string;
  static: "word";
}
```

## Spaces
* Use `2` spaces to indent members. Do not use tabs
```typescript
// Good
interface Foo {
  a: name;
}

// Bad
interface Bar {
a: name;
}

interface Baz {
    a: name;
}
```

* Left align if not a member of a parent item
```typescript
// Good
interface Foo {
  a: name;
}

namespace Bar {
  interface Foo {
    a: name;
  }
}

declare module Baz {
  interface Foo {
    a: name;
  }
}

// Bad
  interface Qux {
    a: name;
  }
```

## References
### Primatives
* When defining a primitive, let Typescript implicitly define the type
```typescript
// Good
const foo = true;
const bar = 123;
const baz = 'string';

// Bad
const qux: boolean = false;
const quux: number = 321;
const quuux: string = 'quuux';
```

* Do not use the capital version of the type. These types do not refer to the language primitives however, and almost never should be used as a type
```typescript
// Good
const foo = (): boolean => true;
const bar = (): number => 123;
const baz = (): string => 'string';

// Bad
const qux = (): Boolean => false;
const quux = (): Number => 321;
const quuux = (): String => 'quuux';
const quuuux = (): Object => ({}); // object should not be used either
```

### Objects
* Typescript is a [structural type system](https://en.wikipedia.org/wiki/Structural_type_system) where the members are evaluated instead of the specific type
* When defining an object, it is often advisable to explicitly define the type, but it is not required

```typescript
// Good
interface Foo {
  a: string;
}

const foo: Foo = {
  a: 'name';
};

// Ok
interface Bar {
  a: string;
}
const bar = {
  a: 'string',
  b: true
};
const returnA = (barItem: Bar) => barItem.a;
returnA(bar); // This will not throw an error
returnA({
  a: 'string',
  b: true
}); // This will throw an error. See More Info link below

// Bad
interface Baz {
  a: string;
  b?: boolean
}
const baz = {
  a: 'string'
}

baz.b = false; // This will throw an error, b does not exist on baz
```
[More Info](https://www.typescriptlang.org/docs/handbook/interfaces.html#excess-property-checks)

* When possible, do not use the `object` type. Use `Record<string, PropertyType>`
```typescript
// Good
type PropertyType = string | number
interface Foo {
  data: Record<string, PropertyType>
}

const foo1: Foo = {
  data: {
    a: 'string',
    b: 1
  }
}
const foo2: Foo = {
  data: {
    a: 1
    b: 'string',
  }
}

// Good, yet not as typesafe as Foo
interface Bar {
  data: Record<string, unknown>
}

const bar1: Bar = {
  data: {
    a: 1,
    b: foo
  }
}
const bar2: Bar = {
  data: {
    a: 'string',
    b: true
  }
}

// Bad
interface Baz {
  data: object
}
const baz: Baz = {
  data: {
    a: 'string'
  }
}
```

### Arrays
* Arrays can be defined with a given type or types
```typescript
const foo: string[] = ['a', 'b'];
const bar: (string | number)[] = ['a', 1];
const bar: (string | number)[] = [1, 'a'];
```

* Standard arrays do not have a set length, and items can be pushed to it. A `ReadonlyArray` can be used, but this will also prevent items from being changed as well
```typescript
const foo: string[] = ['a', 'b'];
// Good
foo.push('c');

// Bad
foo.push(1);
```

* For a given `ItemType`, use `ItemType[]` not `Array<ItemType>`
```typescript
const foo: string[] = ['a', 'b'];
const bar: (string | number)[] = ['a', 1];
const bar: (string | number)[] = [1, 'a'];
```

* Standard arrays do not have a set length, and items can be pushed to it. A `ReadonlyArray` can be used, but this will also prevent items from being changed as well
```typescript
const foo: string[] = ['a', 'b'];
// Good
const foo: string[] = [];

// Bad
const bar: Array<string> = [];
```

### Tuples
* If array items and length are known, use a tuple
```typescript
const foo: [string, number] = ['a', 1];
foo[2] = true // this will throw an error


type Bar = (string | number)[];
const bar: Bar = ['a', 1];
bar[0] = 1; // If bar[0] needs to be a string, this will not fail
bar[2] = 'array too long' // This will not throw an error
```

* Use variable tuple types if we know certain items, but not length
```typescript
type ALotOfStrings = string[];
type Foo = [boolean, ...ALotOfStrings, number];

const foo1: Foo = [true, 1];
const foo2: Foo = [true, 'string', 1];
const foo3: Foo = [true, 'string', 'string', 'string', 'string', 1];
```

### Enums
* Useful for english readable indexes. By default, they are zero based
```typescript
enum Color {
  Red,
  Green,
  Blue,
}
console.log(Color.Green); // 1
```

* Assigning a number to an member will return indexes in relation to number provided
```typescript
enum Metal {
  Gold = 1,
  Silver,
  Bronze
}
console.log(Metal.Silver); // 2
```

* Enums are also built with reverse mappings
```typescript
enum Grade {
  Freshman = 9,
  Sophomore,
  Junior,
  Senior,
}

console.log(Grade.Sophomore); // 10
console.log(Grade['Junior']); // 11
console.log(Grade[12]); // Senior
```

## Special Types
### Unknown
Unknown can be used for a a data type that is not known, such as in a type check or an API response
```typescript
const isNumber = (item: unknown): item is number => typeof item === number;
const foo = (a: number) => a;

const data = 'string';

if (isNumber(data)) {
  foo(data);          // Will never be evaluated
}

// Bad
foo(data); // This will throw an error
```

### Any
* Avoid the `any` type. Your pull request may be rejected with only a single `any`
```typescript
// Good
const foo = (a: unknown) => a;

// Bad
const bar = (a: any) => a;
```

### Void
Void is used to define that nothing will be returned from a given function
```typescript
interface Foo {
  () => void
}

// Good
const foo1: Foo = () => {
  doSomething();
};

// Bad
const foo2: Foo = () => doSomething();
```

### Never
Never is a type that should never occur
```typescript
interface Foo<T> {
  a: T
  b: T extends string ? boolean : never;
}

// Good
const foo1: Foo = {
  a: 'string',
  b: true
};

const throwError = (): never => {
  throw new Error('Something went wrong.')
}

// Bad
const foo2: Foo = {
  a: 1,
  b: true
};
```

## Interfaces & Types
* Use `PascalCase` for name
```typescript
// Good
interface FooBar {
  a: string;
}

// Bad
interface barFoo = {
  a: string;
}

interface bar_foo = {
  a: string;
}
```

* Use `camelCase` for members
```typescript
// Good
interface Foo {
  aString: string;
}

// Bad
interface Bar {
  AString: string;
}

interface Baz {
  A_String: string;
}
```

* Do not prepend types and interfaces with `I` or `T`
```typescript
// Good
interface Foo {
  a: string;
}

// Bad
interface IBar {
  a: string;
}

type TBaz = string | number;
```

* When analogous, use an `interface` over using a `type`
  * Use type when you need a union or intersection
  * An interface can `extends` or `implements`, while types can not
```typescript
// Good
interface Foo {
  a: string;
}

interface Bar {
  () => string;
}

type Baz = string | number;
type Qux = Foo & Bar;

// Not advisable, but it exists in our codebase
type Quux = (a: string) => string;

// Bad
type Quuux = {
  a: string;
}
```

## Functions
* Like javascript, functions are simply objects
```typescript
// Bad
interface Bar {
  a: number
}

const bar: Bar = (a: number) => this.a + a
bar.a = 1 // This will not error as long as foo.a is defined in the same module that foo is instantiated in
```

## Optional
* An interface or type member can be defined as optional
```typescript
// Good
interface Foo {
  a: string;
  b?: string;
}

const foo: Foo = {
  a: 'string'
};
foo.b = 'another string';

// Bad
interface Bar {
  a: string;
  b: string;
}

const bar: Bar = {
  a: 'string'
}; // This will throw an error
```

## ReadOnly
* Like `const` is used to make primitives immutable, defining an interface or type member as `readonly` will make the member immutable
```typescript
interface Foo {
  readonly a: string
}

const foo: Foo = {
  a: 'string'
}
foo.a = 'new string' // This throws and error
```

* Even `readonly` optional propeties can not be set once the object is defined
```typescript
interface Foo {
  readonly a?: string
}

const foo: Foo = {}
foo.a = 'string' // This throws and error
```

## Generics
* Use `T` for the type variable if only one is needed
```typescript
// Good
const foo = <T>(arg: T): T => arg;

// Bad
const foo = <Arg>(arg: Arg): Arg => arg;
```

* If more than one type variable is required, start with `T` and name your variable in alphabetical sequence
```typescript
// Good
const foo = <T, U extends keyof T>(obj: T, key: U): T[U] => obj[key];

// Bad
const foo = <T, K extends keyof T>(obj: T, key: K): T[K] => obj[key];
```

* When possible, allow the compiler to infer type of variables
```typescript
const foo = <T>(arg: T): T => arg;

// Good
const output = foo('myString');

// Bad
const output = foo<string>('myString');
```

## Type Guards
- Alway be explicit in your typeguards

```typescript
// Good
const isString = (str: unknown): str is string => {
    return typeof str === 'string'
}

// Bad
const isString = (str: unknown): str is string => {
    return !!str
}
```