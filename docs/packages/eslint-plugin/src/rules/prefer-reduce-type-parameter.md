[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-reduce-type-parameter.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 9
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 1

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `MemberExpressionWithCallExpressionParent`

```ts
type MemberExpressionWithCallExpressionParent = {
  parent: TSESTree.CallExpression;
} & TSESTree.MemberExpression;
```


---