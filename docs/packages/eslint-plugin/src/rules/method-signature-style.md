[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `method-signature-style.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 37
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/method-signature-style.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `isClosingParenToken` | `../util` |
| `isCommaToken` | `../util` |
| `isOpeningParenToken` | `../util` |
| `isSemicolonToken` | `../util` |
| `nullThrows` | `../util` |


---

## Functions

### `getMethodKey(node: TSESTree.TSMethodSignature | TSESTree.TSPropertySignature): string`

<details><summary>Code</summary>

```ts
function getMethodKey(
      node: TSESTree.TSMethodSignature | TSESTree.TSPropertySignature,
    ): string {
      let key = context.sourceCode.getText(node.key);
      if (node.computed) {
        key = `[${key}]`;
      }
      if (node.optional) {
        key = `${key}?`;
      }
      if (node.readonly) {
        key = `readonly ${key}`;
      }
      return key;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSMethodSignature | TSESTree.TSPropertySignature`
- **Return Type**: `string`
- **Calls**:
  - `context.sourceCode.getText`
### `getMethodParams(node: TSESTree.TSFunctionType | TSESTree.TSMethodSignature): string`

<details><summary>Code</summary>

```ts
function getMethodParams(
      node: TSESTree.TSFunctionType | TSESTree.TSMethodSignature,
    ): string {
      let params = '()';
      if (node.params.length > 0) {
        const openingParen = nullThrows(
          context.sourceCode.getTokenBefore(
            node.params[0],
            isOpeningParenToken,
          ),
          'Missing opening paren before first parameter',
        );
        const closingParen = nullThrows(
          context.sourceCode.getTokenAfter(
            node.params[node.params.length - 1],
            isClosingParenToken,
          ),
          'Missing closing paren after last parameter',
        );

        params = context.sourceCode.text.substring(
          openingParen.range[0],
          closingParen.range[1],
        );
      }
      if (node.typeParameters != null) {
        const typeParams = context.sourceCode.getText(node.typeParameters);
        params = `${typeParams}${params}`;
      }
      return params;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSFunctionType | TSESTree.TSMethodSignature`
- **Return Type**: `string`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenBefore`
  - `context.sourceCode.getTokenAfter`
  - `context.sourceCode.text.substring`
  - `context.sourceCode.getText`
### `getMethodReturnType(node: TSESTree.TSFunctionType | TSESTree.TSMethodSignature): string`

<details><summary>Code</summary>

```ts
function getMethodReturnType(
      node: TSESTree.TSFunctionType | TSESTree.TSMethodSignature,
    ): string {
      return node.returnType == null
        ? // if the method has no return type, it implicitly has an `any` return type
          // we just make it explicit here so we can do the fix
          'any'
        : context.sourceCode.getText(node.returnType.typeAnnotation);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSFunctionType | TSESTree.TSMethodSignature`
- **Return Type**: `string`
- **Calls**:
  - `context.sourceCode.getText`
- **Internal Comments**:
```
// we just make it explicit here so we can do the fix
```

### `getDelimiter(node: TSESTree.Node): string`

<details><summary>Code</summary>

```ts
function getDelimiter(node: TSESTree.Node): string {
      const lastToken = context.sourceCode.getLastToken(node);
      if (
        lastToken &&
        (isSemicolonToken(lastToken) || isCommaToken(lastToken))
      ) {
        return lastToken.value;
      }

      return '';
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `string`
- **Calls**:
  - `context.sourceCode.getLastToken`
  - `isSemicolonToken (from ../util)`
  - `isCommaToken (from ../util)`
### `isNodeParentModuleDeclaration(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isNodeParentModuleDeclaration(node: TSESTree.Node): boolean {
      if (!node.parent) {
        return false;
      }

      if (node.parent.type === AST_NODE_TYPES.TSModuleDeclaration) {
        return true;
      }

      if (node.parent.type === AST_NODE_TYPES.Program) {
        return false;
      }
      return isNodeParentModuleDeclaration(node.parent);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isNodeParentModuleDeclaration`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                const key = getMethodKey(methodNode);
                const params = getMethodParams(methodNode);
                const returnType = getMethodReturnType(methodNode);
                const delimiter = getDelimiter(methodNode);
                return fixer.replaceText(
                  methodNode,
                  `${key}: ${params} => ${returnType}${delimiter}`,
                );
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              const key = getMethodKey(propertyNode);
              const params = getMethodParams(typeNode);
              const returnType = getMethodReturnType(typeNode);
              const delimiter = getDelimiter(propertyNode);
              return fixer.replaceText(
                propertyNode,
                `${key}${params}: ${returnType}${delimiter}`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `getMethodKey`
  - `getMethodParams`
  - `getMethodReturnType`
  - `getDelimiter`
  - `fixer.replaceText`

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
type Options = [('method' | 'property')?];
```

### `MessageIds`

```ts
type MessageIds = 'errorMethod' | 'errorProperty';
```


---