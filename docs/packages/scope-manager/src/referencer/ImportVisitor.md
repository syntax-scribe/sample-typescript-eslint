[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ImportVisitor.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 5
- **Classes**: 1
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/referencer/ImportVisitor.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `Referencer` | `./Referencer` |
| `ImportBindingDefinition` | `../definition` |
| `Visitor` | `./Visitor` |


---

## Functions

### `ImportVisitor.visit(referencer: Referencer, declaration: TSESTree.ImportDeclaration): void`

<details><summary>Code</summary>

```ts
static visit(
    referencer: Referencer,
    declaration: TSESTree.ImportDeclaration,
  ): void {
    const importReferencer = new ImportVisitor(declaration, referencer);
    importReferencer.visit(declaration);
  }
```
</details>

- **Parameters**:
  - `referencer: Referencer`
  - `declaration: TSESTree.ImportDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `importReferencer.visit`
### `ImportVisitor.ImportDefaultSpecifier(node: TSESTree.ImportDefaultSpecifier): void`

<details><summary>Code</summary>

```ts
protected ImportDefaultSpecifier(
    node: TSESTree.ImportDefaultSpecifier,
  ): void {
    const local = node.local;
    this.visitImport(local, node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ImportDefaultSpecifier`
- **Return Type**: `void`
- **Calls**:
  - `this.visitImport`
### `ImportVisitor.ImportNamespaceSpecifier(node: TSESTree.ImportNamespaceSpecifier): void`

<details><summary>Code</summary>

```ts
protected ImportNamespaceSpecifier(
    node: TSESTree.ImportNamespaceSpecifier,
  ): void {
    const local = node.local;
    this.visitImport(local, node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ImportNamespaceSpecifier`
- **Return Type**: `void`
- **Calls**:
  - `this.visitImport`
### `ImportVisitor.ImportSpecifier(node: TSESTree.ImportSpecifier): void`

<details><summary>Code</summary>

```ts
protected ImportSpecifier(node: TSESTree.ImportSpecifier): void {
    const local = node.local;
    this.visitImport(local, node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ImportSpecifier`
- **Return Type**: `void`
- **Calls**:
  - `this.visitImport`
### `ImportVisitor.visitImport(id: TSESTree.Identifier, specifier: | TSESTree.ImportDefaultSpecifier
      | TSESTree.ImportNamespaceSpecifier
      | TSESTree.ImportSpecifier): void`

<details><summary>Code</summary>

```ts
protected visitImport(
    id: TSESTree.Identifier,
    specifier:
      | TSESTree.ImportDefaultSpecifier
      | TSESTree.ImportNamespaceSpecifier
      | TSESTree.ImportSpecifier,
  ): void {
    this.#referencer
      .currentScope()
      .defineIdentifier(
        id,
        new ImportBindingDefinition(id, specifier, this.#declaration),
      );
  }
```
</details>

- **Parameters**:
  - `id: TSESTree.Identifier`
  - `specifier: | TSESTree.ImportDefaultSpecifier
      | TSESTree.ImportNamespaceSpecifier
      | TSESTree.ImportSpecifier`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer
      .currentScope()
      .defineIdentifier`

---

## Classes

### `ImportVisitor`

<details><summary>Class Code</summary>

```ts
export class ImportVisitor extends Visitor {
  readonly #declaration: TSESTree.ImportDeclaration;
  readonly #referencer: Referencer;

  constructor(declaration: TSESTree.ImportDeclaration, referencer: Referencer) {
    super(referencer);
    this.#declaration = declaration;
    this.#referencer = referencer;
  }

  static visit(
    referencer: Referencer,
    declaration: TSESTree.ImportDeclaration,
  ): void {
    const importReferencer = new ImportVisitor(declaration, referencer);
    importReferencer.visit(declaration);
  }

  protected ImportDefaultSpecifier(
    node: TSESTree.ImportDefaultSpecifier,
  ): void {
    const local = node.local;
    this.visitImport(local, node);
  }

  protected ImportNamespaceSpecifier(
    node: TSESTree.ImportNamespaceSpecifier,
  ): void {
    const local = node.local;
    this.visitImport(local, node);
  }

  protected ImportSpecifier(node: TSESTree.ImportSpecifier): void {
    const local = node.local;
    this.visitImport(local, node);
  }

  protected visitImport(
    id: TSESTree.Identifier,
    specifier:
      | TSESTree.ImportDefaultSpecifier
      | TSESTree.ImportNamespaceSpecifier
      | TSESTree.ImportSpecifier,
  ): void {
    this.#referencer
      .currentScope()
      .defineIdentifier(
        id,
        new ImportBindingDefinition(id, specifier, this.#declaration),
      );
  }
}
```
</details>

#### Methods

##### `visit(referencer: Referencer, declaration: TSESTree.ImportDeclaration): void`

<details><summary>Code</summary>

```ts
static visit(
    referencer: Referencer,
    declaration: TSESTree.ImportDeclaration,
  ): void {
    const importReferencer = new ImportVisitor(declaration, referencer);
    importReferencer.visit(declaration);
  }
```
</details>

##### `ImportDefaultSpecifier(node: TSESTree.ImportDefaultSpecifier): void`

<details><summary>Code</summary>

```ts
protected ImportDefaultSpecifier(
    node: TSESTree.ImportDefaultSpecifier,
  ): void {
    const local = node.local;
    this.visitImport(local, node);
  }
```
</details>

##### `ImportNamespaceSpecifier(node: TSESTree.ImportNamespaceSpecifier): void`

<details><summary>Code</summary>

```ts
protected ImportNamespaceSpecifier(
    node: TSESTree.ImportNamespaceSpecifier,
  ): void {
    const local = node.local;
    this.visitImport(local, node);
  }
```
</details>

##### `ImportSpecifier(node: TSESTree.ImportSpecifier): void`

<details><summary>Code</summary>

```ts
protected ImportSpecifier(node: TSESTree.ImportSpecifier): void {
    const local = node.local;
    this.visitImport(local, node);
  }
```
</details>

##### `visitImport(id: TSESTree.Identifier, specifier: | TSESTree.ImportDefaultSpecifier
      | TSESTree.ImportNamespaceSpecifier
      | TSESTree.ImportSpecifier): void`

<details><summary>Code</summary>

```ts
protected visitImport(
    id: TSESTree.Identifier,
    specifier:
      | TSESTree.ImportDefaultSpecifier
      | TSESTree.ImportNamespaceSpecifier
      | TSESTree.ImportSpecifier,
  ): void {
    this.#referencer
      .currentScope()
      .defineIdentifier(
        id,
        new ImportBindingDefinition(id, specifier, this.#declaration),
      );
  }
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---