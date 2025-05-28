[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ExportVisitor.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 5 |
| 🧱 Classes | 1 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Classes](#classes)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/referencer/ExportVisitor.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `Referencer` | `./Referencer` |
| `Visitor` | `./Visitor` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `exportReferencer` | `ExportVisitor` | const | `new ExportVisitor(node, referencer)` | ✗ |


---

## Functions

### `ExportVisitor.visit(referencer: Referencer, node: ExportNode): void`

<details><summary>Code</summary>

```ts
static visit(referencer: Referencer, node: ExportNode): void {
    const exportReferencer = new ExportVisitor(node, referencer);
    exportReferencer.visit(node);
  }
```
</details>

- **Parameters**:
  - `referencer: Referencer`
  - `node: ExportNode`
- **Return Type**: `void`
- **Calls**:
  - `exportReferencer.visit`
### `ExportVisitor.ExportDefaultDeclaration(node: TSESTree.ExportDefaultDeclaration): void`

<details><summary>Code</summary>

```ts
protected ExportDefaultDeclaration(
    node: TSESTree.ExportDefaultDeclaration,
  ): void {
    if (node.declaration.type === AST_NODE_TYPES.Identifier) {
      // export default A;
      // this could be a type or a variable
      this.visit(node.declaration);
    } else {
      // export const a = 1;
      // export something();
      // etc
      // these not included in the scope of this visitor as they are all guaranteed to be values or declare variables
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ExportDefaultDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
- **Internal Comments**:
```
// export default A; (x4)
// this could be a type or a variable (x4)
```

### `ExportVisitor.ExportNamedDeclaration(node: TSESTree.ExportNamedDeclaration): void`

<details><summary>Code</summary>

```ts
protected ExportNamedDeclaration(
    node: TSESTree.ExportNamedDeclaration,
  ): void {
    if (node.source) {
      // export ... from 'foo';
      // these are external identifiers so there shouldn't be references or defs
      return;
    }

    if (!node.declaration) {
      // export { x };
      this.visitChildren(node);
    } else {
      // export const x = 1;
      // this is not included in the scope of this visitor as it creates a variable
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ExportNamedDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.visitChildren`
- **Internal Comments**:
```
// export ... from 'foo';
// these are external identifiers so there shouldn't be references or defs
// export { x }; (x4)
```

### `ExportVisitor.ExportSpecifier(node: TSESTree.ExportSpecifier): void`

<details><summary>Code</summary>

```ts
protected ExportSpecifier(node: TSESTree.ExportSpecifier): void {
    if (
      node.exportKind === 'type' &&
      node.local.type === AST_NODE_TYPES.Identifier
    ) {
      // export { type T };
      // type exports can only reference types
      //
      // we can't let this fall through to the Identifier selector because the exportKind is on this node
      // and we don't have access to the `.parent` during scope analysis
      this.#referencer.currentScope().referenceType(node.local);
    } else {
      this.visit(node.local);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ExportSpecifier`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.currentScope().referenceType`
  - `this.visit`
- **Internal Comments**:
```
// export { type T }; (x7)
// type exports can only reference types (x7)
// (x7)
// we can't let this fall through to the Identifier selector because the exportKind is on this node (x7)
// and we don't have access to the `.parent` during scope analysis (x7)
```

### `ExportVisitor.Identifier(node: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
protected Identifier(node: TSESTree.Identifier): void {
    if (this.#exportNode.exportKind === 'type') {
      // export type { T };
      // type exports can only reference types
      this.#referencer.currentScope().referenceType(node);
    } else {
      this.#referencer.currentScope().referenceDualValueType(node);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Identifier`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.currentScope().referenceType`
  - `this.#referencer.currentScope().referenceDualValueType`
- **Internal Comments**:
```
// export type { T }; (x7)
// type exports can only reference types (x7)
```


---

## Classes

### `ExportVisitor`

<details><summary>Class Code</summary>

```ts
export class ExportVisitor extends Visitor {
  readonly #exportNode: ExportNode;
  readonly #referencer: Referencer;

  constructor(node: ExportNode, referencer: Referencer) {
    super(referencer);
    this.#exportNode = node;
    this.#referencer = referencer;
  }

  static visit(referencer: Referencer, node: ExportNode): void {
    const exportReferencer = new ExportVisitor(node, referencer);
    exportReferencer.visit(node);
  }

  protected ExportDefaultDeclaration(
    node: TSESTree.ExportDefaultDeclaration,
  ): void {
    if (node.declaration.type === AST_NODE_TYPES.Identifier) {
      // export default A;
      // this could be a type or a variable
      this.visit(node.declaration);
    } else {
      // export const a = 1;
      // export something();
      // etc
      // these not included in the scope of this visitor as they are all guaranteed to be values or declare variables
    }
  }

  protected ExportNamedDeclaration(
    node: TSESTree.ExportNamedDeclaration,
  ): void {
    if (node.source) {
      // export ... from 'foo';
      // these are external identifiers so there shouldn't be references or defs
      return;
    }

    if (!node.declaration) {
      // export { x };
      this.visitChildren(node);
    } else {
      // export const x = 1;
      // this is not included in the scope of this visitor as it creates a variable
    }
  }

  protected ExportSpecifier(node: TSESTree.ExportSpecifier): void {
    if (
      node.exportKind === 'type' &&
      node.local.type === AST_NODE_TYPES.Identifier
    ) {
      // export { type T };
      // type exports can only reference types
      //
      // we can't let this fall through to the Identifier selector because the exportKind is on this node
      // and we don't have access to the `.parent` during scope analysis
      this.#referencer.currentScope().referenceType(node.local);
    } else {
      this.visit(node.local);
    }
  }

  protected Identifier(node: TSESTree.Identifier): void {
    if (this.#exportNode.exportKind === 'type') {
      // export type { T };
      // type exports can only reference types
      this.#referencer.currentScope().referenceType(node);
    } else {
      this.#referencer.currentScope().referenceDualValueType(node);
    }
  }
}
```
</details>

#### Methods

##### `visit(referencer: Referencer, node: ExportNode): void`

<details><summary>Code</summary>

```ts
static visit(referencer: Referencer, node: ExportNode): void {
    const exportReferencer = new ExportVisitor(node, referencer);
    exportReferencer.visit(node);
  }
```
</details>

##### `ExportDefaultDeclaration(node: TSESTree.ExportDefaultDeclaration): void`

<details><summary>Code</summary>

```ts
protected ExportDefaultDeclaration(
    node: TSESTree.ExportDefaultDeclaration,
  ): void {
    if (node.declaration.type === AST_NODE_TYPES.Identifier) {
      // export default A;
      // this could be a type or a variable
      this.visit(node.declaration);
    } else {
      // export const a = 1;
      // export something();
      // etc
      // these not included in the scope of this visitor as they are all guaranteed to be values or declare variables
    }
  }
```
</details>

##### `ExportNamedDeclaration(node: TSESTree.ExportNamedDeclaration): void`

<details><summary>Code</summary>

```ts
protected ExportNamedDeclaration(
    node: TSESTree.ExportNamedDeclaration,
  ): void {
    if (node.source) {
      // export ... from 'foo';
      // these are external identifiers so there shouldn't be references or defs
      return;
    }

    if (!node.declaration) {
      // export { x };
      this.visitChildren(node);
    } else {
      // export const x = 1;
      // this is not included in the scope of this visitor as it creates a variable
    }
  }
```
</details>

##### `ExportSpecifier(node: TSESTree.ExportSpecifier): void`

<details><summary>Code</summary>

```ts
protected ExportSpecifier(node: TSESTree.ExportSpecifier): void {
    if (
      node.exportKind === 'type' &&
      node.local.type === AST_NODE_TYPES.Identifier
    ) {
      // export { type T };
      // type exports can only reference types
      //
      // we can't let this fall through to the Identifier selector because the exportKind is on this node
      // and we don't have access to the `.parent` during scope analysis
      this.#referencer.currentScope().referenceType(node.local);
    } else {
      this.visit(node.local);
    }
  }
```
</details>

##### `Identifier(node: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
protected Identifier(node: TSESTree.Identifier): void {
    if (this.#exportNode.exportKind === 'type') {
      // export type { T };
      // type exports can only reference types
      this.#referencer.currentScope().referenceType(node);
    } else {
      this.#referencer.currentScope().referenceDualValueType(node);
    }
  }
```
</details>


---

## Type Aliases

### `ExportNode`

```ts
type ExportNode = | TSESTree.ExportAllDeclaration
  | TSESTree.ExportDefaultDeclaration
  | TSESTree.ExportNamedDeclaration;
```


---