[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |
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

- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/UpdateExpression/fixtures/valid-assignment/fixture.ts`**

## Functions

### `F.m(): void`

<details><summary>Code</summary>

```ts
m() {
    this.#a++;
    this.m().a++;
    this[1] = 1;
    F++;
    // prettier-ignore
    (this.#a)++;
    (<number>this.#a)++;
    (this.#a satisfies number)++;
    (this.#a as number)++;
    this.#a!++;
  }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `this.m`
- **Internal Comments**:
```
// prettier-ignore (x3)
```


---

## Classes

### `F`

<details><summary>Class Code</summary>

```ts
class F {
  #a;

  m() {
    this.#a++;
    this.m().a++;
    this[1] = 1;
    F++;
    // prettier-ignore
    (this.#a)++;
    (<number>this.#a)++;
    (this.#a satisfies number)++;
    (this.#a as number)++;
    this.#a!++;
  }
}
```
</details>

#### Methods

##### `m(): void`

<details><summary>Code</summary>

```ts
m() {
    this.#a++;
    this.m().a++;
    this[1] = 1;
    F++;
    // prettier-ignore
    (this.#a)++;
    (<number>this.#a)++;
    (this.#a satisfies number)++;
    (this.#a as number)++;
    this.#a!++;
  }
```
</details>


---