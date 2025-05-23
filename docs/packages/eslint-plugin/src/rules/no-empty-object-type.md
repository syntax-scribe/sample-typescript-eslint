[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-empty-object-type.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 33
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 4

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-empty-object-type.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Functions

### `noEmptyMessage(emptyType: string): string`

<details><summary>Code</summary>

```ts
(emptyType: string): string =>
  [
    `${emptyType} allows any non-nullish value, including literals like \`0\` and \`""\`.`,
    "- If that's what you want, disable this lint rule with an inline comment or configure the '{{ option }}' rule option.",
    '- If you want a type meaning "any object", you probably want `object` instead.',
    '- If you want a type meaning "any value", you probably want `unknown` instead.',
  ].join('\n')
```
</details>

- **Parameters**:
  - `emptyType: string`
- **Return Type**: `string`
- **Calls**:
  - `[
    `${emptyType} allows any non-nullish value, including literals like \`0\` and \`""\`.`,
    "- If that's what you want, disable this lint rule with an inline comment or configure the '{{ option }}' rule option.",
    '- If you want a type meaning "any object", you probably want `object` instead.',
    '- If you want a type meaning "any value", you probably want `unknown` instead.',
  ].join`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                fixer.replaceText(node, replacement)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `AllowInterfaces`

```ts
type AllowInterfaces = 'always' | 'never' | 'with-single-extends';
```

### `AllowObjectTypes`

```ts
type AllowObjectTypes = 'always' | 'never';
```

### `Options`

```ts
type Options = [
  {
    allowInterfaces?: AllowInterfaces;
    allowObjectTypes?: AllowObjectTypes;
    allowWithName?: string;
  },
];
```

### `MessageIds`

```ts
type MessageIds = | 'noEmptyInterface'
  | 'noEmptyInterfaceWithSuper'
  | 'noEmptyObject'
  | 'replaceEmptyInterface'
  | 'replaceEmptyInterfaceWithSuper'
  | 'replaceEmptyObjectType';
```


---