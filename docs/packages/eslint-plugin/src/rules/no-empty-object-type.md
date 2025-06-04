[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-empty-object-type.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 33 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 4 |
| 📑 Type Aliases | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-empty-object-type.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `allowWithNameTester` | `RegExp` | const | `allowWithName
      ? new RegExp(allowWithName, 'u')
      : undefined` | ✗ |
| `extend` | `any` | const | `node.extends` | ✗ |
| `typeParam` | `any` | const | `node.typeParameters
                      ? context.sourceCode.getText(node.typeParameters)
                      : ''` | ✗ |
| `typeParam` | `any` | const | `node.typeParameters
                      ? context.sourceCode.getText(node.typeParameters)
                      : ''` | ✗ |


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