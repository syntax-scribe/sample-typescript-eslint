[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-confusing-non-null-assertion.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 27
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-confusing-non-null-assertion.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `ReportDescriptor` | `@typescript-eslint/utils/ts-eslint` |
| `RuleFix` | `@typescript-eslint/utils/ts-eslint` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Functions

### `isConfusingOperator(operator: string): operator is ConfusingOperator`

<details><summary>Code</summary>

```ts
function isConfusingOperator(operator: string): operator is ConfusingOperator {
  return confusingOperators.has(operator as ConfusingOperator);
}
```
</details>

- **Parameters**:
  - `operator: string`
- **Return Type**: `operator is ConfusingOperator`
- **Calls**:
  - `confusingOperators.has`
### `confusingOperatorToMessageData(operator: ConfusingOperator): Pick<ReportDescriptor<MessageId>, 'data' | 'messageId'>`

<details><summary>Code</summary>

```ts
function confusingOperatorToMessageData(
      operator: ConfusingOperator,
    ): Pick<ReportDescriptor<MessageId>, 'data' | 'messageId'> {
      switch (operator) {
        case '=':
          return {
            messageId: 'confusingAssign',
          };
        case '==':
        case '===':
          return {
            messageId: 'confusingEqual',
          };
        case 'in':
        case 'instanceof':
          return {
            messageId: 'confusingOperator',
            data: { operator },
          };
        // istanbul ignore next
        default:
          operator satisfies never;
          throw new Error(`Unexpected operator ${operator as string}`);
      }
    }
```
</details>

- **Parameters**:
  - `operator: ConfusingOperator`
- **Return Type**: `Pick<ReportDescriptor<MessageId>, 'data' | 'messageId'>`
- **Internal Comments**:
```
// istanbul ignore next
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => fixer.remove(leftHandFinalToken)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.remove`
### `wrapUpLeftFixer(node: TSESTree.AssignmentExpression | TSESTree.BinaryExpression): TSESLint.ReportFixFunction`

<details><summary>Code</summary>

```ts
function wrapUpLeftFixer(
  node: TSESTree.AssignmentExpression | TSESTree.BinaryExpression,
): TSESLint.ReportFixFunction {
  return (fixer): TSESLint.RuleFix[] => [
    fixer.insertTextBefore(node.left, '('),
    fixer.insertTextAfter(node.left, ')'),
  ];
}
```
</details>

- **Parameters**:
  - `node: TSESTree.AssignmentExpression | TSESTree.BinaryExpression`
- **Return Type**: `TSESLint.ReportFixFunction`
- **Calls**:
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `MessageId`

```ts
type MessageId = | 'confusingAssign'
  | 'confusingEqual'
  | 'confusingOperator'
  | 'notNeedInAssign'
  | 'notNeedInEqualTest'
  | 'notNeedInOperator'
  | 'wrapUpLeft';
```

### `ConfusingOperator`

```ts
type ConfusingOperator = typeof confusingOperators extends Set<infer T> ? T : never;
```


---