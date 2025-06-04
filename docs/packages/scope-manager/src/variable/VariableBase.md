[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `VariableBase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/variable/VariableBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `Definition` | `../definition` |
| `Reference` | `../referencer/Reference` |
| `Scope` | `../scope` |
| `createIdGenerator` | `../ID` |


---

## Classes

### `VariableBase`

<details><summary>Class Code</summary>

```ts
export class VariableBase {
  /**
   * A unique ID for this instance - primarily used to help debugging and testing
   */
  public readonly $id: number = generator();

  /**
   * The array of the definitions of this variable.
   * @public
   */
  public readonly defs: Definition[] = [];
  /**
   * True if the variable is considered used for the purposes of `no-unused-vars`, false otherwise.
   * @public
   */
  public eslintUsed = false;
  /**
   * The array of `Identifier` nodes which define this variable.
   * If this variable is redeclared, this array includes two or more nodes.
   * @public
   */
  public readonly identifiers: TSESTree.Identifier[] = [];
  /**
   * The variable name, as given in the source code.
   * @public
   */
  public readonly name: string;
  /**
   * List of {@link Reference} of this variable (excluding parameter entries)  in its defining scope and all nested scopes.
   * For defining occurrences only see {@link Variable#defs}.
   * @public
   */
  public readonly references: Reference[] = [];
  /**
   * Reference to the enclosing Scope.
   */
  public readonly scope: Scope;

  constructor(name: string, scope: Scope) {
    this.name = name;
    this.scope = scope;
  }
}
```
</details>


---