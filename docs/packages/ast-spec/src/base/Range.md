[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Range.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/Range.ts`**

## Type Aliases

### `Range`

/**
 * An array of two numbers.
 * Both numbers are a 0-based index which is the position in the array of source code characters.
 * The first is the start position of the node, the second is the end position of the node.
 */

```ts
type Range = [number, number];
```


---