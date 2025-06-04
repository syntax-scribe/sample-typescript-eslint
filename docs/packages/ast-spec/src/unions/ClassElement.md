[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ClassElement.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 8 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/ClassElement.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AccessorProperty` | `../element/AccessorProperty/spec` |
| `MethodDefinition` | `../element/MethodDefinition/spec` |
| `PropertyDefinition` | `../element/PropertyDefinition/spec` |
| `StaticBlock` | `../element/StaticBlock/spec` |
| `TSAbstractAccessorProperty` | `../element/TSAbstractAccessorProperty/spec` |
| `TSAbstractMethodDefinition` | `../element/TSAbstractMethodDefinition/spec` |
| `TSAbstractPropertyDefinition` | `../element/TSAbstractPropertyDefinition/spec` |
| `TSIndexSignature` | `../element/TSIndexSignature/spec` |


---

## Type Aliases

### `ClassElement`

```ts
type ClassElement = | AccessorProperty
  | MethodDefinition
  | PropertyDefinition
  | StaticBlock
  | TSAbstractAccessorProperty
  | TSAbstractMethodDefinition
  | TSAbstractPropertyDefinition
  | TSIndexSignature;
```


---