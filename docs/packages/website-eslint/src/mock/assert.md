[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `assert.js`

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 1
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website-eslint/src/mock/assert.js`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `fail(actual: any, expected: any, message: any, operator: any, stackStartFunction: any): void`

<details><summary>Code</summary>

```ts
function fail(actual, expected, message, operator, stackStartFunction) {
  throw new AssertionError({
    actual,
    expected,
    message,
    operator,
    stackStartFunction,
  });
}
```
</details>

- **Parameters**:
  - `actual: any`
  - `expected: any`
  - `message: any`
  - `operator: any`
  - `stackStartFunction: any`
- **Return Type**: `void`
### `assert(value: any, message: any): void`

<details><summary>Code</summary>

```ts
function assert(value, message) {
  if (!value) {
    fail(value, true, message, '==', assert);
  }
}
```
</details>

- **Parameters**:
  - `value: any`
  - `message: any`
- **Return Type**: `void`
- **Calls**:
  - `fail`

---

## Classes

### `AssertionError`

<details><summary>Class Code</summary>

```ts
class AssertionError extends Error {
  constructor(options) {
    super(options);

    this.actual = options.actual;
    this.expected = options.expected;
    this.operator = options.operator;
    if (options.message) {
      this.message = options.message;
      this.generatedMessage = false;
    } else {
      this.message = '';
      this.generatedMessage = true;
    }
    const stackStartFunction = options.stackStartFunction || fail;
    if (Error.captureStackTrace) {
      Error.captureStackTrace(this, stackStartFunction);
    } else {
      // non v8 browsers so we can have a stacktrace
      const err = new Error();
      if (err.stack) {
        let out = err.stack;

        // try to strip useless frames
        const fn_name =
          typeof stackStartFunction === 'function'
            ? stackStartFunction.name
            : stackStartFunction.toString();
        const idx = out.indexOf(`\n${fn_name}`);
        if (idx >= 0) {
          // once we have located the function frame
          // we need to strip out everything before it (and its line)
          const next_line = out.indexOf('\n', idx + 1);
          out = out.substring(next_line + 1);
        }

        this.stack = out;
      }
    }
  }
}
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---