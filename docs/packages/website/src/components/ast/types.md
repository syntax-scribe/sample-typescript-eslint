[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `types.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/website/src/components/ast/types.ts`**


---

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