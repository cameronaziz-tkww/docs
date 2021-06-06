# Syntax

## Object and Array Literals

- Use curly braces {} instead of new Object()

```typescript
// Good
const foo = {};
const bar = {
  a: 'string',
};

// Bad
const baz = new Object();
const qux = new Object();
qux.a = 'string';
```

- Use brackets [] instead of new Array()

```typescript
// Good
const foo = [];
const bar = [
  {
    a: 'string',
  },
];

// Bad
const baz = new Array();
const qux = new Array();
qux.push({ a: 'string' });
```

## Assignment Expressions

- Assignment expressions inside of the condition block of if, while, and do while statements should be avoided

```typescript
// Good
while (typeof node === 'object') {
  node = node.next;
  // ...
}

// Bad
while ((node = node.next)) {
  // ...
}
```
