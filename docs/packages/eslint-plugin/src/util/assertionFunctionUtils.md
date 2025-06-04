[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `assertionFunctionUtils.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/assertionFunctionUtils.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserServicesWithTypeInformation` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `checkableArguments` | `TSESTree.Expression[]` | const | `[]` | ✗ |
| `checkableArguments` | `TSESTree.Expression[]` | const | `[]` | ✗ |


---

## Functions

### `findTruthinessAssertedArgument(services: ParserServicesWithTypeInformation, node: TSESTree.CallExpression): TSESTree.Expression | undefined`

<details><summary>Code</summary>

```ts
export function findTruthinessAssertedArgument(
  services: ParserServicesWithTypeInformation,
  node: TSESTree.CallExpression,
): TSESTree.Expression | undefined {
  // If the call looks like `assert(expr1, expr2, ...c, d, e, f)`, then we can
  // only care if `expr1` or `expr2` is asserted, since anything that happens
  // within or after a spread argument is out of scope to reason about.
  const checkableArguments: TSESTree.Expression[] = [];
  for (const argument of node.arguments) {
    if (argument.type === AST_NODE_TYPES.SpreadElement) {
      break;
    }
    checkableArguments.push(argument);
  }

  // nothing to do
  if (checkableArguments.length === 0) {
    return undefined;
  }

  const checker = services.program.getTypeChecker();
  const tsNode = services.esTreeNodeToTSNodeMap.get(node);
  const signature = checker.getResolvedSignature(tsNode);

  if (signature == null) {
    return undefined;
  }

  const firstTypePredicateResult =
    checker.getTypePredicateOfSignature(signature);

  if (firstTypePredicateResult == null) {
    return undefined;
  }

  const { kind, parameterIndex, type } = firstTypePredicateResult;
  if (!(kind === ts.TypePredicateKind.AssertsIdentifier && type == null)) {
    return undefined;
  }

  return checkableArguments.at(parameterIndex);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Inspect a call expression to see if it's a call to an assertion function.
 * If it is, return the node of the argument that is asserted.
 */
```

- **Parameters**:
  - `services: ParserServicesWithTypeInformation`
  - `node: TSESTree.CallExpression`
- **Return Type**: `TSESTree.Expression | undefined`
- **Calls**:
  - `checkableArguments.push`
  - `services.program.getTypeChecker`
  - `services.esTreeNodeToTSNodeMap.get`
  - `checker.getResolvedSignature`
  - `checker.getTypePredicateOfSignature`
  - `checkableArguments.at`
- **Internal Comments**:
```
// If the call looks like `assert(expr1, expr2, ...c, d, e, f)`, then we can (x2)
// only care if `expr1` or `expr2` is asserted, since anything that happens (x2)
// within or after a spread argument is out of scope to reason about. (x2)
// nothing to do
```

### `findTypeGuardAssertedArgument(services: ParserServicesWithTypeInformation, node: TSESTree.CallExpression): | {
      argument: TSESTree.Expression;
      asserts: boolean;
      type: ts.Type;
    }
  | undefined`

<details><summary>Code</summary>

```ts
export function findTypeGuardAssertedArgument(
  services: ParserServicesWithTypeInformation,
  node: TSESTree.CallExpression,
):
  | {
      argument: TSESTree.Expression;
      asserts: boolean;
      type: ts.Type;
    }
  | undefined {
  // If the call looks like `assert(expr1, expr2, ...c, d, e, f)`, then we can
  // only care if `expr1` or `expr2` is asserted, since anything that happens
  // within or after a spread argument is out of scope to reason about.
  const checkableArguments: TSESTree.Expression[] = [];
  for (const argument of node.arguments) {
    if (argument.type === AST_NODE_TYPES.SpreadElement) {
      break;
    }
    checkableArguments.push(argument);
  }

  // nothing to do
  if (checkableArguments.length === 0) {
    return undefined;
  }

  const checker = services.program.getTypeChecker();
  const tsNode = services.esTreeNodeToTSNodeMap.get(node);
  const callSignature = checker.getResolvedSignature(tsNode);

  if (callSignature == null) {
    return undefined;
  }

  const typePredicateInfo = checker.getTypePredicateOfSignature(callSignature);

  if (typePredicateInfo == null) {
    return undefined;
  }

  const { kind, parameterIndex, type } = typePredicateInfo;
  if (
    !(
      (kind === ts.TypePredicateKind.AssertsIdentifier ||
        kind === ts.TypePredicateKind.Identifier) &&
      type != null
    )
  ) {
    return undefined;
  }

  if (parameterIndex >= checkableArguments.length) {
    return undefined;
  }

  return {
    argument: checkableArguments[parameterIndex],
    asserts: kind === ts.TypePredicateKind.AssertsIdentifier,
    type,
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Inspect a call expression to see if it's a call to an assertion function.
 * If it is, return the node of the argument that is asserted and other useful info.
 */
```

- **Parameters**:
  - `services: ParserServicesWithTypeInformation`
  - `node: TSESTree.CallExpression`
- **Return Type**: `| {
      argument: TSESTree.Expression;
      asserts: boolean;
      type: ts.Type;
    }
  | undefined`
- **Calls**:
  - `checkableArguments.push`
  - `services.program.getTypeChecker`
  - `services.esTreeNodeToTSNodeMap.get`
  - `checker.getResolvedSignature`
  - `checker.getTypePredicateOfSignature`
- **Internal Comments**:
```
// If the call looks like `assert(expr1, expr2, ...c, d, e, f)`, then we can (x2)
// only care if `expr1` or `expr2` is asserted, since anything that happens (x2)
// within or after a spread argument is out of scope to reason about. (x2)
// nothing to do
```


---