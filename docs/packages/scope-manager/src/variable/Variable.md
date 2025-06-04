[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Variable.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/variable/Variable.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `VariableBase` | `./VariableBase` |


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