[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `no-unused-vars-eslint.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 6 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/no-unused-vars/no-unused-vars-eslint.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TestCaseError` | `@typescript-eslint/rule-tester` |
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `MessageIds` | `../../../src/rules/no-unused-vars` |
| `rule` | `../../../src/rules/no-unused-vars` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      // espree defaults to `script`, so we need to mirror it
      sourceType: 'script',
    },
  },
})` | ✗ |


---

## Functions

### `create(context: any): { ReturnStatement: (node: TSESTree.Node) => void; VariableDeclaration: (node: TSESTree.Node) => void; }`

<details><summary>Code</summary>

```ts
context => {
    /**
     * Mark a variable as used
     */
    function useA(node: TSESTree.Node): void {
      context.sourceCode.markVariableAsUsed('a', node);
    }
    return {
      ReturnStatement: useA,
      VariableDeclaration: useA,
    };
  }
```
</details>

- **Parameters**:
  - `context: any`
- **Return Type**: `{ ReturnStatement: (node: TSESTree.Node) => void; VariableDeclaration: (node: TSESTree.Node) => void; }`
- **Calls**:
  - `context.sourceCode.markVariableAsUsed`
- **Internal Comments**:
```
/**
     * Mark a variable as used
     */
```

### `useA(node: TSESTree.Node): void`

<details><summary>Code</summary>

```ts
function useA(node: TSESTree.Node): void {
      context.sourceCode.markVariableAsUsed('a', node);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Mark a variable as used
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.markVariableAsUsed`
### `create(context: any): { ReturnStatement: (node: TSESTree.Node) => void; VariableDeclaration: (node: TSESTree.Node) => void; }`

<details><summary>Code</summary>

```ts
context => {
    /**
     * Mark a variable as used
     */
    function useA(node: TSESTree.Node): void {
      context.sourceCode.markVariableAsUsed('a', node);
    }
    return {
      ReturnStatement: useA,
      VariableDeclaration: useA,
    };
  }
```
</details>

- **Parameters**:
  - `context: any`
- **Return Type**: `{ ReturnStatement: (node: TSESTree.Node) => void; VariableDeclaration: (node: TSESTree.Node) => void; }`
- **Calls**:
  - `context.sourceCode.markVariableAsUsed`
- **Internal Comments**:
```
/**
     * Mark a variable as used
     */
```

### `definedError(varName: string, additional: string): TestCaseError<MessageIds>`

<details><summary>Code</summary>

```ts
function definedError(
  varName: string,
  additional = '',
): TestCaseError<MessageIds> {
  return {
    data: {
      action: 'defined',
      additional,
      varName,
    },
    messageId: 'unusedVar',
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns an expected error for defined-but-not-used variables.
 * @param varName The name of the variable
 * @param [additional] The additional text for the message data
 * @param [type] The node type (defaults to "Identifier")
 * @returns An expected error object
 */
```

- **Parameters**:
  - `varName: string`
  - `additional: string`
- **Return Type**: `TestCaseError<MessageIds>`
### `assignedError(varName: string, additional: string): TestCaseError<MessageIds>`

<details><summary>Code</summary>

```ts
function assignedError(
  varName: string,
  additional = '',
): TestCaseError<MessageIds> {
  return {
    data: {
      action: 'assigned a value',
      additional,
      varName,
    },
    messageId: 'unusedVar',
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns an expected error for assigned-but-not-used variables.
 * @param varName The name of the variable
 * @param [additional] The additional text for the message data
 * @param [type] The node type (defaults to "Identifier")
 * @returns An expected error object
 */
```

- **Parameters**:
  - `varName: string`
  - `additional: string`
- **Return Type**: `TestCaseError<MessageIds>`
### `usedIgnoredError(varName: string, additional: string, type: any): TestCaseError<MessageIds>`

<details><summary>Code</summary>

```ts
function usedIgnoredError(
  varName: string,
  additional = '',
  type = AST_NODE_TYPES.Identifier,
): TestCaseError<MessageIds> {
  return {
    data: {
      additional,
      varName,
    },
    messageId: 'usedIgnoredVar',
    type,
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns an expected error for used-but-ignored variables.
 * @param varName The name of the variable
 * @param [additional] The additional text for the message data
 * @param [type] The node type (defaults to "Identifier")
 * @returns An expected error object
 */
```

- **Parameters**:
  - `varName: string`
  - `additional: string`
  - `type: any`
- **Return Type**: `TestCaseError<MessageIds>`

---