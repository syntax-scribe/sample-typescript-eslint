[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `NoInfer.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/utils/src/ts-utils/NoInfer.ts`**

## Type Aliases

### `NoInfer<A>`

/**
 * We could use NoInfer typescript build-in utility
 * introduced in typescript 5.4, however at the moment of creation
 * the supported ts versions are >=4.8.4 <5.7.0
 * so for the moment we have to stick to this polyfill.
 *
 * @see https://github.com/millsp/ts-toolbelt/blob/master/sources/Function/NoInfer.ts
 */

```ts
type NoInfer<A> = [A][A extends unknown ? 0 : never];
```


---