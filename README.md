
[![CI](https://github.com/viktor-podzigun/mock-fn/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/viktor-podzigun/mock-fn/actions/workflows/ci.yml?query=workflow%3Aci+branch%3Amain)
[![Coverage Status](https://coveralls.io/repos/github/viktor-podzigun/mock-fn/badge.svg?branch=main)](https://coveralls.io/github/viktor-podzigun/mock-fn?branch=main)
[![npm version](https://img.shields.io/npm/v/mock-fn)](https://www.npmjs.com/package/mock-fn)

## mock-fn

Simple `mockFunction` test utility.

### Install

```bash
npm i --save-dev mock-fn
```

### Usage

```javascript
import { strict as assert } from "node:assert";

import mockFunction from "mock-fn";

it("should mock void function", () => {
  //given
  const voidFnMock = mockFunction();

  //when
  voidFnMock();

  //then
  assert.deepEqual(voidFnMock.times, 1);
});

it("should assert input params", () => {
  //given
  const fnMock = mockFunction((a, b) => {
    assert.deepEqual(a, 1);
    assert.deepEqual(b, 2);
    return 123;
  });

  //when
  const result = fnMock(1, 2);

  //then
  assert.deepEqual(result, 123);
  assert.deepEqual(fnMock.times, 1);
});

it("should return different results depending on number of calls", () => {
  //given
  const fnMock = mockFunction(() => {
    if (fnMock.times === 1) return 1;
    if (fnMock.times === 2) return 2;
    return 0;
  });

  //when & then
  assert.deepEqual(fnMock(), 1);
  assert.deepEqual(fnMock(), 2);
  assert.deepEqual(fnMock(), 0);
  assert.deepEqual(fnMock.times, 3);
});
```
