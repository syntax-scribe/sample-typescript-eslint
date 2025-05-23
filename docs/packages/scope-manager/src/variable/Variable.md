[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Variable.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 1
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/variable/Variable.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `VariableBase` | `./VariableBase` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

### `Variable`

<details><summary>Class Code</summary>

```ts
export class Variable extends VariableBase {
  /**
   * `true` if the variable is valid in a type context, false otherwise
   * @public
   */
  public get isTypeVariable(): boolean {
    if (this.defs.length === 0) {
      // we don't statically know whether this is a type or a value
      return true;
    }

    return this.defs.some(def => def.isTypeDefinition);
  }

  /**
   * `true` if the variable is valid in a value context, false otherwise
   * @public
   */
  public get isValueVariable(): boolean {
    if (this.defs.length === 0) {
      // we don't statically know whether this is a type or a value
      return true;
    }

    return this.defs.some(def => def.isVariableDefinition);
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