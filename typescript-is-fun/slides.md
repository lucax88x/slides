---
theme: apple-basic
background: false
title: typescript is fun
subtitle: todo subtitle
highlighter: shiki
drawings:
  persist: false
transition: slide-left
layout: center
class: text-center
src: ../shared/start.md
---
imported slide
---
src: ../shared/me.md
---
imported slide
---
layout: center
class: text-center
---

# TypeScript is Fun
<br>

forget about the browser

---
layout: quote
---

# "TypeScript's type system is Turing complete"

<div class="text-right text-sm opacity-70 mt-8">
Wait... what?
</div>

---

# What Can We Do?

<div class="grid grid-cols-2 gap-8 mt-8">

<div>

## 🥱 Boring TypeScript

```ts
interface User {
  name: string;
  age: number;
}

function greet(user: User): string {
  return `Hello ${user.name}`;
}
```

<div class="text-sm opacity-70 mt-4">
Type checking, autocompletion, safety...
</div>

</div>

<div>

## 🤯 Fun TypeScript

```ts
type Reverse<S extends string> =
  S extends `${infer First}${infer Rest}`
    ? `${Reverse<Rest>}${First}`
    : S;

type Result = Reverse<'hello'>
//   ^? 'olleh'
```

<div class="text-sm opacity-70 mt-4">
Compile-time computation, type-level programming...
</div>

</div>

</div>

---

# String Manipulation at Type Level

<div class="text-sm">

```ts {all|1-4|6-9|11-14|16-19|all}
// Capitalize first letter
type Capitalize<S extends string> = S extends `${infer F}${infer R}`
  ? `${Uppercase<F>}${R}`
  : S;

// Snake case to camel case
type SnakeToCamel<S extends string> = S extends `${infer T}_${infer U}`
  ? `${T}${Capitalize<SnakeToCamel<U>>}`
  : S;

// Parse template literal
type ParseRoute<T extends string> =
  T extends `${infer Start}/:${infer Param}/${infer Rest}`
    ? { [K in Param | keyof ParseRoute<`/${Rest}`>]: string }
    : {};

type UserRoute = ParseRoute<'/users/:userId/posts/:postId'>
//   ^? { userId: string; postId: string }
```

</div>

<div class="mt-4 text-sm opacity-70">
✨ Type-safe routing, zero runtime cost
</div>

---

# SQL Query Builder (Type-Safe!)

```ts {all|1-6|8-15|17-24|26-28|all}
type User = {
  id: number;
  name: string;
  email: string;
  age: number;
};

// SELECT builder
type Select<T, K extends keyof T> = {
  [P in K]: T[P]
};

type Query1 = Select<User, 'id' | 'name'>
//   ^? { id: number; name: string }

// WHERE builder with type inference
type Where<T, K extends keyof T, V> =
  V extends T[K] ? T : never;

type Query2 = Where<User, 'age', number>
//   ^? User (age is number ✓)

type Query3 = Where<User, 'age', string>
//   ^? never (age is not string ✗)

const result: Query1 = { id: 1, name: 'John' }
// email missing? ✓ Type error!
// age included? ✓ Type error!
```

---

# Template Literal Types: The Fun Begins

```ts {all|1-3|5-10|12-17|19-22|all}
// CSS properties
type CSSValue = string | number;
type CSSUnit = 'px' | 'em' | 'rem' | '%' | 'vh' | 'vw';

// Generate all possible combinations
type Size = `${number}${CSSUnit}`;

const margin: Size = '16px';    // ✓
const padding: Size = '2rem';   // ✓
const invalid: Size = '10kg';   // ✗ Type error!

// Direction helpers
type Direction = 'top' | 'right' | 'bottom' | 'left';
type MarginProps = `margin${Capitalize<Direction>}`;

type Props = { [K in MarginProps]: Size };
//   ^? { marginTop: Size; marginRight: Size; ... }

// Use it
const styles: Props = {
  marginTop: '10px',
  marginRight: '20px',
  marginBottom: '10px',
  marginLeft: '20px',
};
```

---

# Recursive Types: Math at Compile Time

