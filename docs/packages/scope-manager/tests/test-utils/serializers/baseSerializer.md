[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `baseSerializer.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/test-utils/serializers/baseSerializer.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `NewPlugin` | `@vitest/pretty-format` |


---

## Functions

### `createSerializer(type: Constructor, keys: (keyof InstanceType<Constructor>)[]): NewPlugin`

<details><summary>Code</summary>

```ts
export function createSerializer<Constructor extends ConstructorSignature>(
  type: Constructor,
  keys: (keyof InstanceType<Constructor>)[],
): NewPlugin;
```
</details>

- **Parameters**:
  - `type: Constructor`
  - `keys: (keyof InstanceType<Constructor>)[]`
- **Return Type**: `NewPlugin`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `ConstructorSignature`

```ts
type ConstructorSignature = new (...args: never) => unknown;
```


---