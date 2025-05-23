[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `VisitorBase.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 4
- **Classes**: 1
- **Imports**: 4
- **Interfaces**: 1
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/scope-manager/src/referencer/VisitorBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `TSESTree` | `@typescript-eslint/types` |
| `VisitorKeys` | `@typescript-eslint/visitor-keys` |
| `visitorKeys` | `@typescript-eslint/visitor-keys` |


---

## Functions

### `isObject(obj: unknown): obj is Record<string, unknown>`

<details><summary>Code</summary>

```ts
function isObject(obj: unknown): obj is Record<string, unknown> {
  return typeof obj === 'object' && obj != null;
}
```
</details>

- **Parameters**:
  - `obj: unknown`
- **Return Type**: `obj is Record<string, unknown>`
### `isNode(node: unknown): node is TSESTree.Node`

<details><summary>Code</summary>

```ts
function isNode(node: unknown): node is TSESTree.Node {
  return isObject(node) && typeof node.type === 'string';
}
```
</details>

- **Parameters**:
  - `node: unknown`
- **Return Type**: `node is TSESTree.Node`
- **Calls**:
  - `isObject`
### `VisitorBase.visitChildren(node: T | null | undefined, excludeArr: (keyof T)[]): void`

<details><summary>Code</summary>

```ts
visitChildren<T extends TSESTree.Node>(
    node: T | null | undefined,
    excludeArr: (keyof T)[] = [],
  ): void {
    if (node?.type == null) {
      return;
    }

    const exclude = new Set([...excludeArr, 'parent'] as string[]);
    const children = this.#childVisitorKeys[node.type] ?? Object.keys(node);
    for (const key of children) {
      if (exclude.has(key)) {
        continue;
      }

      const child = node[key as keyof TSESTree.Node] as unknown;
      if (!child) {
        continue;
      }

      if (Array.isArray(child)) {
        for (const subChild of child) {
          if (isNode(subChild)) {
            this.visit(subChild);
          }
        }
      } else if (isNode(child)) {
        this.visit(child);
      }
    }
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Default method for visiting children.
   * @param node the node whose children should be visited
   * @param excludeArr a list of keys to not visit
   */
```

- **Parameters**:
  - `node: T | null | undefined`
  - `excludeArr: (keyof T)[]`
- **Return Type**: `void`
- **Calls**:
  - `Object.keys`
  - `exclude.has`
  - `Array.isArray`
  - `isNode`
  - `this.visit`
### `VisitorBase.visit(node: TSESTree.Node | null | undefined): void`

<details><summary>Code</summary>

```ts
visit(node: TSESTree.Node | null | undefined): void {
    if (node?.type == null) {
      return;
    }

    const visitor = (this as NodeVisitor)[node.type];
    if (visitor) {
      visitor.call(this, node);
      if (!this.#visitChildrenEvenIfSelectorExists) {
        return;
      }
    }

    this.visitChildren(node);
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Dispatching node.
   */
```

- **Parameters**:
  - `node: TSESTree.Node | null | undefined`
- **Return Type**: `void`
- **Calls**:
  - `visitor.call`
  - `this.visitChildren`

---

## Classes

### `VisitorBase`

<details><summary>Class Code</summary>

```ts
export abstract class VisitorBase {
  readonly #childVisitorKeys: VisitorKeys;
  readonly #visitChildrenEvenIfSelectorExists: boolean;
  constructor(options: VisitorOptions) {
    this.#childVisitorKeys = options.childVisitorKeys ?? visitorKeys;
    this.#visitChildrenEvenIfSelectorExists =
      options.visitChildrenEvenIfSelectorExists ?? false;
  }

  /**
   * Default method for visiting children.
   * @param node the node whose children should be visited
   * @param excludeArr a list of keys to not visit
   */
  visitChildren<T extends TSESTree.Node>(
    node: T | null | undefined,
    excludeArr: (keyof T)[] = [],
  ): void {
    if (node?.type == null) {
      return;
    }

    const exclude = new Set([...excludeArr, 'parent'] as string[]);
    const children = this.#childVisitorKeys[node.type] ?? Object.keys(node);
    for (const key of children) {
      if (exclude.has(key)) {
        continue;
      }

      const child = node[key as keyof TSESTree.Node] as unknown;
      if (!child) {
        continue;
      }

      if (Array.isArray(child)) {
        for (const subChild of child) {
          if (isNode(subChild)) {
            this.visit(subChild);
          }
        }
      } else if (isNode(child)) {
        this.visit(child);
      }
    }
  }

  /**
   * Dispatching node.
   */
  visit(node: TSESTree.Node | null | undefined): void {
    if (node?.type == null) {
      return;
    }

    const visitor = (this as NodeVisitor)[node.type];
    if (visitor) {
      visitor.call(this, node);
      if (!this.#visitChildrenEvenIfSelectorExists) {
        return;
      }
    }

    this.visitChildren(node);
  }
}
```
</details>

#### Methods

##### `visitChildren(node: T | null | undefined, excludeArr: (keyof T)[]): void`

<details><summary>Code</summary>

```ts
visitChildren<T extends TSESTree.Node>(
    node: T | null | undefined,
    excludeArr: (keyof T)[] = [],
  ): void {
    if (node?.type == null) {
      return;
    }

    const exclude = new Set([...excludeArr, 'parent'] as string[]);
    const children = this.#childVisitorKeys[node.type] ?? Object.keys(node);
    for (const key of children) {
      if (exclude.has(key)) {
        continue;
      }

      const child = node[key as keyof TSESTree.Node] as unknown;
      if (!child) {
        continue;
      }

      if (Array.isArray(child)) {
        for (const subChild of child) {
          if (isNode(subChild)) {
            this.visit(subChild);
          }
        }
      } else if (isNode(child)) {
        this.visit(child);
      }
    }
  }
```
</details>

##### `visit(node: TSESTree.Node | null | undefined): void`

<details><summary>Code</summary>

```ts
visit(node: TSESTree.Node | null | undefined): void {
    if (node?.type == null) {
      return;
    }

    const visitor = (this as NodeVisitor)[node.type];
    if (visitor) {
      visitor.call(this, node);
      if (!this.#visitChildrenEvenIfSelectorExists) {
        return;
      }
    }

    this.visitChildren(node);
  }
```
</details>


---

## Interfaces

### `VisitorOptions`

<details><summary>Interface Code</summary>

```ts
export interface VisitorOptions {
  childVisitorKeys?: VisitorKeys | null;
  visitChildrenEvenIfSelectorExists?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `childVisitorKeys` | `VisitorKeys | null` | ✓ |  |
| `visitChildrenEvenIfSelectorExists` | `boolean` | ✓ |  |


---

## Type Aliases

### `NodeVisitor`

```ts
type NodeVisitor = Partial<
  Record<AST_NODE_TYPES, (node: TSESTree.Node) => void>
>;
```


---