```ts {all|1-4|6-9|11-14|16-19|21-24|all}
// Build tuple of length N
type BuildTuple<L extends number, T extends any[] = []> =
  T['length'] extends L ? T : BuildTuple<L, [...T, any]>;

// Add two numbers
type Add<A extends number, B extends number> =
  [...BuildTuple<A>, ...BuildTuple<B>]['length'];

type Sum = Add<5, 3>;
//   ^? 8

// Subtract
type Subtract<A extends number, B extends number> =
  BuildTuple<A> extends [...BuildTuple<B>, ...infer R] ? R['length'] : never;

type Diff = Subtract<10, 3>;
//   ^? 7

// Multiply
type Multiply<A extends number, B extends number, Acc extends any[] = []> =
  B extends 0 ? Acc['length']
    : Multiply<A, Subtract<B, 1>, [...Acc, ...BuildTuple<A>]>;

type Product = Multiply<4, 3>;
//   ^? 12
```

<div class="mt-4 text-sm opacity-70">
⚠️ TypeScript has recursion limits, but still... mind = blown
</div>

---

# Conditional Types: Type-Level If-Else

```ts {all|1-4|6-9|11-17|19-22|all}
// Extract return type from function
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

type Fn = () => string;
type R = ReturnType<Fn>; // string

// Deep readonly
type DeepReadonly<T> = {
  readonly [P in keyof T]: T[P] extends object
    ? DeepReadonly<T[P]>
    : T[P];
};

type User = { name: string; address: { city: string } };
type ReadonlyUser = DeepReadonly<User>;
//   ^? { readonly name: string; readonly address: { readonly city: string } }

// Flatten nested arrays
type Flatten<T> = T extends (infer U)[]
  ? Flatten<U>
  : T;

type Nested = number[][][];
type Flat = Flatten<Nested>;
//   ^? number
```

---

# Pattern Matching with Infer

```ts {all|1-5|7-12|14-19|21-27|all}
// Extract Promise value
type Awaited<T> = T extends Promise<infer U>
  ? Awaited<U>
  : T;

type P1 = Awaited<Promise<string>>;              // string
type P2 = Awaited<Promise<Promise<number>>>;     // number

// Extract array element type
type ElementType<T> = T extends (infer E)[] ? E : T;

type Arr = ElementType<string[]>;   // string
type NotArr = ElementType<number>;  // number

// Extract function parameters
type Parameters<T> = T extends (...args: infer P) => any ? P : never;

type Fn = (a: string, b: number) => void;
type Params = Parameters<Fn>;
//   ^? [a: string, b: number]

// Pop last element from tuple
type Pop<T extends any[]> = T extends [...infer Rest, any] ? Rest : [];

type Tuple = [1, 2, 3, 4];
type Popped = Pop<Tuple>;
//   ^? [1, 2, 3]
```

---

# Mapped Types: Transform Everything

```ts {all|1-6|8-13|15-22|24-31|all}
// Make everything optional
type Partial<T> = {
  [P in keyof T]?: T[P];
};

type User = { id: number; name: string };
type PartialUser = Partial<User>;
//   ^? { id?: number; name?: string }

// Pick specific keys
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};

type UserPreview = Pick<User, 'name'>;
//   ^? { name: string }

// Omit specific keys
type Omit<T, K extends keyof T> = Pick<T, Exclude<keyof T, K>>;

type UserWithoutId = Omit<User, 'id'>;
//   ^? { name: string }

// Transform all values to promises
type Promisify<T> = {
  [P in keyof T]: Promise<T[P]>;
};

type UserAPI = Promisify<User>;
//   ^? { id: Promise<number>; name: Promise<string> }
```

---

# The Ultimate Challenge: Type-Level JSON Parser

<div class="text-xs">

