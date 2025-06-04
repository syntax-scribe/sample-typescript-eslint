[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/typed-this/fixture.ts`**

## Interfaces

### `UIElement`

<details><summary>Interface Code</summary>

```ts
interface UIElement {
  addClickListener(onclick: (this: void, e: Event) => void): void;
}
```
</details>


---