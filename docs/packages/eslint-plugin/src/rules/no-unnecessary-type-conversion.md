[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unnecessary-type-conversion.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 178
- **Classes**: 0
- **Imports**: 9
- **Interfaces**: 0
- **Type Aliases**: 2

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


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