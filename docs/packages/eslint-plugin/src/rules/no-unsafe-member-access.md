[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unsafe-member-access.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 3 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Enums](#enums)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unsafe-member-access.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `getThisExpression` | `../util` |
| `isTypeAnyType` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `stateCache` | `Map<TSESTree.Node, State>` | const | `new Map<TSESTree.Node, State>()` | ✗ |
| `state` | `State` | const | `isTypeAnyType(type) ? State.Unsafe : State.Safe` | ✗ |
| `messageId` | `'unsafeMemberExpression' | 'unsafeThisMemberExpression'` | let/var | `'unsafeMemberExpression'` | ✗ |


---

## Functions

### `createDataType(type: ts.Type): '`any`' | '`error` typed'`

<details><summary>Code</summary>

```ts
function createDataType(type: ts.Type): '`any`' | '`error` typed' {
  const isErrorType = tsutils.isIntrinsicErrorType(type);
  return isErrorType ? '`error` typed' : '`any`';
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `'`any`' | '`error` typed'`
- **Calls**:
  - `tsutils.isIntrinsicErrorType`
### `checkMemberExpression(node: TSESTree.MemberExpression): State`

<details><summary>Code</summary>

```ts
function checkMemberExpression(node: TSESTree.MemberExpression): State {
      const cachedState = stateCache.get(node);
      if (cachedState) {
        return cachedState;
      }

      if (node.object.type === AST_NODE_TYPES.MemberExpression) {
        const objectState = checkMemberExpression(node.object);
        if (objectState === State.Unsafe) {
          // if the object is unsafe, we know this will be unsafe as well
          // we don't need to report, as we have already reported on the inner member expr
          stateCache.set(node, objectState);
          return objectState;
        }
      }

      const type = services.getTypeAtLocation(node.object);
      const state = isTypeAnyType(type) ? State.Unsafe : State.Safe;
      stateCache.set(node, state);

      if (state === State.Unsafe) {
        const propertyName = context.sourceCode.getText(node.property);

        let messageId: 'unsafeMemberExpression' | 'unsafeThisMemberExpression' =
          'unsafeMemberExpression';

        if (!isNoImplicitThis) {
          // `this.foo` or `this.foo[bar]`
          const thisExpression = getThisExpression(node);

          if (
            thisExpression &&
            isTypeAnyType(
              getConstrainedTypeAtLocation(services, thisExpression),
            )
          ) {
            messageId = 'unsafeThisMemberExpression';
          }
        }

        context.report({
          node: node.property,
          messageId,
          data: {
            type: createDataType(type),
            property: node.computed ? `[${propertyName}]` : `.${propertyName}`,
          },
        });
      }

      return state;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.MemberExpression`
- **Return Type**: `State`
- **Calls**:
  - `stateCache.get`
  - `checkMemberExpression`
  - `stateCache.set`
  - `services.getTypeAtLocation`
  - `isTypeAnyType (from ../util)`
  - `context.sourceCode.getText`
  - `getThisExpression (from ../util)`
  - `getConstrainedTypeAtLocation (from ../util)`
  - `context.report`
  - `createDataType`
- **Internal Comments**:
```
// if the object is unsafe, we know this will be unsafe as well (x4)
// we don't need to report, as we have already reported on the inner member expr (x4)
// `this.foo` or `this.foo[bar]` (x2)
```


---

## Enums

### `const enum State`

<details><summary>Enum Code</summary>

```ts
const enum State {
  Unsafe = 1,
  Safe = 2,
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `Unsafe` | `1` |  |
| `Safe` | `2` |  |


---