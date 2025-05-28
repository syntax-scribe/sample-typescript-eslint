[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-find.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 40 |
| 🧱 Classes | 0 |
| 📦 Imports | 12 |
| 📊 Variables & Constants | 6 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-find.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleFix` | `@typescript-eslint/utils/ts-eslint` |
| `Type` | `typescript` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `getStaticValue` | `../util` |
| `isStaticMemberAccessOfValue` | `../util` |
| `nullThrows` | `../util` |
| `skipChainExpression` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `callee` | `any` | const | `node.callee` | ✗ |
| `isBracketSyntaxForFilter` | `any` | const | `callee.computed` | ✗ |
| `filterNode` | `any` | const | `callee.property` | ✗ |
| `isAtLeastOneArrayishComponent` | `boolean` | let/var | `false` | ✗ |
| `callee` | `any` | const | `node.callee` | ✗ |
| `object` | `any` | const | `node.object` | ✗ |


---

## Functions

### `parseArrayFilterExpressions(expression: TSESTree.Expression): FilterExpressionData[]`

<details><summary>Code</summary>

```ts
function parseArrayFilterExpressions(
      expression: TSESTree.Expression,
    ): FilterExpressionData[] {
      const node = skipChainExpression(expression);

      if (node.type === AST_NODE_TYPES.SequenceExpression) {
        // Only the last expression in (a, b, [1, 2, 3].filter(condition))[0] matters
        const lastExpression = nullThrows(
          node.expressions.at(-1),
          'Expected to have more than zero expressions in a sequence expression',
        );
        return parseArrayFilterExpressions(lastExpression);
      }

      // This is the only reason we're returning a list rather than a single value.
      if (node.type === AST_NODE_TYPES.ConditionalExpression) {
        // Both branches of the ternary _must_ return results.
        const consequentResult = parseArrayFilterExpressions(node.consequent);
        if (consequentResult.length === 0) {
          return [];
        }

        const alternateResult = parseArrayFilterExpressions(node.alternate);
        if (alternateResult.length === 0) {
          return [];
        }

        // Accumulate the results from both sides and pass up the chain.
        return [...consequentResult, ...alternateResult];
      }

      // Check if it looks like <<stuff>>(...), but not <<stuff>>?.(...)
      if (node.type === AST_NODE_TYPES.CallExpression && !node.optional) {
        const callee = node.callee;
        // Check if it looks like <<stuff>>.filter(...) or <<stuff>>['filter'](...),
        // or the optional chaining variants.
        if (callee.type === AST_NODE_TYPES.MemberExpression) {
          const isBracketSyntaxForFilter = callee.computed;
          if (isStaticMemberAccessOfValue(callee, context, 'filter')) {
            const filterNode = callee.property;

            const filteredObjectType = getConstrainedTypeAtLocation(
              services,
              callee.object,
            );

            // As long as the object is a (possibly nullable) array,
            // this is an Array.prototype.filter expression.
            if (isArrayish(filteredObjectType)) {
              return [
                {
                  filterNode,
                  isBracketSyntaxForFilter,
                },
              ];
            }
          }
        }
      }

      // not a filter expression.
      return [];
    }
```
</details>

- **Parameters**:
  - `expression: TSESTree.Expression`
- **Return Type**: `FilterExpressionData[]`
- **Calls**:
  - `skipChainExpression (from ../util)`
  - `nullThrows (from ../util)`
  - `node.expressions.at`
  - `parseArrayFilterExpressions`
  - `isStaticMemberAccessOfValue (from ../util)`
  - `getConstrainedTypeAtLocation (from ../util)`
  - `isArrayish`
- **Internal Comments**:
```
// Only the last expression in (a, b, [1, 2, 3].filter(condition))[0] matters (x2)
// This is the only reason we're returning a list rather than a single value.
// Both branches of the ternary _must_ return results. (x2)
// Accumulate the results from both sides and pass up the chain.
// Check if it looks like <<stuff>>(...), but not <<stuff>>?.(...)
// Check if it looks like <<stuff>>.filter(...) or <<stuff>>['filter'](...),
// or the optional chaining variants.
// As long as the object is a (possibly nullable) array,
// this is an Array.prototype.filter expression.
// not a filter expression.
```

### `isArrayish(type: Type): boolean`

<details><summary>Code</summary>

```ts
function isArrayish(type: Type): boolean {
      let isAtLeastOneArrayishComponent = false;
      for (const unionPart of tsutils.unionConstituents(type)) {
        if (
          tsutils.isIntrinsicNullType(unionPart) ||
          tsutils.isIntrinsicUndefinedType(unionPart)
        ) {
          continue;
        }

        // apparently checker.isArrayType(T[] & S[]) => false.
        // so we need to check the intersection parts individually.
        const isArrayOrIntersectionThereof = tsutils
          .intersectionConstituents(unionPart)
          .every(
            intersectionPart =>
              checker.isArrayType(intersectionPart) ||
              checker.isTupleType(intersectionPart),
          );

        if (!isArrayOrIntersectionThereof) {
          // There is a non-array, non-nullish type component,
          // so it's not an array.
          return false;
        }

        isAtLeastOneArrayishComponent = true;
      }

      return isAtLeastOneArrayishComponent;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Tells whether the type is a possibly nullable array/tuple or union thereof.
     */
```

- **Parameters**:
  - `type: Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.unionConstituents`
  - `tsutils.isIntrinsicNullType`
  - `tsutils.isIntrinsicUndefinedType`
  - `tsutils
          .intersectionConstituents(unionPart)
          .every`
  - `checker.isArrayType`
  - `checker.isTupleType`
- **Internal Comments**:
```
// apparently checker.isArrayType(T[] & S[]) => false. (x2)
// so we need to check the intersection parts individually. (x2)
// There is a non-array, non-nullish type component,
// so it's not an array.
```

### `getObjectIfArrayAtZeroExpression(node: TSESTree.CallExpression): TSESTree.Expression | undefined`

<details><summary>Code</summary>

```ts
function getObjectIfArrayAtZeroExpression(
      node: TSESTree.CallExpression,
    ): TSESTree.Expression | undefined {
      // .at() should take exactly one argument.
      if (node.arguments.length !== 1) {
        return undefined;
      }

      const callee = node.callee;
      if (
        callee.type === AST_NODE_TYPES.MemberExpression &&
        !callee.optional &&
        isStaticMemberAccessOfValue(callee, context, 'at')
      ) {
        const atArgument = getStaticValue(node.arguments[0], globalScope);
        if (atArgument != null && isTreatedAsZeroByArrayAt(atArgument.value)) {
          return callee.object;
        }
      }

      return undefined;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression`
- **Return Type**: `TSESTree.Expression | undefined`
- **Calls**:
  - `isStaticMemberAccessOfValue (from ../util)`
  - `getStaticValue (from ../util)`
  - `isTreatedAsZeroByArrayAt`
- **Internal Comments**:
```
// .at() should take exactly one argument.
```

### `isTreatedAsZeroByArrayAt(value: unknown): boolean`

<details><summary>Code</summary>

```ts
function isTreatedAsZeroByArrayAt(value: unknown): boolean {
      // This would cause the number constructor coercion to throw. Other static
      // values are safe.
      if (typeof value === 'symbol') {
        return false;
      }

      const asNumber = Number(value);

      if (isNaN(asNumber)) {
        return true;
      }

      return Math.trunc(asNumber) === 0;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Implements the algorithm for array indexing by `.at()` method.
     * @see https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/at#parameters
     */
```

- **Parameters**:
  - `value: unknown`
- **Return Type**: `boolean`
- **Calls**:
  - `Number`
  - `isNaN`
  - `Math.trunc`
- **Internal Comments**:
```
// This would cause the number constructor coercion to throw. Other static
// values are safe.
```

### `isMemberAccessOfZero(node: TSESTree.MemberExpressionComputedName): boolean`

<details><summary>Code</summary>

```ts
function isMemberAccessOfZero(
      node: TSESTree.MemberExpressionComputedName,
    ): boolean {
      const property = getStaticValue(node.property, globalScope);
      // Check if it looks like <<stuff>>[0] or <<stuff>>['0'], but not <<stuff>>?.[0]
      return (
        !node.optional &&
        property != null &&
        isTreatedAsZeroByMemberAccess(property.value)
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.MemberExpressionComputedName`
- **Return Type**: `boolean`
- **Calls**:
  - `getStaticValue (from ../util)`
  - `isTreatedAsZeroByMemberAccess`
- **Internal Comments**:
```
// Check if it looks like <<stuff>>[0] or <<stuff>>['0'], but not <<stuff>>?.[0]
```

### `isTreatedAsZeroByMemberAccess(value: unknown): boolean`

<details><summary>Code</summary>

```ts
function isTreatedAsZeroByMemberAccess(value: unknown): boolean {
      return String(value) === '0';
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Implements the algorithm for array indexing by member operator.
     * @see https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#array_indices
     */
```

- **Parameters**:
  - `value: unknown`
- **Return Type**: `boolean`
- **Calls**:
  - `String`
### `generateFixToRemoveArrayElementAccess(fixer: TSESLint.RuleFixer, arrayNode: TSESTree.Expression, wholeExpressionBeingFlagged: TSESTree.Expression): RuleFix`

<details><summary>Code</summary>

```ts
function generateFixToRemoveArrayElementAccess(
      fixer: TSESLint.RuleFixer,
      arrayNode: TSESTree.Expression,
      wholeExpressionBeingFlagged: TSESTree.Expression,
    ): RuleFix {
      const tokenToStartDeletingFrom = nullThrows(
        // The next `.` or `[` is what we're looking for.
        // think of (...).at(0) or (...)[0] or even (...)["at"](0).
        context.sourceCode.getTokenAfter(
          arrayNode,
          token => token.value === '.' || token.value === '[',
        ),
        'Expected to find a member access token!',
      );
      return fixer.removeRange([
        tokenToStartDeletingFrom.range[0],
        wholeExpressionBeingFlagged.range[1],
      ]);
    }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `arrayNode: TSESTree.Expression`
  - `wholeExpressionBeingFlagged: TSESTree.Expression`
- **Return Type**: `RuleFix`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenAfter`
  - `fixer.removeRange`
- **Internal Comments**:
```
// The next `.` or `[` is what we're looking for. (x4)
// think of (...).at(0) or (...)[0] or even (...)["at"](0). (x4)
```

### `generateFixToReplaceFilterWithFind(fixer: TSESLint.RuleFixer, filterExpression: FilterExpressionData): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
function generateFixToReplaceFilterWithFind(
      fixer: TSESLint.RuleFixer,
      filterExpression: FilterExpressionData,
    ): TSESLint.RuleFix {
      return fixer.replaceText(
        filterExpression.filterNode,
        filterExpression.isBracketSyntaxForFilter ? '"find"' : 'find',
      );
    }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `filterExpression: FilterExpressionData`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the .at(0) or ['at'](0).
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the .at(0) or ['at'](0). (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```

### `fix(fixer: any): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix[] => {
                    return [
                      ...filterExpressions.map(filterExpression =>
                        generateFixToReplaceFilterWithFind(
                          fixer,
                          filterExpression,
                        ),
                      ),
                      // Get rid of the [0].
                      generateFixToRemoveArrayElementAccess(
                        fixer,
                        object,
                        node,
                      ),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `filterExpressions.map`
  - `generateFixToReplaceFilterWithFind`
  - `generateFixToRemoveArrayElementAccess`
- **Internal Comments**:
```
// Get rid of the [0]. (x2)
```


---

## Interfaces

### `FilterExpressionData`

<details><summary>Interface Code</summary>

```ts
interface FilterExpressionData {
      filterNode: TSESTree.Node;
      isBracketSyntaxForFilter: boolean;
    }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `filterNode` | `TSESTree.Node` | ✗ |  |
| `isBracketSyntaxForFilter` | `boolean` | ✗ |  |


---