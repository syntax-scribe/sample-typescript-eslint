[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `literal-type3.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/literal-type3.ts`**

## Functions

### `setAlignment(value: `${VerticalAlignment}-${HorizontalAlignment}`): void`

<details><summary>Code</summary>

```ts
declare function setAlignment(
  value: `${VerticalAlignment}-${HorizontalAlignment}`,
): void;
```
</details>

- **Parameters**:
  - `value: `${VerticalAlignment}-${HorizontalAlignment}``
- **Return Type**: `void`

---

## Type Aliases

### `VerticalAlignment`

```ts
type VerticalAlignment = 'top' | 'middle' | 'bottom';
```

### `HorizontalAlignment`

```ts
type HorizontalAlignment = 'left' | 'center' | 'right';
```


---