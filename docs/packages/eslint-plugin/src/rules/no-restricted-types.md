[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-restricted-types.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 12
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-restricted-types.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `objectReduceKey` | `../util` |


---

## Functions

### `removeSpaces(str: string): string`

<details><summary>Code</summary>

```ts
function removeSpaces(str: string): string {
  return str.replaceAll(/\s/g, '');
}
```
</details>

- **Parameters**:
  - `str: string`
- **Return Type**: `string`
- **Calls**:
  - `str.replaceAll`
### `stringifyNode(node: TSESTree.Node, sourceCode: TSESLint.SourceCode): string`

<details><summary>Code</summary>

```ts
function stringifyNode(
  node: TSESTree.Node,
  sourceCode: TSESLint.SourceCode,
): string {
  return removeSpaces(sourceCode.getText(node));
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `sourceCode: TSESLint.SourceCode`
- **Return Type**: `string`
- **Calls**:
  - `removeSpaces`
  - `sourceCode.getText`
### `getCustomMessage(bannedType: string | true | { fixWith?: string; message?: string } | null): string`

<details><summary>Code</summary>

```ts
function getCustomMessage(
  bannedType: string | true | { fixWith?: string; message?: string } | null,
): string {
  if (!bannedType || bannedType === true) {
    return '';
  }

  if (typeof bannedType === 'string') {
    return ` ${bannedType}`;
  }

  if (bannedType.message) {
    return ` ${bannedType.message}`;
  }

  return '';
}
```
</details>

- **Parameters**:
  - `bannedType: string | true | { fixWith?: string; message?: string } | null`
- **Return Type**: `string`
### `checkBannedTypes(typeNode: TSESTree.Node, name: string): void`

<details><summary>Code</summary>

```ts
function checkBannedTypes(
      typeNode: TSESTree.Node,
      name = stringifyNode(typeNode, context.sourceCode),
    ): void {
      const bannedType = bannedTypes.get(name);

      if (bannedType == null || bannedType === false) {
        return;
      }

      const customMessage = getCustomMessage(bannedType);
      const fixWith =
        bannedType && typeof bannedType === 'object' && bannedType.fixWith;
      const suggest =
        bannedType && typeof bannedType === 'object'
          ? bannedType.suggest
          : undefined;

      context.report({
        node: typeNode,
        messageId: 'bannedTypeMessage',
        data: {
          name,
          customMessage,
        },
        fix: fixWith
          ? (fixer): TSESLint.RuleFix => fixer.replaceText(typeNode, fixWith)
          : null,
        suggest: suggest?.map(replacement => ({
          messageId: 'bannedTypeReplacement',
          data: {
            name,
            replacement,
          },
          fix: (fixer): TSESLint.RuleFix =>
            fixer.replaceText(typeNode, replacement),
        })),
      });
    }
```
</details>

- **Parameters**:
  - `typeNode: TSESTree.Node`
  - `name: string`
- **Return Type**: `void`
- **Calls**:
  - `bannedTypes.get`
  - `getCustomMessage`
  - `context.report`
  - `fixer.replaceText`
  - `suggest?.map`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
            fixer.replaceText(typeNode, replacement)
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
            fixer.replaceText(typeNode, replacement)
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
            fixer.replaceText(typeNode, replacement)
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
            fixer.replaceText(typeNode, replacement)
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
            fixer.replaceText(typeNode, replacement)
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
            fixer.replaceText(typeNode, replacement)
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
            fixer.replaceText(typeNode, replacement)
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
            fixer.replaceText(typeNode, replacement)
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

### `Types`

```ts
type Types = Record<
  string,
  | boolean
  | string
  | {
      fixWith?: string;
      message: string;
      suggest?: readonly string[];
    }
  | null
>;
```

### `Options`

```ts
type Options = [
  {
    types?: Types;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'bannedTypeMessage' | 'bannedTypeReplacement';
```


---