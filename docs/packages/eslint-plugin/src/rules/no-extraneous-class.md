[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-extraneous-class.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 4 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-extraneous-class.ts`**

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
| `parent` | `any` | const | `node.parent` | ✗ |
| `reportNode` | `any` | const | `parent.type === AST_NODE_TYPES.ClassDeclaration && parent.id
            ? parent.id
            : parent` | ✗ |
| `onlyStatic` | `boolean` | let/var | `true` | ✗ |
| `onlyConstructor` | `boolean` | let/var | `true` | ✗ |


---

## Functions

### `isAllowWithDecorator(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression | undefined): boolean`

<details><summary>Code</summary>

```ts
(
      node: TSESTree.ClassDeclaration | TSESTree.ClassExpression | undefined,
    ): boolean => {
      return !!(
        allowWithDecorator &&
        node?.decorators &&
        node.decorators.length !== 0
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression | undefined`
- **Return Type**: `boolean`

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    allowConstructorOnly?: boolean;
    allowEmpty?: boolean;
    allowStaticOnly?: boolean;
    allowWithDecorator?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'empty' | 'onlyConstructor' | 'onlyStatic';
```


---