```ts {all|1-5|7-16|18-25|27-35|all}
// Tokenize JSON string
type Tokenize<S extends string> =
  S extends `${infer T}${infer Rest}`
    ? T extends '{' | '}' | '[' | ']' | ':' | ',' ? [T, ...Tokenize<Rest>] : Tokenize<Rest>
    : [];

// Parse JSON object
type ParseObject<T extends string, Acc = {}> =
  T extends `"${infer Key}":${infer Rest}`
    ? Rest extends `"${infer Value}"${infer After}`
      ? ParseObject<After, Acc & { [K in Key]: Value }>
      : Rest extends `${infer Num extends number}${infer After}`
        ? ParseObject<After, Acc & { [K in Key]: Num }>
        : Acc
    : Acc;

// Usage
type JSON1 = ParseObject<'"name":"John"'>
//   ^? { name: "John" }

type JSON2 = ParseObject<'"age":30'>
//   ^? { age: 30 }

type ComplexJSON = ParseObject<'"name":"John","age":30'>
//   ^? { name: "John"; age: 30 }
```

</div>

<div class="mt-4 text-sm opacity-70">
💀 Yes, you can parse JSON at compile time... but should you?
</div>

---

# Real-World: Type-Safe Event Emitter

```ts {all|1-5|7-13|15-20|22-28|all}
type Events = {
  'user:login': { userId: string; timestamp: number };
  'user:logout': { userId: string };
  'order:created': { orderId: string; amount: number };
};

class TypedEmitter<T extends Record<string, any>> {
  on<K extends keyof T>(event: K, handler: (data: T[K]) => void) {
    // implementation
  }

  emit<K extends keyof T>(event: K, data: T[K]) {
    // implementation
  }
}

const emitter = new TypedEmitter<Events>();

// ✓ Type-safe!
emitter.on('user:login', (data) => {
  console.log(data.userId, data.timestamp);
});

// ✗ Type error!
emitter.emit('user:login', { userId: '123' });
// Missing 'timestamp' property

emitter.emit('invalid:event', {});
// Unknown event type
```

---

# Real-World: Type-Safe State Machine

```ts {all|1-10|12-21|23-30|all}
type States = {
  idle: { type: 'idle' };
  loading: { type: 'loading'; progress: number };
  success: { type: 'success'; data: string };
  error: { type: 'error'; message: string };
};

type ValidTransitions = {
  idle: 'loading';
  loading: 'success' | 'error';
  success: 'idle';
  error: 'idle';
};

type CanTransition<From extends keyof States, To extends keyof States> =
  To extends ValidTransitions[From] ? To : never;

// Usage
function transition<From extends keyof States, To extends keyof States>(
  from: States[From],
  to: CanTransition<From, To>
): States[CanTransition<From, To>] | never {
  // implementation
  return {} as any;
}

transition({ type: 'idle' }, 'loading');        // ✓
transition({ type: 'loading' }, 'success');     // ✓
transition({ type: 'idle' }, 'success');        // ✗ Invalid transition!
```

---

# Branded Types: Make Primitives Safer

```ts {all|1-4|6-11|13-18|20-28|all}
// Create branded types
type Brand<K, T> = K & { __brand: T };

type UserId = Brand<string, 'UserId'>;
type Email = Brand<string, 'Email'>;
type PostId = Brand<number, 'PostId'>;

// Constructor functions
const UserId = (id: string): UserId => id as UserId;
const Email = (email: string): Email => email as Email;
const PostId = (id: number): PostId => id as PostId;

// Type-safe functions
function getUserById(id: UserId): User { /* ... */ }
function sendEmail(to: Email, subject: string): void { /* ... */ }
function getPost(id: PostId): Post { /* ... */ }

// Usage
const userId = UserId('user-123');
const email = Email('test@example.com');
const postId = PostId(42);

getUserById(userId);           // ✓
getUserById('random-string');  // ✗ Type error!
sendEmail(userId, 'Hello');    // ✗ Type error! (userId is not Email)
getPost(42);                   // ✗ Type error! (need PostId)
getPost(postId);               // ✓
```

---

# Type Gymnastics: FizzBuzz

