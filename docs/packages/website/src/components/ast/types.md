[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `types.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/website/src/components/ast/types.ts`**

## Type Aliases

### `OnHoverNodeFn`

```ts
type OnHoverNodeFn = (node?: [number, number]) => void;
```

### `ParentNodeType`

```ts
type ParentNodeType = | 'esNode'
  | 'scope'
  | 'scopeDefinition'
  | 'scopeManager'
  | 'scopeReference'
  | 'scopeVariable'
  | 'tsNode'
  | 'tsSignature'
  | 'tsSymbol'
  | 'tsType'
  | undefined;
```


---