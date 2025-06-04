[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `consistent-indexed-object-style.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 99 |
| 📦 Imports | 11 |
| 📊 Variables & Constants | 14 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/consistent-indexed-object-style.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ScopeVariable` | `@typescript-eslint/scope-manager` |
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `ReportFixFunction` | `@typescript-eslint/utils/ts-eslint` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ASTUtils` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getFixOrSuggest` | `../util` |
| `isNodeEqual` | `../util` |
| `isParenthesized` | `../util` |
| `nullThrows` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `keyType` | `any` | const | `parameter.typeAnnotation` | ✗ |
| `valueType` | `any` | const | `member.typeAnnotation` | ✗ |
| `record` | `string` | const | `member.readonly
                ? `Readonly<Record<${key}, ${value}>>`
                : `Record<${key}, ${value}>`` | ✗ |
| `typeName` | `any` | const | `node.typeName` | ✗ |
| `params` | `any` | const | `node.typeArguments?.params` | ✗ |
| `indexParam` | `any` | const | `params[0]` | ✗ |
| `shouldFix` | `boolean` | const | `indexParam.type === AST_NODE_TYPES.TSStringKeyword ||
            indexParam.type === AST_NODE_TYPES.TSNumberKeyword ||
            indexParam.type === AST_NODE_TYPES.TSSymbolKeyword` | ✗ |
| `genericTypes` | `string` | let/var | `''` | ✗ |
| `key` | `any` | const | `node.key` | ✗ |
| `constraint` | `any` | const | `node.constraint` | ✗ |
| `parentId` | `any` | const | `findParentDeclaration(node)?.id` | ✗ |
| `canFix` | `boolean` | const | `node.readonly !== '-'` | ✗ |
| `valueType` | `any` | const | `node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any'` | ✗ |
| `recordText` | `string` | let/var | ``Record<${keyType}, ${valueType}>`` | ✗ |


---

## Functions

### `checkMembers(members: TSESTree.TypeElement[], node: TSESTree.TSInterfaceDeclaration | TSESTree.TSTypeLiteral, parentId: TSESTree.Identifier | undefined, prefix: string, postfix: string, safeFix: boolean): void`

<details><summary>Code</summary>

```ts
function checkMembers(
      members: TSESTree.TypeElement[],
      node: TSESTree.TSInterfaceDeclaration | TSESTree.TSTypeLiteral,
      parentId: TSESTree.Identifier | undefined,
      prefix: string,
      postfix: string,
      safeFix = true,
    ): void {
      if (members.length !== 1) {
        return;
      }
      const [member] = members;

      if (member.type !== AST_NODE_TYPES.TSIndexSignature) {
        return;
      }

      const parameter = member.parameters.at(0);
      if (parameter?.type !== AST_NODE_TYPES.Identifier) {
        return;
      }

      const keyType = parameter.typeAnnotation;
      if (!keyType) {
        return;
      }

      const valueType = member.typeAnnotation;
      if (!valueType) {
        return;
      }

      if (parentId) {
        const scope = context.sourceCode.getScope(parentId);
        const superVar = ASTUtils.findVariable(scope, parentId.name);

        if (
          superVar &&
          isDeeplyReferencingType(node, superVar, new Set([parentId]))
        ) {
          return;
        }
      }

      context.report({
        node,
        messageId: 'preferRecord',
        fix: safeFix
          ? (fixer): TSESLint.RuleFix => {
              const key = context.sourceCode.getText(keyType.typeAnnotation);
              const value = context.sourceCode.getText(
                valueType.typeAnnotation,
              );
              const record = member.readonly
                ? `Readonly<Record<${key}, ${value}>>`
                : `Record<${key}, ${value}>`;
              return fixer.replaceText(node, `${prefix}${record}${postfix}`);
            }
          : null,
      });
    }
```
</details>

- **Parameters**:
  - `members: TSESTree.TypeElement[]`
  - `node: TSESTree.TSInterfaceDeclaration | TSESTree.TSTypeLiteral`
  - `parentId: TSESTree.Identifier | undefined`
  - `prefix: string`
  - `postfix: string`
  - `safeFix: boolean`
- **Return Type**: `void`
- **Calls**:
  - `member.parameters.at`
  - `context.sourceCode.getScope`
  - `ASTUtils.findVariable`
  - `isDeeplyReferencingType`
  - `context.report`
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
                  const key = context.sourceCode.getText(params[0]);
                  const type = context.sourceCode.getText(params[1]);
                  return fixer.replaceText(node, `{ [key: ${key}]: ${type} }`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `fix(fixer: any): ReturnType<ReportFixFunction>`

<details><summary>Code</summary>

```ts
(fixer): ReturnType<ReportFixFunction> => {
                const keyType = context.sourceCode.getText(constraint);
                const valueType = node.typeAnnotation
                  ? context.sourceCode.getText(node.typeAnnotation)
                  : 'any';

                let recordText = `Record<${keyType}, ${valueType}>`;

                if (node.optional === '+' || node.optional === true) {
                  recordText = `Partial<${recordText}>`;
                } else if (node.optional === '-') {
                  recordText = `Required<${recordText}>`;
                }

                if (node.readonly === '+' || node.readonly === true) {
                  recordText = `Readonly<${recordText}>`;
                }

                return fixer.replaceText(node, recordText);
              }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `ReturnType<ReportFixFunction>`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`
### `findParentDeclaration(node: TSESTree.Node): TSESTree.TSTypeAliasDeclaration | undefined`

<details><summary>Code</summary>

```ts
function findParentDeclaration(
  node: TSESTree.Node,
): TSESTree.TSTypeAliasDeclaration | undefined {
  if (node.parent && node.parent.type !== AST_NODE_TYPES.TSTypeAnnotation) {
    if (node.parent.type === AST_NODE_TYPES.TSTypeAliasDeclaration) {
      return node.parent;
    }
    return findParentDeclaration(node.parent);
  }
  return undefined;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `TSESTree.TSTypeAliasDeclaration | undefined`
- **Calls**:
  - `findParentDeclaration`
### `isDeeplyReferencingType(node: TSESTree.Node, superVar: ScopeVariable, visited: Set<TSESTree.Node>): boolean`

<details><summary>Code</summary>

```ts
function isDeeplyReferencingType(
  node: TSESTree.Node,
  superVar: ScopeVariable,
  visited: Set<TSESTree.Node>,
): boolean {
  if (visited.has(node)) {
    // something on the chain is circular but it's not the reference being checked
    return false;
  }

  visited.add(node);

  switch (node.type) {
    case AST_NODE_TYPES.TSTypeLiteral:
      return node.members.some(member =>
        isDeeplyReferencingType(member, superVar, visited),
      );
    case AST_NODE_TYPES.TSTypeAliasDeclaration:
      return isDeeplyReferencingType(node.typeAnnotation, superVar, visited);
    case AST_NODE_TYPES.TSIndexedAccessType:
      return [node.indexType, node.objectType].some(type =>
        isDeeplyReferencingType(type, superVar, visited),
      );
    case AST_NODE_TYPES.TSMappedType:
      if (node.typeAnnotation) {
        return isDeeplyReferencingType(node.typeAnnotation, superVar, visited);
      }

      break;
    case AST_NODE_TYPES.TSConditionalType:
      return [
        node.checkType,
        node.extendsType,
        node.falseType,
        node.trueType,
      ].some(type => isDeeplyReferencingType(type, superVar, visited));
    case AST_NODE_TYPES.TSUnionType:
    case AST_NODE_TYPES.TSIntersectionType:
      return node.types.some(type =>
        isDeeplyReferencingType(type, superVar, visited),
      );
    case AST_NODE_TYPES.TSInterfaceDeclaration:
      return node.body.body.some(type =>
        isDeeplyReferencingType(type, superVar, visited),
      );
    case AST_NODE_TYPES.TSTypeAnnotation:
      return isDeeplyReferencingType(node.typeAnnotation, superVar, visited);
    case AST_NODE_TYPES.TSIndexSignature: {
      if (node.typeAnnotation) {
        return isDeeplyReferencingType(node.typeAnnotation, superVar, visited);
      }
      break;
    }
    case AST_NODE_TYPES.TSTypeParameterInstantiation: {
      return node.params.some(param =>
        isDeeplyReferencingType(param, superVar, visited),
      );
    }
    case AST_NODE_TYPES.TSTypeReference: {
      if (isDeeplyReferencingType(node.typeName, superVar, visited)) {
        return true;
      }

      if (
        node.typeArguments &&
        isDeeplyReferencingType(node.typeArguments, superVar, visited)
      ) {
        return true;
      }

      break;
    }
    case AST_NODE_TYPES.Identifier: {
      // check if the identifier is a reference of the type being checked
      if (superVar.references.some(ref => isNodeEqual(ref.identifier, node))) {
        return true;
      }

      // otherwise, follow its definition(s)
      const refVar = ASTUtils.findVariable(superVar.scope, node.name);

      if (refVar) {
        return refVar.defs.some(def =>
          isDeeplyReferencingType(def.node, superVar, visited),
        );
      }
    }
  }

  return false;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `superVar: ScopeVariable`
  - `visited: Set<TSESTree.Node>`
- **Return Type**: `boolean`
- **Calls**:
  - `visited.has`
  - `visited.add`
  - `node.members.some`
  - `isDeeplyReferencingType`
  - `[node.indexType, node.objectType].some`
  - `[
        node.checkType,
        node.extendsType,
        node.falseType,
        node.trueType,
      ].some`
  - `node.types.some`
  - `node.body.body.some`
  - `node.params.some`
  - `superVar.references.some`
  - `isNodeEqual (from ../util)`
  - `ASTUtils.findVariable`
  - `refVar.defs.some`
- **Internal Comments**:
```
// something on the chain is circular but it's not the reference being checked
// check if the identifier is a reference of the type being checked
// otherwise, follow its definition(s) (x2)
```


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = | 'preferIndexSignature'
  | 'preferIndexSignatureSuggestion'
  | 'preferRecord';
```

### `Options`

```ts
type Options = ['index-signature' | 'record'];
```


---