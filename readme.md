# First Steps with NPM

[![CI build](https://github.com/ueberfuhr-tutorials/npm-first-steps/actions/workflows/ci.yml/badge.svg)](https://github.com/ueberfuhr-tutorials/npm-first-steps/actions/workflows/ci.yml)

This tutorial will introduce how to build and use a first NPM module. It contains the solution projects, but to understand how NPM works, you should do the steps at your own.

## Create a Helloword Module

### Project Initialization

```bash
# Create an empty directory
mkdir npm-helloworld
cd npm-helloworld
# Create a package.json file
npm init
# ... just press 'OK' multiple times until the file is generated
```

Open the `package.json` and add the following line:

```json
{
  "type": "module"
}

```

### Implementation

Create a `index.js` file (referenced in `package.json`) with the following content:

```javascript
export function getHelloWorld() {
    return "Hello World!";
}
```

### Testing

Install test frameworks to your project, e.g.

```bash
npm install chai@latest --save-dev
npm install mocha@latest --save-dev
```

Then, create a `test.js` file with this content:

```javascript
import { expect } from 'chai';
import { getHelloWorld } from './index.js';

describe('Function getHelloWorld', () => {
    it('Should Return Hello World!', () => {
        expect(getHelloWorld()).to.equal("Hello World!");
    });
});
```

To make the test runnable, insert a script into the `package.json` file:

```json
{
  "scripts": {
    "test": "mocha test.js"
  }
}
```

You should then be able to run the test with

```bash
npm run test
```

# Use the Module in another one

## Project Initialization

Initialize another NPM module (e.g. `npm-myapp`) the same way.

## Use the module

Install the `npm-helloworld` module. Because we want to do this without any remote repository, we need to pack the module and install it into the new one.

```bash
# in npm-helloworld, create a TGZ file
npm pack
# in npm-myapp
npm install <path-to-tgz-file>
```

Create an `index.js` file and use the function from the other module:

```javascript
import { getHelloWorld } from "npm-helloworld";

console.log(getHelloWorld()); 
```

You should then be able to start it with

```bash
node index.js
```

It is recommended to add a script to `package.json`:

```json
{
  "scripts": {
    "start": "node index.js"
  }
}
```

You should then be able to run the test with

```bash
npm run start
```
