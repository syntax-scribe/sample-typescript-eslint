[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `TSESTreeNode.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 3 |
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
📂 **`packages/scope-manager/tests/test-utils/serializers/TSESTreeNode.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `NewPlugin` | `@vitest/pretty-format` |
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `createIdGenerator` | `../../../src/ID` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `EXCLUDED_KEYS` | `Set<string>` | const | `new Set([
  // prevent cycles
  'parent',
  // type is printed in front of the object
  'type',
  // locations are just noise
  'loc',
  'range',
])` | ✗ |
| `SEEN_NODES` | `Map<Node, number>` | const | `new Map<Node, number>()` | ✗ |
| `serializer` | `NewPlugin` | const | `{
  serialize(node: Node): string {
    if (node.type === AST_NODE_TYPES.Identifier) {
      return `Identifier<"${(node as Identifier).name}">`;
    }

    const keys = Object.keys(node).filter(k => !EXCLUDED_KEYS.has(k));
    if (keys.length === 0) {
      return node.type;
    }

    if (SEEN_NODES.has(node)) {
      return `${node.type}$${SEEN_NODES.get(node)}`;
    }

    const id = generator();
    SEEN_NODES.set(node, id);
    return `${node.type}$${id}`;
  },
  test(val): boolean {
    return !!(
      val &&
      typeof val === 'object' &&
      // make sure it's not one of the classes from the package
      Object.getPrototypeOf(val) === Object.prototype &&
      'type' in val &&
      (val as TSESTree.Node).type in AST_NODE_TYPES
    );
  },
}` | ✓ |


---

## Functions

### `serialize(node: Node): string`

<details><summary>Code</summary>

```ts
serialize(node: Node): string {
    if (node.type === AST_NODE_TYPES.Identifier) {
      return `Identifier<"${(node as Identifier).name}">`;
    }

    const keys = Object.keys(node).filter(k => !EXCLUDED_KEYS.has(k));
    if (keys.length === 0) {
      return node.type;
    }

    if (SEEN_NODES.has(node)) {
      return `${node.type}$${SEEN_NODES.get(node)}`;
    }

    const id = generator();
    SEEN_NODES.set(node, id);
    return `${node.type}$${id}`;
  }
```
</details>

- **Parameters**:
  - `node: Node`
- **Return Type**: `string`
- **Calls**:
  - `Object.keys(node).filter`
  - `EXCLUDED_KEYS.has`
  - `SEEN_NODES.has`
  - `SEEN_NODES.get`
  - `generator`
  - `SEEN_NODES.set`
### `test(val: any): boolean`

<details><summary>Code</summary>

```ts
test(val): boolean {
    return !!(
      val &&
      typeof val === 'object' &&
      // make sure it's not one of the classes from the package
      Object.getPrototypeOf(val) === Object.prototype &&
      'type' in val &&
      (val as TSESTree.Node).type in AST_NODE_TYPES
    );
  }
```
</details>

- **Parameters**:
  - `val: any`
- **Return Type**: `boolean`
- **Calls**:
  - `Object.getPrototypeOf`
- **Internal Comments**:
```
// make sure it's not one of the classes from the package (x4)
```


---

## Type Aliases

### `Node`

```ts
type Node = { type: AST_NODE_TYPES } & Record<string, unknown>;
```

### `Identifier`

```ts
type Identifier = { name: string; type: AST_NODE_TYPES.Identifier } & Node;
```


---