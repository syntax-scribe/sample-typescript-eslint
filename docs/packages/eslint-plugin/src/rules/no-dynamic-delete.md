[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-dynamic-delete.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 4
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-dynamic-delete.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Functions

### `createFixer(member: TSESTree.MemberExpression): TSESLint.ReportFixFunction | undefined`

<details><summary>Code</summary>

```ts
function createFixer(
      member: TSESTree.MemberExpression,
    ): TSESLint.ReportFixFunction | undefined {
      if (
        member.property.type === AST_NODE_TYPES.Literal &&
        typeof member.property.value === 'string'
      ) {
        return createPropertyReplacement(
          member.property,
          `.${member.property.value}`,
        );
      }

      return undefined;
    }
```
</details>

- **Parameters**:
  - `member: TSESTree.MemberExpression`
- **Return Type**: `TSESLint.ReportFixFunction | undefined`
- **Calls**:
  - `createPropertyReplacement`
### `createPropertyReplacement(property: TSESTree.Expression, replacement: string): (fixer: TSESLint.RuleFixer) => TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
function createPropertyReplacement(
      property: TSESTree.Expression,
      replacement: string,
    ) {
      return (fixer: TSESLint.RuleFixer): TSESLint.RuleFix =>
        fixer.replaceTextRange(getTokenRange(property), replacement);
    }
```
</details>

- **Parameters**:
  - `property: TSESTree.Expression`
  - `replacement: string`
- **Return Type**: `(fixer: TSESLint.RuleFixer) => TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceTextRange`
  - `getTokenRange`
### `getTokenRange(property: TSESTree.Expression): [number, number]`

<details><summary>Code</summary>

```ts
function getTokenRange(property: TSESTree.Expression): [number, number] {
      return [
        nullThrows(
          context.sourceCode.getTokenBefore(property),
          NullThrowsReasons.MissingToken('token before', 'property'),
        ).range[0],
        nullThrows(
          context.sourceCode.getTokenAfter(property),
          NullThrowsReasons.MissingToken('token after', 'property'),
        ).range[1],
      ];
    }
```
</details>

- **Parameters**:
  - `property: TSESTree.Expression`
- **Return Type**: `[number, number]`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenBefore`
  - `NullThrowsReasons.MissingToken`
  - `context.sourceCode.getTokenAfter`
### `isAcceptableIndexExpression(property: TSESTree.Expression): boolean`

<details><summary>Code</summary>

```ts
function isAcceptableIndexExpression(property: TSESTree.Expression): boolean {
  return (
    (property.type === AST_NODE_TYPES.Literal &&
      ['number', 'string'].includes(typeof property.value)) ||
    (property.type === AST_NODE_TYPES.UnaryExpression &&
      property.operator === '-' &&
      property.argument.type === AST_NODE_TYPES.Literal &&
      typeof property.argument.value === 'number')
  );
}
```
</details>

- **Parameters**:
  - `property: TSESTree.Expression`
- **Return Type**: `boolean`
- **Calls**:
  - `['number', 'string'].includes`

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