[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `ast-node-types.test-d.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📑 Type Aliases | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/ast-node-types.test-d.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../src/ast-node-types` |
| `Node` | `../src/unions/Node` |


---

## Type Aliases

### `GetKeys<T extends AST_NODE_TYPES extends AST_NODE_TYPES>`

```ts
type GetKeys<T extends AST_NODE_TYPES extends AST_NODE_TYPES> = keyof Extract<Node, { type: T }>;
```

### `AllKeys`

```ts
type AllKeys = {
  readonly [T in AST_NODE_TYPES]: GetKeys<T>;
};
```

### `TakesString<T extends Record<string, string> extends Record<string, string>>`

```ts
type TakesString<T extends Record<string, string> extends Record<string, string>> = T;
```

### `_Test`

```ts
type _Test = TakesString<AllKeys> | void;
```


---