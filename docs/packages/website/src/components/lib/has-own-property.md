[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `has-own-property.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/components/lib/has-own-property.ts`**

## Functions

### `hasOwnProperty(property: Key, object: Container): object is Container & Record<Key, unknown>`

<details><summary>Code</summary>

```ts
export function hasOwnProperty<
  Container extends object,
  Key extends PropertyKey,
>(
  property: Key,
  object: Container,
): object is Container & Record<Key, unknown> {
  return property in object;
}
```
</details>

- **Parameters**:
  - `property: Key`
  - `object: Container`
- **Return Type**: `object is Container & Record<Key, unknown>`

---