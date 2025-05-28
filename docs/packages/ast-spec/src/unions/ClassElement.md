[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ClassElement.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 8 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

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

## 🔧 Functions

> No functions found in this file.


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