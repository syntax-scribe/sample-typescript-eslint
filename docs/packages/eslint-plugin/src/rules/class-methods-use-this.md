[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `class-methods-use-this.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 6 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 4 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 3 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/class-methods-use-this.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getFunctionHeadLoc` | `../util` |
| `getFunctionNameWithKind` | `../util` |
| `getStaticMemberAccessValue` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `exceptMethods` | `Set<unknown>` | const | `new Set(exceptMethodsRaw)` | ✗ |
| `stack` | `Stack | undefined` | let/var | `*not shown*` | ✗ |
| `oldStack` | `Stack` | const | `stack` | ✗ |
| `hashIfNeeded` | `"" | "#"` | const | `node.key.type === AST_NODE_TYPES.PrivateIdentifier ? '#' : ''` | ✗ |


---

## Functions

### `pushContext(member: | TSESTree.AccessorProperty
        | TSESTree.MethodDefinition
        | TSESTree.PropertyDefinition): void`

<details><summary>Code</summary>

```ts
function pushContext(
      member?:
        | TSESTree.AccessorProperty
        | TSESTree.MethodDefinition
        | TSESTree.PropertyDefinition,
    ): void {
      if (member?.parent.type === AST_NODE_TYPES.ClassBody) {
        stack = {
          class: member.parent.parent,
          member,
          parent: stack,
          usesThis: false,
        };
      } else {
        stack = {
          class: null,
          member: null,
          parent: stack,
          usesThis: false,
        };
      }
    }
```
</details>

- **Parameters**:
  - `member: | TSESTree.AccessorProperty
        | TSESTree.MethodDefinition
        | TSESTree.PropertyDefinition`
- **Return Type**: `void`
### `enterFunction(node: TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression): void`

<details><summary>Code</summary>

```ts
function enterFunction(
      node: TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression,
    ): void {
      if (
        node.parent.type === AST_NODE_TYPES.MethodDefinition ||
        node.parent.type === AST_NODE_TYPES.PropertyDefinition ||
        node.parent.type === AST_NODE_TYPES.AccessorProperty
      ) {
        pushContext(node.parent);
      } else {
        pushContext();
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression`
- **Return Type**: `void`
- **Calls**:
  - `pushContext`
### `popContext(): Stack | undefined`

<details><summary>Code</summary>

```ts
function popContext(): Stack | undefined {
      const oldStack = stack;
      stack = stack?.parent;
      return oldStack;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Pop `this` used flag from the stack.
     */
```

- **Return Type**: `Stack | undefined`
### `isPublicField(accessibility: TSESTree.Accessibility | undefined): boolean`

<details><summary>Code</summary>

```ts
function isPublicField(
      accessibility: TSESTree.Accessibility | undefined,
    ): boolean {
      if (!accessibility || accessibility === 'public') {
        return true;
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `accessibility: TSESTree.Accessibility | undefined`
- **Return Type**: `boolean`
### `isIncludedInstanceMethod(node: NonNullable<Stack['member']>): node is NonNullable<Stack['member']>`

<details><summary>Code</summary>

```ts
function isIncludedInstanceMethod(
      node: NonNullable<Stack['member']>,
    ): node is NonNullable<Stack['member']> {
      if (
        node.static ||
        (node.type === AST_NODE_TYPES.MethodDefinition &&
          node.kind === 'constructor') ||
        ((node.type === AST_NODE_TYPES.PropertyDefinition ||
          node.type === AST_NODE_TYPES.AccessorProperty) &&
          !enforceForClassFields)
      ) {
        return false;
      }

      if (node.computed || exceptMethods.size === 0) {
        return true;
      }

      const hashIfNeeded =
        node.key.type === AST_NODE_TYPES.PrivateIdentifier ? '#' : '';
      const name = getStaticMemberAccessValue(node, context);

      return (
        typeof name !== 'string' || !exceptMethods.has(hashIfNeeded + name)
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if the node is an instance method not excluded by config
     */
```

- **Parameters**:
  - `node: NonNullable<Stack['member']>`
- **Return Type**: `node is NonNullable<Stack['member']>`
- **Calls**:
  - `getStaticMemberAccessValue (from ../util)`
  - `exceptMethods.has`
### `exitFunction(node: TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression): void`

<details><summary>Code</summary>

```ts
function exitFunction(
      node: TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression,
    ): void {
      const stackContext = popContext();
      if (
        stackContext?.member == null ||
        stackContext.usesThis ||
        (ignoreOverrideMethods && stackContext.member.override) ||
        (ignoreClassesThatImplementAnInterface === true &&
          stackContext.class.implements.length > 0) ||
        (ignoreClassesThatImplementAnInterface === 'public-fields' &&
          stackContext.class.implements.length > 0 &&
          isPublicField(stackContext.member.accessibility))
      ) {
        return;
      }

      if (isIncludedInstanceMethod(stackContext.member)) {
        context.report({
          loc: getFunctionHeadLoc(node, context.sourceCode),
          node,
          messageId: 'missingThis',
          data: {
            name: getFunctionNameWithKind(node),
          },
        });
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if we are leaving a function that is a method, and reports if 'this' has not been used.
     * Static methods and the constructor are exempt.
     * Then pops the context off the stack.
     */
```

- **Parameters**:
  - `node: TSESTree.ArrowFunctionExpression | TSESTree.FunctionExpression`
- **Return Type**: `void`
- **Calls**:
  - `popContext`
  - `isPublicField`
  - `isIncludedInstanceMethod`
  - `context.report`
  - `getFunctionHeadLoc (from ../util)`
  - `getFunctionNameWithKind (from ../util)`

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    enforceForClassFields?: boolean;
    exceptMethods?: string[];
    ignoreClassesThatImplementAnInterface?: boolean | 'public-fields';
    ignoreOverrideMethods?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'missingThis';
```

### `Stack`

```ts
type Stack = | {
          class: null;
          member: null;
          parent: Stack | undefined;
          usesThis: boolean;
        }
      | {
          class: TSESTree.ClassDeclaration | TSESTree.ClassExpression;
          member:
            | TSESTree.AccessorProperty
            | TSESTree.MethodDefinition
            | TSESTree.PropertyDefinition;
          parent: Stack | undefined;
          usesThis: boolean;
        };
```


---