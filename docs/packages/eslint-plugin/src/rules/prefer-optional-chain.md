[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-optional-chain.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 17
- **Classes**: 0
- **Imports**: 14
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-optional-chain.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleFix` | `@typescript-eslint/utils/ts-eslint` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ValidOperand` | `./prefer-optional-chain-utils/gatherLogicalOperands` |
| `PreferOptionalChainMessageIds` | `./prefer-optional-chain-utils/PreferOptionalChainOptions` |
| `PreferOptionalChainOptions` | `./prefer-optional-chain-utils/PreferOptionalChainOptions` |
| `createRule` | `../util` |
| `getOperatorPrecedence` | `../util` |
| `getParserServices` | `../util` |
| `OperatorPrecedence` | `../util` |
| `analyzeChain` | `./prefer-optional-chain-utils/analyzeChain` |
| `checkNullishAndReport` | `./prefer-optional-chain-utils/checkNullishAndReport` |
| `gatherLogicalOperands` | `./prefer-optional-chain-utils/gatherLogicalOperands` |
| `OperandValidity` | `./prefer-optional-chain-utils/gatherLogicalOperands` |


---

## Functions

### `isLeftSideLowerPrecedence(): boolean`

<details><summary>Code</summary>

```ts
function isLeftSideLowerPrecedence(): boolean {
          const logicalTsNode = parserServices.esTreeNodeToTSNodeMap.get(node);
          const leftTsNode = parserServices.esTreeNodeToTSNodeMap.get(leftNode);
          const leftPrecedence = getOperatorPrecedence(
            leftTsNode.kind,
            logicalTsNode.operatorToken.kind,
          );

          return leftPrecedence < OperatorPrecedence.LeftHandSide;
        }
```
</details>

- **Return Type**: `boolean`
- **Calls**:
  - `parserServices.esTreeNodeToTSNodeMap.get`
  - `getOperatorPrecedence (from ../util)`
### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```

### `fix(fixer: any): RuleFix`

<details><summary>Code</summary>

```ts
(fixer): RuleFix => {
                const leftNodeText = context.sourceCode.getText(leftNode);
                // Any node that is made of an operator with higher or equal precedence,
                const maybeWrappedLeftNode = isLeftSideLowerPrecedence()
                  ? `(${leftNodeText})`
                  : leftNodeText;
                const propertyToBeOptionalText = context.sourceCode.getText(
                  parentNode.property,
                );
                const maybeWrappedProperty = parentNode.computed
                  ? `[${propertyToBeOptionalText}]`
                  : propertyToBeOptionalText;
                return fixer.replaceTextRange(
                  parentNode.range,
                  `${maybeWrappedLeftNode}?.${maybeWrappedProperty}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `isLeftSideLowerPrecedence`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// Any node that is made of an operator with higher or equal precedence, (x2)
```


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