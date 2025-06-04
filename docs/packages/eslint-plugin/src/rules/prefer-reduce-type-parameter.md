[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-reduce-type-parameter.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 9 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 2 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-reduce-type-parameter.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `isStaticMemberAccessOfValue` | `../util` |
| `isTypeAssertion` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `isAssertionNecessary` | `boolean` | const | `!checker.isTypeAssignableTo(
            initializerType,
            assertedType,
          )` | ✗ |
| `fixes` | `any[]` | const | `[
                fixer.removeRange([
                  secondArg.range[0],
                  secondArg.expression.range[0],
                ]),
                fixer.removeRange([
                  secondArg.expression.range[1],
                  secondArg.range[1],
                ]),
              ]` | ✗ |


---

## Functions

### `isArrayType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isArrayType(type: ts.Type): boolean {
      return tsutils
        .unionConstituents(type)
        .every(unionPart =>
          tsutils
            .intersectionConstituents(unionPart)
            .every(t => checker.isArrayType(t) || checker.isTupleType(t)),
        );
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils
        .unionConstituents(type)
        .every`
  - `tsutils
            .intersectionConstituents(unionPart)
            .every`
  - `checker.isArrayType`
  - `checker.isTupleType`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => {
              const fixes = [
                fixer.removeRange([
                  secondArg.range[0],
                  secondArg.expression.range[0],
                ]),
                fixer.removeRange([
                  secondArg.expression.range[1],
                  secondArg.range[1],
                ]),
              ];

              if (!callee.parent.typeArguments) {
                fixes.push(
                  fixer.insertTextAfter(
                    callee,
                    `<${context.sourceCode.getText(secondArg.typeAnnotation)}>`,
                  ),
                );
              }

              return fixes;
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
- **Calls**:
  - `fixer.removeRange`
  - `fixes.push`
  - `fixer.insertTextAfter`
  - `context.sourceCode.getText`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => {
              const fixes = [
                fixer.removeRange([
                  secondArg.range[0],
                  secondArg.expression.range[0],
                ]),
                fixer.removeRange([
                  secondArg.expression.range[1],
                  secondArg.range[1],
                ]),
              ];

              if (!callee.parent.typeArguments) {
                fixes.push(
                  fixer.insertTextAfter(
                    callee,
                    `<${context.sourceCode.getText(secondArg.typeAnnotation)}>`,
                  ),
                );
              }

              return fixes;
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
- **Calls**:
  - `fixer.removeRange`
  - `fixes.push`
  - `fixer.insertTextAfter`
  - `context.sourceCode.getText`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => {
              const fixes = [
                fixer.removeRange([
                  secondArg.range[0],
                  secondArg.expression.range[0],
                ]),
                fixer.removeRange([
                  secondArg.expression.range[1],
                  secondArg.range[1],
                ]),
              ];

              if (!callee.parent.typeArguments) {
                fixes.push(
                  fixer.insertTextAfter(
                    callee,
                    `<${context.sourceCode.getText(secondArg.typeAnnotation)}>`,
                  ),
                );
              }

              return fixes;
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
- **Calls**:
  - `fixer.removeRange`
  - `fixes.push`
  - `fixer.insertTextAfter`
  - `context.sourceCode.getText`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => {
              const fixes = [
                fixer.removeRange([
                  secondArg.range[0],
                  secondArg.expression.range[0],
                ]),
                fixer.removeRange([
                  secondArg.expression.range[1],
                  secondArg.range[1],
                ]),
              ];

              if (!callee.parent.typeArguments) {
                fixes.push(
                  fixer.insertTextAfter(
                    callee,
                    `<${context.sourceCode.getText(secondArg.typeAnnotation)}>`,
                  ),
                );
              }

              return fixes;
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
- **Calls**:
  - `fixer.removeRange`
  - `fixes.push`
  - `fixer.insertTextAfter`
  - `context.sourceCode.getText`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => {
              const fixes = [
                fixer.removeRange([
                  secondArg.range[0],
                  secondArg.expression.range[0],
                ]),
                fixer.removeRange([
                  secondArg.expression.range[1],
                  secondArg.range[1],
                ]),
              ];

              if (!callee.parent.typeArguments) {
                fixes.push(
                  fixer.insertTextAfter(
                    callee,
                    `<${context.sourceCode.getText(secondArg.typeAnnotation)}>`,
                  ),
                );
              }

              return fixes;
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
- **Calls**:
  - `fixer.removeRange`
  - `fixes.push`
  - `fixer.insertTextAfter`
  - `context.sourceCode.getText`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => {
              const fixes = [
                fixer.removeRange([
                  secondArg.range[0],
                  secondArg.expression.range[0],
                ]),
                fixer.removeRange([
                  secondArg.expression.range[1],
                  secondArg.range[1],
                ]),
              ];

              if (!callee.parent.typeArguments) {
                fixes.push(
                  fixer.insertTextAfter(
                    callee,
                    `<${context.sourceCode.getText(secondArg.typeAnnotation)}>`,
                  ),
                );
              }

              return fixes;
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
- **Calls**:
  - `fixer.removeRange`
  - `fixes.push`
  - `fixer.insertTextAfter`
  - `context.sourceCode.getText`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => {
              const fixes = [
                fixer.removeRange([
                  secondArg.range[0],
                  secondArg.expression.range[0],
                ]),
                fixer.removeRange([
                  secondArg.expression.range[1],
                  secondArg.range[1],
                ]),
              ];

              if (!callee.parent.typeArguments) {
                fixes.push(
                  fixer.insertTextAfter(
                    callee,
                    `<${context.sourceCode.getText(secondArg.typeAnnotation)}>`,
                  ),
                );
              }

              return fixes;
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
- **Calls**:
  - `fixer.removeRange`
  - `fixes.push`
  - `fixer.insertTextAfter`
  - `context.sourceCode.getText`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => {
              const fixes = [
                fixer.removeRange([
                  secondArg.range[0],
                  secondArg.expression.range[0],
                ]),
                fixer.removeRange([
                  secondArg.expression.range[1],
                  secondArg.range[1],
                ]),
              ];

              if (!callee.parent.typeArguments) {
                fixes.push(
                  fixer.insertTextAfter(
                    callee,
                    `<${context.sourceCode.getText(secondArg.typeAnnotation)}>`,
                  ),
                );
              }

              return fixes;
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
- **Calls**:
  - `fixer.removeRange`
  - `fixes.push`
  - `fixer.insertTextAfter`
  - `context.sourceCode.getText`

---

## Type Aliases

### `MemberExpressionWithCallExpressionParent`

```ts
type MemberExpressionWithCallExpressionParent = {
  parent: TSESTree.CallExpression;
} & TSESTree.MemberExpression;
```


---