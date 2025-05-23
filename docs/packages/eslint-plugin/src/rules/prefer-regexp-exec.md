[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-regexp-exec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 52
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-regexp-exec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `getStaticValue` | `../util` |
| `getTypeName` | `../util` |
| `getWrappingFixer` | `../util` |
| `isStaticMemberAccessOfValue` | `../util` |


---

## Functions

### `isStringType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isStringType(type: ts.Type): boolean {
      return getTypeName(checker, type) === 'string';
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if a given node type is a string.
     * @param type The node type to check.
     */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `getTypeName (from ../util)`
### `isRegExpType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isRegExpType(type: ts.Type): boolean {
      return getTypeName(checker, type) === 'RegExp';
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if a given node type is a RegExp.
     * @param type The node type to check.
     */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `getTypeName (from ../util)`
### `collectArgumentTypes(types: ts.Type[]): ArgumentType`

<details><summary>Code</summary>

```ts
function collectArgumentTypes(types: ts.Type[]): ArgumentType {
      let result = ArgumentType.Other;

      for (const type of types) {
        if (isRegExpType(type)) {
          result |= ArgumentType.RegExp;
        } else if (isStringType(type)) {
          result |= ArgumentType.String;
        }
      }

      return result;
    }
```
</details>

- **Parameters**:
  - `types: ts.Type[]`
- **Return Type**: `ArgumentType`
- **Calls**:
  - `isRegExpType`
  - `isStringType`
### `definitelyDoesNotContainGlobalFlag(node: TSESTree.CallExpressionArgument): boolean`

<details><summary>Code</summary>

```ts
function definitelyDoesNotContainGlobalFlag(
      node: TSESTree.CallExpressionArgument,
    ): boolean {
      if (
        (node.type === AST_NODE_TYPES.CallExpression ||
          node.type === AST_NODE_TYPES.NewExpression) &&
        node.callee.type === AST_NODE_TYPES.Identifier &&
        node.callee.name === 'RegExp'
      ) {
        const flags = node.arguments.at(1);
        return !(
          flags?.type === AST_NODE_TYPES.Literal &&
          typeof flags.value === 'string' &&
          flags.value.includes('g')
        );
      }

      return false;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Returns true if and only if we have syntactic proof that the /g flag is
     * absent. Returns false in all other cases (i.e. it still might or might
     * not contain the global flag).
     */
```

- **Parameters**:
  - `node: TSESTree.CallExpressionArgument`
- **Return Type**: `boolean`
- **Calls**:
  - `node.arguments.at`
  - `flags.value.includes`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string): string`

<details><summary>Code</summary>

```ts
objectCode => `${regExp.toString()}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `${argumentCode}.exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`
### `wrap(objectCode: string, argumentCode: string): string`

<details><summary>Code</summary>

```ts
(objectCode, argumentCode) =>
                  `RegExp(${argumentCode}).exec(${objectCode})`
```
</details>

- **Parameters**:
  - `objectCode: string`
  - `argumentCode: string`
- **Return Type**: `string`

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