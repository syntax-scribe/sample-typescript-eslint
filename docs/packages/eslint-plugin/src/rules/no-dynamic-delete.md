[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-dynamic-delete.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
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