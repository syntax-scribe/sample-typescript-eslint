[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `consistent-type-definitions.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 3 |
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
📂 **`packages/eslint-plugin/src/rules/consistent-type-definitions.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `typeNode` | `any` | const | `node.typeParameters ?? node.id` | ✗ |
| `fixes` | `TSESLint.RuleFix[]` | const | `[]` | ✗ |
| `fix` | `(fixer: TSESLint.RuleFixer) => TSESLint.RuleFix[]` | const | `isCurrentlyTraversedNodeWithinModuleDeclaration(node)
            ? null
            : (fixer: TSESLint.RuleFixer): TSESLint.RuleFix[] => {
                const typeNode = node.typeParameters ?? node.id;
                const fixes: TSESLint.RuleFix[] = [];

                const firstToken = context.sourceCode.getTokenBefore(node.id);
                if (firstToken) {
                  fixes.push(fixer.replaceText(firstToken, 'type'));
                  fixes.push(
                    fixer.replaceTextRange(
                      [typeNode.range[1], node.body.range[0]],
                      ' = ',
                    ),
                  );
                }

                node.extends.forEach(heritage => {
                  const typeIdentifier = context.sourceCode.getText(heritage);
                  fixes.push(
                    fixer.insertTextAfter(node.body, ` & ${typeIdentifier}`),
                  );
                });

                if (
                  node.parent.type === AST_NODE_TYPES.ExportDefaultDeclaration
                ) {
                  fixes.push(
                    fixer.removeRange([node.parent.range[0], node.range[0]]),
                    fixer.insertTextAfter(
                      node.body,
                      `\nexport default ${node.id.name}`,
                    ),
                  );
                }

                return fixes;
              }` | ✗ |


---

## Functions

### `isCurrentlyTraversedNodeWithinModuleDeclaration(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isCurrentlyTraversedNodeWithinModuleDeclaration(
      node: TSESTree.Node,
    ): boolean {
      return context.sourceCode
        .getAncestors(node)
        .some(
          node =>
            node.type === AST_NODE_TYPES.TSModuleDeclaration &&
            node.declare &&
            node.kind === 'global',
        );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Iterates from the highest parent to the currently traversed node
     * to determine whether any node in tree is globally declared module declaration
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `context.sourceCode
        .getAncestors(node)
        .some`

---