[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `computed-properties-in-interface.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/computed-properties-in-interface.ts`**

## Interfaces

### `A`

<details><summary>Interface Code</summary>

```ts
interface A {
  [s1]: number;
  [s2](s1: number, s2: number): number;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `[s1]` | `number` | ✗ |  |


---