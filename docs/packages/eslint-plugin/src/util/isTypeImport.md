[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isTypeImport.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/isTypeImport.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Definition` | `@typescript-eslint/scope-manager` |
| `ImportBindingDefinition` | `@typescript-eslint/scope-manager` |
| `DefinitionType` | `@typescript-eslint/scope-manager` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Functions

### `isTypeImport(definition: Definition): definition is ImportBindingDefinition`

<details><summary>Code</summary>

```ts
export function isTypeImport(
  definition?: Definition,
): definition is ImportBindingDefinition {
  return (
    definition?.type === DefinitionType.ImportBinding &&
    (definition.parent.importKind === 'type' ||
      (definition.node.type === AST_NODE_TYPES.ImportSpecifier &&
        definition.node.importKind === 'type'))
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Determine whether a variable definition is a type import. e.g.:
 *
 * ```ts
 * import type { Foo } from 'foo';
 * import { type Bar } from 'bar';
 * ```
 *
 * @param definition - The variable definition to check.
 */
```

- **Parameters**:
  - `definition: Definition`
- **Return Type**: `definition is ImportBindingDefinition`

---