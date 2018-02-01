# flow-runtime-experiment

`flow-runtime` allows us to add runtime type-checks with a lean syntax. 

For example, this: 

```javascript=
const add = (x, y) => {
  if (Number.isNaN(x)) {
    throw new Error('x must be a number');
  }
  if (Number.isNaN(y)) {
    throw new Error('y must be a number');
  }
  return x + y;
}
```

Can be written like this: 

```javascript=
const add = (x : number, y : number) => {
  return x + y;
}
```

## Demo

```bash=
yarn install --pure-lockfile 
```

First add type definitions to your code. For example: 

```bash=
cat ./src/index.js
```

Build the library using Babel: 

```bash=
yarn build
```

This generates standard ES code that you can run in Node: 

```bash=
cat ./lib/index.js

node
> require('./lib').add(1, 2)
3
```

And `flow-runtime` gives us type checks: 

```bash=
node
> require('./lib').add(1, 'world')
RuntimeTypeError: y must be a number

Expected: number

Actual Value: "world"

Actual Type: string
```
