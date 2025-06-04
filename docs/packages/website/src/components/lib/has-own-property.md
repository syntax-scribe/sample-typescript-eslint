[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `has-own-property.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

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