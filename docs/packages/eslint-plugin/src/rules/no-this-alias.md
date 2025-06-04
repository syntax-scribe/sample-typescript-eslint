[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-this-alias.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📊 Variables & Constants | 2 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-this-alias.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `id` | `any` | const | `node.type === AST_NODE_TYPES.VariableDeclarator ? node.id : node.left` | ✗ |
| `hasAllowedName` | `any` | const | `id.type === AST_NODE_TYPES.Identifier
            ? // https://github.com/typescript-eslint/typescript-eslint/issues/5439
              // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
              allowedNames!.includes(id.name)
            : false` | ✗ |


---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    allowDestructuring?: boolean;
    allowedNames?: string[];
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'thisAssignment' | 'thisDestructure';
```


---