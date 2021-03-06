# csv-mapper-lite

![build](https://img.shields.io/circleci/project/github/j1wu/csv-mapper-lite.svg)
[![Coverage Status](https://coveralls.io/repos/github/j1wu/csv-mapper-lite/badge.svg?branch=master)](https://coveralls.io/github/j1wu/csv-mapper-lite?branch=master)
[![node6.10.1](https://img.shields.io/badge/node-6.10.1-green.svg)](https://nodejs.org/en/blog/release/v0.6.10/)
[![](https://img.shields.io/badge/ava-0.19.1-green.svg)](https://github.com/avajs/ava)
[![](https://img.shields.io/badge/flow-0.49.1-green.svg)](https://github.com/facebook/flow)
[![npm](https://img.shields.io/npm/v/csv-mapper-lite.svg)](https://www.npmjs.com/package/csv-mapper-lite)

A node.js library for parsing and mapping csv string into pre-defined format.


# Installation

With [yarn](https://yarnpkg.com):

    $ yarn add csv-mapper-lite

With [npm](http://npmjs.org):

    $ npm install csv-mapper-lite


# Tests

Tests are written using the futuristic JavaScript test runner, [ava](https://github.com/avajs/ava).

    $ yarn test


# API Documentation

## process(input : String, mapping : Object) : String

```js
const csvStr = 'col1,col2,col3,,\nworld,hello\n'
const Formatter = require('csv-mapper-lite')
const formatter = new Formatter(csvStr, {
  // required
  rules: {
    newCol1: { expr: 'this.B', defaultValue: '0' },
    newCol2: { expr: 'this.A', defaultValue: '0' },
    newCol3: { expr: 'this.B+this.A', defaultValue: '0' }
  },
  // optional. Additional options and their default values
  separator: ',',
  newLine: '\n',
  noHeader: false,
  shiftFirstRow: false,
  trimTrailing: false,
  dropLastRow: false,
  dropRow: '' // accepts an expression string which will be evaluated during formatting, if evaluation result returns true, current row will be dropped.
})

const output = formatter.process()
console.log(output);
```
Output:
```js
'newCol1,newCol2,newCol3\nhello,world,helloworld'
```