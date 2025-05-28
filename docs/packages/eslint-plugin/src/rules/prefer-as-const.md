[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-as-const.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 13 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-as-const.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Functions

### `compareTypes(valueNode: TSESTree.Expression, typeNode: TSESTree.TypeNode, canFix: boolean): void`

<details><summary>Code</summary>

```ts
function compareTypes(
      valueNode: TSESTree.Expression,
      typeNode: TSESTree.TypeNode,
      canFix: boolean,
    ): void {
      if (
        valueNode.type === AST_NODE_TYPES.Literal &&
        typeNode.type === AST_NODE_TYPES.TSLiteralType &&
        typeNode.literal.type === AST_NODE_TYPES.Literal &&
        valueNode.raw === typeNode.literal.raw
      ) {
        if (canFix) {
          context.report({
            node: typeNode,
            messageId: 'preferConstAssertion',
            fix: fixer => fixer.replaceText(typeNode, 'const'),
          });
        } else {
          context.report({
            node: typeNode,
            messageId: 'variableConstAssertion',
            suggest: [
              {
                messageId: 'variableSuggest',
                fix: (fixer): TSESLint.RuleFix[] => [
                  fixer.remove(typeNode.parent),
                  fixer.insertTextAfter(valueNode, ' as const'),
                ],
              },
            ],
          });
        }
      }
    }
```
</details>

- **Parameters**:
  - `valueNode: TSESTree.Expression`
  - `typeNode: TSESTree.TypeNode`
  - `canFix: boolean`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `fixer.replaceText`
  - `fixer.remove`
  - `fixer.insertTextAfter`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(typeNode, 'const')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(typeNode, 'const')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => [
                  fixer.remove(typeNode.parent),
                  fixer.insertTextAfter(valueNode, ' as const'),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => [
                  fixer.remove(typeNode.parent),
                  fixer.insertTextAfter(valueNode, ' as const'),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => [
                  fixer.remove(typeNode.parent),
                  fixer.insertTextAfter(valueNode, ' as const'),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => [
                  fixer.remove(typeNode.parent),
                  fixer.insertTextAfter(valueNode, ' as const'),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(typeNode, 'const')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(typeNode, 'const')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => [
                  fixer.remove(typeNode.parent),
                  fixer.insertTextAfter(valueNode, ' as const'),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => [
                  fixer.remove(typeNode.parent),
                  fixer.insertTextAfter(valueNode, ' as const'),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => [
                  fixer.remove(typeNode.parent),
                  fixer.insertTextAfter(valueNode, ' as const'),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => [
                  fixer.remove(typeNode.parent),
                  fixer.insertTextAfter(valueNode, ' as const'),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`

---