```ts {all|1-7|9-15|17-20|22-29|all}
// Build number range
type Range<N extends number, Acc extends number[] = []> =
  Acc['length'] extends N
    ? Acc[number]
    : Range<N, [...Acc, Acc['length']]>;

type Numbers = Range<100>; // 0 | 1 | 2 | ... | 99

// FizzBuzz logic
type FizzBuzz<N extends number> =
  N extends 0 ? 'FizzBuzz'
  : [N] extends [0] ? N
  : `${N}` extends `${string}${0 | 5}`
    ? `${N}` extends `${string}${0}` ? 'Buzz' : 'Fizz'
    : N;

// More precise version
type Mod15<N extends number> = `${N}` extends `${string}${0 | 5}` ? 0 : 1;
type Mod3<N extends number> = /* complex logic */;
type Mod5<N extends number> = /* complex logic */;

type FizzBuzzPrecise<N extends number> =
  [Mod3<N>, Mod5<N>] extends [0, 0] ? 'FizzBuzz'
  : Mod3<N> extends 0 ? 'Fizz'
  : Mod5<N> extends 0 ? 'Buzz'
  : N;

type Test = FizzBuzz<15>;  // 'FizzBuzz'
type Test2 = FizzBuzz<9>;  // 'Fizz'
type Test3 = FizzBuzz<10>; // 'Buzz'
```

---

# Advanced: Chainable API

```ts {all|1-8|10-17|19-26|all}
type Chainable<T = {}> = {
  option<K extends string, V>(
    key: K extends keyof T ? never : K,
    value: V
  ): Chainable<T & { [P in K]: V }>;

  get(): T;
};

// Implementation
const config = <T>(): Chainable<T> => ({
  option: (key: any, value: any) => config(),
  get: () => ({} as T)
});

// Usage - fully type-safe!
const result = config()
  .option('host', 'localhost')
  .option('port', 3000)
  .option('ssl', true)
  .option('host', 'duplicate')  // ✗ Error: 'host' already exists!
  .get();

type Result = typeof result;
//   ^? { host: string; port: number; ssl: boolean }
```

---

# The Dark Arts: HKT Simulation

<div class="text-xs">

```ts {all|1-7|9-18|20-30|32-39|all}
// Higher-Kinded Types (HKT) - not natively supported, but...
interface HKT {
  readonly _URI: unique symbol;
  readonly _A: unknown;
  readonly out: unknown;
}

type URI2HKT<URI extends string, A> = {
  readonly _URI: URI;
  readonly _A: A;
};

type URIS = 'Array' | 'Promise' | 'Option';

interface URItoKind<A> extends URI2HKT<URIS, A> {
  readonly Array: Array<A>;
  readonly Promise: Promise<A>;
  readonly Option: Option<A>;
}

type Kind<URI extends URIS, A> = URItoKind<A>[URI];

// Now we can write generic functions!
type Map<F extends URIS, A, B> = (fa: Kind<F, A>) => Kind<F, B>;

const mapArray: Map<'Array', number, string> =
  (arr) => arr.map(String);

const mapPromise: Map<'Promise', number, string> =
  (p) => p.then(String);
```

</div>

<div class="mt-4 text-sm opacity-70">
🧙‍♂️ Yes, we're emulating category theory in TypeScript's type system
</div>

---

# Practical Magic: Form Validation

```ts {all|1-8|10-20|22-34|all}
type ValidationRule<T> = {
  required?: boolean;
  min?: T extends number ? number : never;
  max?: T extends number ? number : never;
  minLength?: T extends string ? number : never;
  maxLength?: T extends string ? number : never;
  pattern?: T extends string ? RegExp : never;
};

type Schema = {
  username: ValidationRule<string> & { required: true; minLength: 3 };
  email: ValidationRule<string> & { required: true; pattern: RegExp };
  age: ValidationRule<number> & { min: 18; max: 120 };
  bio: ValidationRule<string> & { maxLength: 500 };
};

type ValidatedForm<S extends Record<string, ValidationRule<any>>> = {
  [K in keyof S]: S[K] extends { required: true }
    ? string | number
    : string | number | undefined;
};

type Form = ValidatedForm<Schema>;
//   ^? { username: string; email: string; age: number; bio?: string }

const form: Form = {
  username: 'john',
  email: 'john@example.com',
  age: 25,
  // bio is optional
};

// Missing username? ✗ Type error!
// age as string? ✗ Type error!
```

---

# Type-Level Parsers: Command Line Args

