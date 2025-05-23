[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getContextualType.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/type-utils/src/getContextualType.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `getContextualType(checker: ts.TypeChecker, node: ts.Expression): ts.Type | undefined`

<details><summary>Code</summary>

```ts
export function getContextualType(
  checker: ts.TypeChecker,
  node: ts.Expression,
): ts.Type | undefined {
  const parent = node.parent;

  if (ts.isCallExpression(parent) || ts.isNewExpression(parent)) {
    if (node === parent.expression) {
      // is the callee, so has no contextual type
      return;
    }
  } else if (
    ts.isVariableDeclaration(parent) ||
    ts.isPropertyDeclaration(parent) ||
    ts.isParameter(parent)
  ) {
    return parent.type ? checker.getTypeFromTypeNode(parent.type) : undefined;
  } else if (ts.isJsxExpression(parent)) {
    return checker.getContextualType(parent);
  } else if (
    ts.isIdentifier(node) &&
    (ts.isPropertyAssignment(parent) ||
      ts.isShorthandPropertyAssignment(parent))
  ) {
    return checker.getContextualType(node);
  } else if (
    ts.isBinaryExpression(parent) &&
    parent.operatorToken.kind === ts.SyntaxKind.EqualsToken &&
    parent.right === node
  ) {
    // is RHS of assignment
    return checker.getTypeAtLocation(parent.left);
  } else if (
    ![ts.SyntaxKind.JsxExpression, ts.SyntaxKind.TemplateSpan].includes(
      parent.kind,
    )
  ) {
    // parent is not something we know we can get the contextual type of
    return;
  }
  // TODO - support return statement checking

  return checker.getContextualType(node);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns the contextual type of a given node.
 * Contextual type is the type of the target the node is going into.
 * i.e. the type of a called function's parameter, or the defined type of a variable declaration
 */
```

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `node: ts.Expression`
- **Return Type**: `ts.Type | undefined`
- **Calls**:
  - `ts.isCallExpression`
  - `ts.isNewExpression`
  - `ts.isVariableDeclaration`
  - `ts.isPropertyDeclaration`
  - `ts.isParameter`
  - `checker.getTypeFromTypeNode`
  - `ts.isJsxExpression`
  - `checker.getContextualType`
  - `ts.isIdentifier`
  - `ts.isPropertyAssignment`
  - `ts.isShorthandPropertyAssignment`
  - `ts.isBinaryExpression`
  - `checker.getTypeAtLocation`
  - `[ts.SyntaxKind.JsxExpression, ts.SyntaxKind.TemplateSpan].includes`
- **Internal Comments**:
```
// is the callee, so has no contextual type
// is RHS of assignment
// parent is not something we know we can get the contextual type of
// TODO - support return statement checking
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