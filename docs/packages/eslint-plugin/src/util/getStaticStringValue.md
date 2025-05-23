[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getStaticStringValue.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getStaticStringValue.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `isNullLiteral` | `./isNullLiteral` |


---

## Functions

### `getStaticStringValue(node: TSESTree.Node): string | null`

<details><summary>Code</summary>

```ts
export function getStaticStringValue(node: TSESTree.Node): string | null {
  switch (node.type) {
    case AST_NODE_TYPES.Literal:
      // eslint-disable-next-line eqeqeq, @typescript-eslint/internal/eqeq-nullish -- intentional strict comparison for literal value
      if (node.value === null) {
        if (isNullLiteral(node)) {
          return String(node.value); // "null"
        }
        if ('regex' in node) {
          return `/${node.regex.pattern}/${node.regex.flags}`;
        }

        if ('bigint' in node) {
          return node.bigint;
        }

        // Otherwise, this is an unknown literal. The function will return null.
      } else {
        return String(node.value);
      }
      break;

    case AST_NODE_TYPES.TemplateLiteral:
      if (node.expressions.length === 0 && node.quasis.length === 1) {
        return node.quasis[0].value.cooked;
      }
      break;

    // no default
  }

  return null;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns the result of the string conversion applied to the evaluated value of the given expression node,
 * if it can be determined statically.
 *
 * This function returns a `string` value for all `Literal` nodes and simple `TemplateLiteral` nodes only.
 * In all other cases, this function returns `null`.
 * @param node Expression node.
 * @returns String value if it can be determined. Otherwise, `null`.
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `string | null`
- **Calls**:
  - `isNullLiteral (from ./isNullLiteral)`
  - `String`
- **Internal Comments**:
```
// eslint-disable-next-line eqeqeq, @typescript-eslint/internal/eqeq-nullish -- intentional strict comparison for literal value
```


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---