```ts {all|1-6|8-16|18-26|all}
type ParseArgs<T extends string> =
  T extends `--${infer Flag}=${infer Value} ${infer Rest}`
    ? { [K in Flag]: Value } & ParseArgs<Rest>
    : T extends `--${infer Flag}=${infer Value}`
      ? { [K in Flag]: Value }
      : {};

// Enhanced with type conversion
type ParseValue<V extends string> =
  V extends 'true' | 'false' ? boolean
  : V extends `${number}` ? number
  : V extends `[${infer Items}]` ? Items extends `${infer A},${infer B}`
    ? [ParseValue<A>, ParseValue<B>]
    : [ParseValue<Items>]
  : string;

type SmartParseArgs<T extends string> =
  T extends `--${infer Flag}=${infer Value} ${infer Rest}`
    ? { [K in Flag]: ParseValue<Value> } & SmartParseArgs<Rest>
    : T extends `--${infer Flag}=${infer Value}`
      ? { [K in Flag]: ParseValue<Value> }
      : {};

type Args = SmartParseArgs<'--port=3000 --debug=true --name=server'>;
//   ^? { port: 3000; debug: true; name: "server" }
```

---

# Extreme: Tic-Tac-Toe in Types

<div class="text-xs">

```ts {all|1-7|9-18|20-30|32-40|all}
type Cell = 'X' | 'O' | ' ';
type Board = [
  [Cell, Cell, Cell],
  [Cell, Cell, Cell],
  [Cell, Cell, Cell]
];

type EmptyBoard = [[' ', ' ', ' '], [' ', ' ', ' '], [' ', ' ', ' ']];

// Make a move
type Move<B extends Board, Row extends 0 | 1 | 2, Col extends 0 | 1 | 2, Player extends 'X' | 'O'> =
  B[Row][Col] extends ' '
    ? [
        Row extends 0 ? SetCell<B[0], Col, Player> : B[0],
        Row extends 1 ? SetCell<B[1], Col, Player> : B[1],
        Row extends 2 ? SetCell<B[2], Col, Player> : B[2]
      ]
    : never;

type SetCell<R extends [Cell, Cell, Cell], Col extends 0 | 1 | 2, Player extends 'X' | 'O'> =
  Col extends 0 ? [Player, R[1], R[2]]
  : Col extends 1 ? [R[0], Player, R[2]]
  : [R[0], R[1], Player];

// Check winner
type CheckWinner<B extends Board> =
  // Check rows, columns, diagonals...
  // (implementation omitted for brevity)
  'X' | 'O' | 'draw' | 'ongoing';

// Play the game!
type Game1 = Move<EmptyBoard, 0, 0, 'X'>;
//   ^? [['X', ' ', ' '], [' ', ' ', ' '], [' ', ' ', ' ']]

type Game2 = Move<Game1, 1, 1, 'O'>;
//   ^? [['X', ' ', ' '], [' ', 'O', ' '], [' ', ' ', ' ']]

type InvalidMove = Move<Game1, 0, 0, 'O'>;
//   ^? never (cell already taken!)
```

</div>

---
layout: two-cols
---

# Why Do This?

<div class="text-sm">

### 🧠 Learn Deep Patterns

- Understand variance
- Master conditional types
- Think in transformations

### 🛡️ Bulletproof APIs

- Impossible states = impossible
- Compiler catches bugs
- Self-documenting code

### ⚡ Zero Runtime Cost

- All computation at compile time
- No bundle size impact
- Pure type safety

</div>

::

<div class="text-sm">

### 🎯 Real Benefits

**Type-safe routing**
```ts
router.get('/users/:id', (req) => {
  req.params.id // string ✓
})
```

**Type-safe queries**
```ts
db.select('users')
  .where('age', '>', 18)
  .pick('name', 'email')
// Type: { name: string; email: string }[]
```

**Type-safe forms**
```ts
<Form schema={userSchema}>
  {/* Autocomplete for all fields */}
  {/* Type errors for invalid fields */}
</Form>
```

</div>

---
layout: center
class: text-center
---

# TypeScript: Not Just for the Browser

<div class="mt-8 text-lg opacity-80">

It's a full programming language<br>
that runs at **compile time**

</div>

<div class="mt-12 text-sm opacity-60">

Resources:
- [Type Challenges](https://github.com/type-challenges/type-challenges)
- [ts-toolbelt](https://github.com/millsp/ts-toolbelt)
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)

</div>

