[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `errors.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 2 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/rule-schema-to-typescript-types/src/errors.ts`**


---

## Classes

### `NotSupportedError`

<details><summary>Class Code</summary>

```ts
export class NotSupportedError extends Error {
  constructor(thing: string, target: unknown) {
    super(
      `Generating a type for ${thing} is not currently supported:\n${JSON.stringify(
        target,
        null,
        2,
      )}`,
    );
  }
}
```
</details>

### `UnexpectedError`

<details><summary>Class Code</summary>

```ts
export class UnexpectedError extends Error {
  constructor(error: string, target: unknown) {
    super(`Unexpected Error: ${error}:\n${JSON.stringify(target, null, 2)}`);
  }
}
```
</details>


---