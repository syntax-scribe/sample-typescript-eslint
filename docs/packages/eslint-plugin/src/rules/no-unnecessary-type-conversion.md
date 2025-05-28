[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unnecessary-type-conversion.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 178 |
| 🧱 Classes | 0 |
| 📦 Imports | 9 |
| 📊 Variables & Constants | 11 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unnecessary-type-conversion.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleFix` | `@typescript-eslint/utils/ts-eslint` |
| `RuleFixer` | `@typescript-eslint/utils/ts-eslint` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `getWrappingFixer` | `../util` |
| `isTypeFlagSet` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `outerNode` | `any` | const | `isDoubleOperator ? node.parent : node` | ✗ |
| `wrappingFixerParams` | `{ node: any; innerNode: any[]; sourceCode: any; }` | const | `{
          node: outerNode,
          innerNode: [node.argument],
          sourceCode: context.sourceCode,
        }` | ✗ |
| `wrappingFixerParams` | `{ node: TSESTree.AssignmentExpression; innerNode: any[]; sourceCode: any; }` | const | `{
            node,
            innerNode: [node.left],
            sourceCode: context.sourceCode,
          }` | ✗ |
| `wrappingFixerParams` | `{ node: TSESTree.BinaryExpression; innerNode: any[]; sourceCode: any; }` | const | `{
            node,
            innerNode: [node.left],
            sourceCode: context.sourceCode,
          }` | ✗ |
| `wrappingFixerParams` | `{ node: TSESTree.BinaryExpression; innerNode: any[]; sourceCode: any; }` | const | `{
            node,
            innerNode: [node.right],
            sourceCode: context.sourceCode,
          }` | ✗ |
| `nodeCallee` | `any` | const | `node.callee` | ✗ |
| `builtInTypeFlags` | `{ BigInt: any; Boolean: any; Number: any; String: any; }` | const | `{
          BigInt: ts.TypeFlags.BigIntLike,
          Boolean: ts.TypeFlags.BooleanLike,
          Number: ts.TypeFlags.NumberLike,
          String: ts.TypeFlags.StringLike,
        }` | ✗ |
| `typeFlag` | `any` | const | `builtInTypeFlags[nodeCallee.name as keyof typeof builtInTypeFlags]` | ✗ |
| `wrappingFixerParams` | `{ node: TSESTree.CallExpression; innerNode: any[]; sourceCode: any; }` | const | `{
          node,
          innerNode: [node.arguments[0]],
          sourceCode: context.sourceCode,
        }` | ✗ |
| `memberExpr` | `TSESTree.MemberExpression` | const | `node.parent as TSESTree.MemberExpression` | ✗ |
| `wrappingFixerParams` | `{ node: any; innerNode: any[]; sourceCode: any; }` | const | `{
            node: memberExpr.parent,
            innerNode: [memberExpr.object],
            sourceCode: context.sourceCode,
          }` | ✗ |


---

## Functions

### `doesUnderlyingTypeMatchFlag(type: ts.Type, typeFlag: ts.TypeFlags): boolean`

<details><summary>Code</summary>

```ts
function doesUnderlyingTypeMatchFlag(
      type: ts.Type,
      typeFlag: ts.TypeFlags,
    ): boolean {
      return tsutils
        .unionConstituents(type)
        .every(t => isTypeFlagSet(t, typeFlag));
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `typeFlag: ts.TypeFlags`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils
        .unionConstituents(type)
        .every`
  - `isTypeFlagSet (from ../util)`
### `handleUnaryOperator(node: TSESTree.UnaryExpression, typeFlag: ts.TypeFlags, typeString: 'boolean' | 'number', violation: string, isDoubleOperator: boolean): void`

<details><summary>Code</summary>

```ts
function handleUnaryOperator(
      node: TSESTree.UnaryExpression,
      typeFlag: ts.TypeFlags,
      typeString: 'boolean' | 'number',
      violation: string,
      isDoubleOperator: boolean, // !! or ~~
    ) {
      const outerNode = isDoubleOperator ? node.parent : node;
      const type = services.getTypeAtLocation(node.argument);
      if (doesUnderlyingTypeMatchFlag(type, typeFlag)) {
        const wrappingFixerParams = {
          node: outerNode,
          innerNode: [node.argument],
          sourceCode: context.sourceCode,
        };

        context.report({
          loc: {
            start: outerNode.loc.start,
            end: {
              column: node.loc.start.column + 1,
              line: node.loc.start.line,
            },
          },
          messageId: 'unnecessaryTypeConversion',
          data: { type: typeString, violation },
          suggest: [
            {
              messageId: 'suggestRemove',
              fix: getWrappingFixer(wrappingFixerParams),
            },
            {
              messageId: 'suggestSatisfies',
              data: { type: typeString },
              fix: getWrappingFixer({
                ...wrappingFixerParams,
                wrap: expr => `${expr} satisfies ${typeString}`,
              }),
            },
          ],
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.UnaryExpression`
  - `typeFlag: ts.TypeFlags`
  - `typeString: 'boolean' | 'number'`
  - `violation: string`
  - `isDoubleOperator: boolean`
- **Return Type**: `void`
- **Calls**:
  - `services.getTypeAtLocation`
  - `doesUnderlyingTypeMatchFlag`
  - `context.report`
  - `getWrappingFixer (from ../util)`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies ${typeString}`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`
### `wrap(expr: string): string`

<details><summary>Code</summary>

```ts
expr => `${expr} satisfies string`
```
</details>

- **Parameters**:
  - `expr: string`
- **Return Type**: `string`

---

## Type Aliases

### `Options`

```ts
type Options = [];
```

### `MessageIds`

```ts
type MessageIds = | 'suggestRemove'
  | 'suggestSatisfies'
  | 'unnecessaryTypeConversion';
```


---