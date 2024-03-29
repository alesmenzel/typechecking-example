# Typechecking example

Using typescript to typecheck JavaScript files.

## Setup

Install typescript.

```bash
npm i --save-dev typescript
```

Create a typescript configuration.

```bash
npx tsc --init
```

and use the following configuration:

```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "allowJs": true,
    "checkJs": true,
    "noEmit": true,
    "strict": true,
    "esModuleInterop": true
  },
  "include": ["./**/*.js"],
  "exclude": ["node_modules"]
}
```

Now you can run

```bash
npx tsc
```

and it will print all typechecking errors, like this:

```bash
$ npx tsc
index.js:12:5 - error TS2345: Argument of type '"5"' is not assignable to parameter of type 'number'.

12 add("5", "6");


Found 1 error.
```

## Defining a type

One way to define types is with JSDoc.

```js
/**
 * Add two numbers
 *
 * @param {Number} a
 * @param {Number} b
 */
function add(a, b) {
  return a + b;
}
```

you can mark optional parameters with `[]`.

```js
/**
 * Get the current weather
 *
 * @param {Object} [opts]
 * @param {Function} next
 */
function getWeather(opts, next) {
  // ...
}
```

Defining type of a variable:

```js
/**
 * @type {Number}
 */
const INTERVAL = 12000;
```

## Ignoring stuff

In the rare case you really need to disable type checking for some odd reason. Add `// @ts-nocheck` comment at the first line of your file (this will ignore typechecks in the whole file).

```js
// @ts-nocheck
```

To only disable it for a certain line (the part after `:` is an optional description why we ignore it):

```js
// @ts-ignore
add("5", 6);

// @ts-ignore: The function can handle it
add("5", 6);
```

For some odd reason you still cant ignore a block of code though ([see this issue on github for more information](https://github.com/Microsoft/TypeScript/issues/19573)).
