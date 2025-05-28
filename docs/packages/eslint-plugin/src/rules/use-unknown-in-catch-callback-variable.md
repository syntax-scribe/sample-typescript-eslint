[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `use-unknown-in-catch-callback-variable.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 35 |
| 🧱 Classes | 0 |
| 📦 Imports | 10 |
| 📊 Variables & Constants | 7 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/use-unknown-in-catch-callback-variable.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `ReportDescriptor` | `@typescript-eslint/utils/ts-eslint` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `getStaticMemberAccessValue` | `../util` |
| `isParenlessArrowFunction` | `../util` |
| `isRestParameterDeclaration` | `../util` |
| `nullThrows` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `useUnknownMessageBase` | `"Prefer the safe `: unknown` for a `{{method}}`{{append}} callback variable."` | const | `'Prefer the safe `: unknown` for a `{{method}}`{{append}} callback variable.'` | ✗ |
| `decl` | `any` | const | `firstParam.valueDeclaration` | ✗ |
| `catchVariableOuter` | `any` | const | `catchVariableOuterWithIncorrectTypes as Exclude<
          typeof catchVariableOuterWithIncorrectTypes,
          TSESTree.TSParameterProperty
        >` | ✗ |
| `catchVariableInner` | `any` | const | `catchVariableOuter.type === AST_NODE_TYPES.AssignmentPattern
          ? catchVariableOuter.left
          : catchVariableOuter` | ✗ |
| `catchVariableTypeAnnotation` | `any` | const | `catchVariableInner.typeAnnotation` | ✗ |
| `catchVariableTypeAnnotation` | `any` | const | `catchVariableInner.typeAnnotation` | ✗ |
| `argToCheck` | `never` | const | `argsToCheck[argIndexToCheck] as Exclude<
          TSESTree.Node,
          TSESTree.SpreadElement
        >` | ✗ |


---

## Functions

### `isFlaggableHandlerType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isFlaggableHandlerType(type: ts.Type): boolean {
      for (const unionPart of tsutils.unionConstituents(type)) {
        const callSignatures = tsutils.getCallSignaturesOfType(unionPart);
        if (callSignatures.length === 0) {
          // Ignore any non-function components to the type. Those are not this rule's problem.
          continue;
        }

        for (const callSignature of callSignatures) {
          const firstParam = callSignature.parameters.at(0);
          if (!firstParam) {
            // it's not an issue if there's no catch variable at all.
            continue;
          }

          let firstParamType = checker.getTypeOfSymbol(firstParam);

          const decl = firstParam.valueDeclaration;
          if (decl != null && isRestParameterDeclaration(decl)) {
            if (checker.isArrayType(firstParamType)) {
              firstParamType = checker.getTypeArguments(firstParamType)[0];
            } else if (checker.isTupleType(firstParamType)) {
              firstParamType = checker.getTypeArguments(firstParamType)[0];
            } else {
              // a rest arg that's not an array or tuple should definitely be flagged.
              return true;
            }
          }

          if (!tsutils.isIntrinsicUnknownType(firstParamType)) {
            return true;
          }
        }
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.unionConstituents`
  - `tsutils.getCallSignaturesOfType`
  - `callSignature.parameters.at`
  - `checker.getTypeOfSymbol`
  - `isRestParameterDeclaration (from ../util)`
  - `checker.isArrayType`
  - `checker.getTypeArguments`
  - `checker.isTupleType`
  - `tsutils.isIntrinsicUnknownType`
- **Internal Comments**:
```
// Ignore any non-function components to the type. Those are not this rule's problem.
// it's not an issue if there's no catch variable at all.
// a rest arg that's not an array or tuple should definitely be flagged.
```

### `collectFlaggedNodes(node: Exclude<TSESTree.Node, TSESTree.SpreadElement>): (TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression)[]`

<details><summary>Code</summary>

```ts
function collectFlaggedNodes(
      node: Exclude<TSESTree.Node, TSESTree.SpreadElement>,
    ): (TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression)[] {
      switch (node.type) {
        case AST_NODE_TYPES.LogicalExpression:
          return [
            ...collectFlaggedNodes(node.left),
            ...collectFlaggedNodes(node.right),
          ];
        case AST_NODE_TYPES.SequenceExpression:
          return collectFlaggedNodes(
            nullThrows(
              node.expressions.at(-1),
              'sequence expression must have multiple expressions',
            ),
          );
        case AST_NODE_TYPES.ConditionalExpression:
          return [
            ...collectFlaggedNodes(node.consequent),
            ...collectFlaggedNodes(node.alternate),
          ];
        case AST_NODE_TYPES.ArrowFunctionExpression:
        case AST_NODE_TYPES.FunctionExpression:
          {
            const argument = esTreeNodeToTSNodeMap.get(node);
            const typeOfArgument = checker.getTypeAtLocation(argument);
            if (isFlaggableHandlerType(typeOfArgument)) {
              return [node];
            }
          }
          break;
        default:
          break;
      }
      return [];
    }
```
</details>

- **Parameters**:
  - `node: Exclude<TSESTree.Node, TSESTree.SpreadElement>`
- **Return Type**: `(TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression)[]`
- **Calls**:
  - `collectFlaggedNodes`
  - `nullThrows (from ../util)`
  - `node.expressions.at`
  - `esTreeNodeToTSNodeMap.get`
  - `checker.getTypeAtLocation`
  - `isFlaggableHandlerType`
### `refineReportIfPossible(argument: TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression): Partial<ReportDescriptor<MessageIds>> | undefined`

<details><summary>Code</summary>

```ts
function refineReportIfPossible(
      argument: TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression,
    ): Partial<ReportDescriptor<MessageIds>> | undefined {
      const catchVariableOuterWithIncorrectTypes = nullThrows(
        argument.params.at(0),
        'There should have been at least one parameter for the rule to have flagged.',
      );

      // Function expressions can't have parameter properties; those only exist in constructors.
      const catchVariableOuter =
        catchVariableOuterWithIncorrectTypes as Exclude<
          typeof catchVariableOuterWithIncorrectTypes,
          TSESTree.TSParameterProperty
        >;
      const catchVariableInner =
        catchVariableOuter.type === AST_NODE_TYPES.AssignmentPattern
          ? catchVariableOuter.left
          : catchVariableOuter;

      switch (catchVariableInner.type) {
        case AST_NODE_TYPES.Identifier: {
          const catchVariableTypeAnnotation = catchVariableInner.typeAnnotation;
          if (catchVariableTypeAnnotation == null) {
            return {
              node: catchVariableOuter,
              suggest: [
                {
                  messageId: 'addUnknownTypeAnnotationSuggestion',
                  fix: (fixer: TSESLint.RuleFixer): TSESLint.RuleFix[] => {
                    if (
                      argument.type ===
                        AST_NODE_TYPES.ArrowFunctionExpression &&
                      isParenlessArrowFunction(argument, context.sourceCode)
                    ) {
                      return [
                        fixer.insertTextBefore(catchVariableInner, '('),
                        fixer.insertTextAfter(catchVariableInner, ': unknown)'),
                      ];
                    }

                    return [
                      fixer.insertTextAfter(catchVariableInner, ': unknown'),
                    ];
                  },
                },
              ],
            };
          }

          return {
            node: catchVariableOuter,
            suggest: [
              {
                messageId: 'wrongTypeAnnotationSuggestion',
                fix: (fixer: TSESLint.RuleFixer): TSESLint.RuleFix =>
                  fixer.replaceText(catchVariableTypeAnnotation, ': unknown'),
              },
            ],
          };
        }
        case AST_NODE_TYPES.ArrayPattern: {
          return {
            node: catchVariableOuter,
            messageId: 'useUnknownArrayDestructuringPattern',
          };
        }
        case AST_NODE_TYPES.ObjectPattern: {
          return {
            node: catchVariableOuter,
            messageId: 'useUnknownObjectDestructuringPattern',
          };
        }
        case AST_NODE_TYPES.RestElement: {
          const catchVariableTypeAnnotation = catchVariableInner.typeAnnotation;
          if (catchVariableTypeAnnotation == null) {
            return {
              node: catchVariableOuter,
              suggest: [
                {
                  messageId: 'addUnknownRestTypeAnnotationSuggestion',
                  fix: (fixer): TSESLint.RuleFix =>
                    fixer.insertTextAfter(catchVariableInner, ': [unknown]'),
                },
              ],
            };
          }
          return {
            node: catchVariableOuter,
            suggest: [
              {
                messageId: 'wrongRestTypeAnnotationSuggestion',
                fix: (fixer): TSESLint.RuleFix =>
                  fixer.replaceText(catchVariableTypeAnnotation, ': [unknown]'),
              },
            ],
          };
        }
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Analyzes the syntax of the catch argument and makes a best effort to pinpoint
     * why it's reporting, and to come up with a suggested fix if possible.
     *
     * This function is explicitly operating under the assumption that the
     * rule _is reporting_, so it is not guaranteed to be sound to call otherwise.
     */
```

- **Parameters**:
  - `argument: TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression`
- **Return Type**: `Partial<ReportDescriptor<MessageIds>> | undefined`
- **Calls**:
  - `nullThrows (from ../util)`
  - `argument.params.at`
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
  - `fixer.replaceText`
- **Internal Comments**:
```
// Function expressions can't have parameter properties; those only exist in constructors. (x2)
```

### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[] => {
                    if (
                      argument.type ===
                        AST_NODE_TYPES.ArrowFunctionExpression &&
                      isParenlessArrowFunction(argument, context.sourceCode)
                    ) {
                      return [
                        fixer.insertTextBefore(catchVariableInner, '('),
                        fixer.insertTextAfter(catchVariableInner, ': unknown)'),
                      ];
                    }

                    return [
                      fixer.insertTextAfter(catchVariableInner, ': unknown'),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[] => {
                    if (
                      argument.type ===
                        AST_NODE_TYPES.ArrowFunctionExpression &&
                      isParenlessArrowFunction(argument, context.sourceCode)
                    ) {
                      return [
                        fixer.insertTextBefore(catchVariableInner, '('),
                        fixer.insertTextAfter(catchVariableInner, ': unknown)'),
                      ];
                    }

                    return [
                      fixer.insertTextAfter(catchVariableInner, ': unknown'),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[] => {
                    if (
                      argument.type ===
                        AST_NODE_TYPES.ArrowFunctionExpression &&
                      isParenlessArrowFunction(argument, context.sourceCode)
                    ) {
                      return [
                        fixer.insertTextBefore(catchVariableInner, '('),
                        fixer.insertTextAfter(catchVariableInner, ': unknown)'),
                      ];
                    }

                    return [
                      fixer.insertTextAfter(catchVariableInner, ': unknown'),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[] => {
                    if (
                      argument.type ===
                        AST_NODE_TYPES.ArrowFunctionExpression &&
                      isParenlessArrowFunction(argument, context.sourceCode)
                    ) {
                      return [
                        fixer.insertTextBefore(catchVariableInner, '('),
                        fixer.insertTextAfter(catchVariableInner, ': unknown)'),
                      ];
                    }

                    return [
                      fixer.insertTextAfter(catchVariableInner, ': unknown'),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix =>
                  fixer.replaceText(catchVariableTypeAnnotation, ': unknown')
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix =>
                  fixer.replaceText(catchVariableTypeAnnotation, ': unknown')
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix =>
                  fixer.replaceText(catchVariableTypeAnnotation, ': unknown')
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix =>
                  fixer.replaceText(catchVariableTypeAnnotation, ': unknown')
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                    fixer.insertTextAfter(catchVariableInner, ': [unknown]')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.insertTextAfter`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                    fixer.insertTextAfter(catchVariableInner, ': [unknown]')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.insertTextAfter`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                    fixer.insertTextAfter(catchVariableInner, ': [unknown]')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.insertTextAfter`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                    fixer.insertTextAfter(catchVariableInner, ': [unknown]')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.insertTextAfter`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                  fixer.replaceText(catchVariableTypeAnnotation, ': [unknown]')
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
                  fixer.replaceText(catchVariableTypeAnnotation, ': [unknown]')
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
                  fixer.replaceText(catchVariableTypeAnnotation, ': [unknown]')
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
                  fixer.replaceText(catchVariableTypeAnnotation, ': [unknown]')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[] => {
                    if (
                      argument.type ===
                        AST_NODE_TYPES.ArrowFunctionExpression &&
                      isParenlessArrowFunction(argument, context.sourceCode)
                    ) {
                      return [
                        fixer.insertTextBefore(catchVariableInner, '('),
                        fixer.insertTextAfter(catchVariableInner, ': unknown)'),
                      ];
                    }

                    return [
                      fixer.insertTextAfter(catchVariableInner, ': unknown'),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[] => {
                    if (
                      argument.type ===
                        AST_NODE_TYPES.ArrowFunctionExpression &&
                      isParenlessArrowFunction(argument, context.sourceCode)
                    ) {
                      return [
                        fixer.insertTextBefore(catchVariableInner, '('),
                        fixer.insertTextAfter(catchVariableInner, ': unknown)'),
                      ];
                    }

                    return [
                      fixer.insertTextAfter(catchVariableInner, ': unknown'),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[] => {
                    if (
                      argument.type ===
                        AST_NODE_TYPES.ArrowFunctionExpression &&
                      isParenlessArrowFunction(argument, context.sourceCode)
                    ) {
                      return [
                        fixer.insertTextBefore(catchVariableInner, '('),
                        fixer.insertTextAfter(catchVariableInner, ': unknown)'),
                      ];
                    }

                    return [
                      fixer.insertTextAfter(catchVariableInner, ': unknown'),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[]`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix[] => {
                    if (
                      argument.type ===
                        AST_NODE_TYPES.ArrowFunctionExpression &&
                      isParenlessArrowFunction(argument, context.sourceCode)
                    ) {
                      return [
                        fixer.insertTextBefore(catchVariableInner, '('),
                        fixer.insertTextAfter(catchVariableInner, ': unknown)'),
                      ];
                    }

                    return [
                      fixer.insertTextAfter(catchVariableInner, ': unknown'),
                    ];
                  }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix[]`
- **Calls**:
  - `isParenlessArrowFunction (from ../util)`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix =>
                  fixer.replaceText(catchVariableTypeAnnotation, ': unknown')
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix =>
                  fixer.replaceText(catchVariableTypeAnnotation, ': unknown')
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix =>
                  fixer.replaceText(catchVariableTypeAnnotation, ': unknown')
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix =>
                  fixer.replaceText(catchVariableTypeAnnotation, ': unknown')
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                    fixer.insertTextAfter(catchVariableInner, ': [unknown]')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.insertTextAfter`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                    fixer.insertTextAfter(catchVariableInner, ': [unknown]')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.insertTextAfter`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                    fixer.insertTextAfter(catchVariableInner, ': [unknown]')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.insertTextAfter`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                    fixer.insertTextAfter(catchVariableInner, ': [unknown]')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.insertTextAfter`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix =>
                  fixer.replaceText(catchVariableTypeAnnotation, ': [unknown]')
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
                  fixer.replaceText(catchVariableTypeAnnotation, ': [unknown]')
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
                  fixer.replaceText(catchVariableTypeAnnotation, ': [unknown]')
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
                  fixer.replaceText(catchVariableTypeAnnotation, ': [unknown]')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`

---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = | 'addUnknownRestTypeAnnotationSuggestion'
  | 'addUnknownTypeAnnotationSuggestion'
  | 'useUnknown'
  | 'useUnknownArrayDestructuringPattern'
  | 'useUnknownObjectDestructuringPattern'
  | 'wrongRestTypeAnnotationSuggestion'
  | 'wrongTypeAnnotationSuggestion';
```


---