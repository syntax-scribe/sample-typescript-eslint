[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unnecessary-type-constraint.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 2 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unnecessary-type-constraint.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `extname` | `node:path` |
| `MakeRequired` | `../util` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `unnecessaryConstraints` | `Map<any, string>` | const | `new Map([
      [AST_NODE_TYPES.TSAnyKeyword, 'any'],
      [AST_NODE_TYPES.TSUnknownKeyword, 'unknown'],
    ])` | ✗ |
| `pathExt` | `ts.Extension` | const | `extname(filename).toLocaleLowerCase() as ts.Extension` | ✗ |


---

## Functions

### `checkRequiresGenericDeclarationDisambiguation(filename: string): boolean`

<details><summary>Code</summary>

```ts
function checkRequiresGenericDeclarationDisambiguation(
      filename: string,
    ): boolean {
      const pathExt = extname(filename).toLocaleLowerCase() as ts.Extension;
      switch (pathExt) {
        case ts.Extension.Cts:
        case ts.Extension.Mts:
        case ts.Extension.Tsx:
          return true;

        default:
          return false;
      }
    }
```
</details>

- **Parameters**:
  - `filename: string`
- **Return Type**: `boolean`
- **Calls**:
  - `extname(filename).toLocaleLowerCase`
### `checkNode(node: TypeParameterWithConstraint, inArrowFunction: boolean): void`

<details><summary>Code</summary>

```ts
(
      node: TypeParameterWithConstraint,
      inArrowFunction: boolean,
    ): void => {
      const constraint = unnecessaryConstraints.get(node.constraint.type);
      function shouldAddTrailingComma(): boolean {
        if (!inArrowFunction || !requiresGenericDeclarationDisambiguation) {
          return false;
        }
        // Only <T>() => {} would need trailing comma
        return (
          (node.parent as TSESTree.TSTypeParameterDeclaration).params.length ===
            1 &&
          context.sourceCode.getTokensAfter(node)[0].value !== ',' &&
          !node.default
        );
      }

      if (constraint) {
        context.report({
          node,
          messageId: 'unnecessaryConstraint',
          data: {
            name: node.name.name,
            constraint,
          },
          suggest: [
            {
              messageId: 'removeUnnecessaryConstraint',
              data: {
                constraint,
              },
              fix(fixer): TSESLint.RuleFix | null {
                return fixer.replaceTextRange(
                  [node.name.range[1], node.constraint.range[1]],
                  shouldAddTrailingComma() ? ',' : '',
                );
              },
            },
          ],
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TypeParameterWithConstraint`
  - `inArrowFunction: boolean`
- **Return Type**: `void`
- **Calls**:
  - `unnecessaryConstraints.get`
  - `context.sourceCode.getTokensAfter`
  - `context.report`
  - `fixer.replaceTextRange`
  - `shouldAddTrailingComma`
- **Internal Comments**:
```
// Only <T>() => {} would need trailing comma
```

### `shouldAddTrailingComma(): boolean`

<details><summary>Code</summary>

```ts
function shouldAddTrailingComma(): boolean {
        if (!inArrowFunction || !requiresGenericDeclarationDisambiguation) {
          return false;
        }
        // Only <T>() => {} would need trailing comma
        return (
          (node.parent as TSESTree.TSTypeParameterDeclaration).params.length ===
            1 &&
          context.sourceCode.getTokensAfter(node)[0].value !== ',' &&
          !node.default
        );
      }
```
</details>

- **Return Type**: `boolean`
- **Calls**:
  - `context.sourceCode.getTokensAfter`
- **Internal Comments**:
```
// Only <T>() => {} would need trailing comma
```


---

## Type Aliases

### `TypeParameterWithConstraint`

```ts
type TypeParameterWithConstraint = MakeRequired<
  TSESTree.TSTypeParameter,
  'constraint'
>;
```


---