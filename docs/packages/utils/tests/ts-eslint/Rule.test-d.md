[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Rule.test-d.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📑 Type Aliases | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/utils/tests/ts-eslint/Rule.test-d.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `RuleListener` | `../../src/ts-eslint` |


---

## Type Aliases

### `RuleListenerKeysWithoutIndexSignature`

```ts
type RuleListenerKeysWithoutIndexSignature = {
  [K in keyof RuleListener as string extends K ? never : K]: K;
};
```

### `RuleListenerSelectors`

```ts
type RuleListenerSelectors = NonNullable<
  RuleListenerKeysWithoutIndexSignature[keyof RuleListenerKeysWithoutIndexSignature]
>;
```

### `AllSelectors`

```ts
type AllSelectors = | `${TSESTree.AST_NODE_TYPES}:exit`
  | `${TSESTree.AST_NODE_TYPES}`;
```

### `SelectorsWithWrongNodeType`

```ts
type SelectorsWithWrongNodeType = {
  [K in TSESTree.AST_NODE_TYPES]: Parameters<
    NonNullable<RuleListener[K]>
  >[0]['type'] extends K
    ? K extends Parameters<NonNullable<RuleListener[K]>>[0]['type']
      ? never
      : K
    : K;
}[TSESTree.AST_NODE_TYPES];
```


---