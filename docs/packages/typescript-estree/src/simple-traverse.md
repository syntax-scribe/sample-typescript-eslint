[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `simple-traverse.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 4
- **Classes**: 1
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/simple-traverse.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `VisitorKeys` | `@typescript-eslint/visitor-keys` |
| `visitorKeys` | `@typescript-eslint/visitor-keys` |
| `TSESTree` | `./ts-estree` |


---

## Functions

### `isValidNode(x: unknown): x is TSESTree.Node`

<details><summary>Code</summary>

```ts
function isValidNode(x: unknown): x is TSESTree.Node {
  return (
    typeof x === 'object' &&
    x != null &&
    'type' in x &&
    typeof x.type === 'string'
  );
}
```
</details>

- **Parameters**:
  - `x: unknown`
- **Return Type**: `x is TSESTree.Node`
### `getVisitorKeysForNode(allVisitorKeys: typeof visitorKeys, node: TSESTree.Node): readonly (keyof TSESTree.Node)[]`

<details><summary>Code</summary>

```ts
function getVisitorKeysForNode(
  allVisitorKeys: typeof visitorKeys,
  node: TSESTree.Node,
): readonly (keyof TSESTree.Node)[] {
  const keys = allVisitorKeys[node.type];
  return (keys ?? []) as never;
}
```
</details>

- **Parameters**:
  - `allVisitorKeys: typeof visitorKeys`
  - `node: TSESTree.Node`
- **Return Type**: `readonly (keyof TSESTree.Node)[]`
### `SimpleTraverser.traverse(node: unknown, parent: TSESTree.Node | undefined): void`

<details><summary>Code</summary>

```ts
traverse(node: unknown, parent: TSESTree.Node | undefined): void {
    if (!isValidNode(node)) {
      return;
    }

    if (this.setParentPointers) {
      node.parent = parent;
    }

    if ('enter' in this.selectors) {
      this.selectors.enter(node, parent);
    } else if (node.type in this.selectors.visitors) {
      this.selectors.visitors[node.type](node, parent);
    }

    const keys = getVisitorKeysForNode(this.allVisitorKeys, node);
    if (keys.length < 1) {
      return;
    }

    for (const key of keys) {
      const childOrChildren = node[key];

      if (Array.isArray(childOrChildren)) {
        for (const child of childOrChildren) {
          this.traverse(child, node);
        }
      } else {
        this.traverse(childOrChildren, node);
      }
    }
  }
```
</details>

- **Parameters**:
  - `node: unknown`
  - `parent: TSESTree.Node | undefined`
- **Return Type**: `void`
- **Calls**:
  - `isValidNode`
  - `this.selectors.enter`
  - `complex_call_1689`
  - `getVisitorKeysForNode`
  - `Array.isArray`
  - `this.traverse`
### `simpleTraverse(startingNode: TSESTree.Node, options: SimpleTraverseOptions, setParentPointers: boolean): void`

<details><summary>Code</summary>

```ts
export function simpleTraverse(
  startingNode: TSESTree.Node,
  options: SimpleTraverseOptions,
  setParentPointers = false,
): void {
  new SimpleTraverser(options, setParentPointers).traverse(
    startingNode,
    undefined,
  );
}
```
</details>

- **Parameters**:
  - `startingNode: TSESTree.Node`
  - `options: SimpleTraverseOptions`
  - `setParentPointers: boolean`
- **Return Type**: `void`
- **Calls**:
  - `new SimpleTraverser(options, setParentPointers).traverse`

---

## Classes

### `SimpleTraverser`

<details><summary>Class Code</summary>

```ts
class SimpleTraverser {
  private readonly allVisitorKeys: Readonly<VisitorKeys> = visitorKeys;
  private readonly selectors: SimpleTraverseOptions;
  private readonly setParentPointers: boolean;

  constructor(selectors: SimpleTraverseOptions, setParentPointers = false) {
    this.selectors = selectors;
    this.setParentPointers = setParentPointers;
    if (selectors.visitorKeys) {
      this.allVisitorKeys = selectors.visitorKeys;
    }
  }

  traverse(node: unknown, parent: TSESTree.Node | undefined): void {
    if (!isValidNode(node)) {
      return;
    }

    if (this.setParentPointers) {
      node.parent = parent;
    }

    if ('enter' in this.selectors) {
      this.selectors.enter(node, parent);
    } else if (node.type in this.selectors.visitors) {
      this.selectors.visitors[node.type](node, parent);
    }

    const keys = getVisitorKeysForNode(this.allVisitorKeys, node);
    if (keys.length < 1) {
      return;
    }

    for (const key of keys) {
      const childOrChildren = node[key];

      if (Array.isArray(childOrChildren)) {
        for (const child of childOrChildren) {
          this.traverse(child, node);
        }
      } else {
        this.traverse(childOrChildren, node);
      }
    }
  }
}
```
</details>

#### Methods

##### `traverse(node: unknown, parent: TSESTree.Node | undefined): void`

<details><summary>Code</summary>

```ts
traverse(node: unknown, parent: TSESTree.Node | undefined): void {
    if (!isValidNode(node)) {
      return;
    }

    if (this.setParentPointers) {
      node.parent = parent;
    }

    if ('enter' in this.selectors) {
      this.selectors.enter(node, parent);
    } else if (node.type in this.selectors.visitors) {
      this.selectors.visitors[node.type](node, parent);
    }

    const keys = getVisitorKeysForNode(this.allVisitorKeys, node);
    if (keys.length < 1) {
      return;
    }

    for (const key of keys) {
      const childOrChildren = node[key];

      if (Array.isArray(childOrChildren)) {
        for (const child of childOrChildren) {
          this.traverse(child, node);
        }
      } else {
        this.traverse(childOrChildren, node);
      }
    }
  }
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `SimpleTraverseOptions`

```ts
type SimpleTraverseOptions = Readonly<
  | {
      enter: (node: TSESTree.Node, parent: TSESTree.Node | undefined) => void;
      visitorKeys?: Readonly<VisitorKeys>;
    }
  | {
      visitorKeys?: Readonly<VisitorKeys>;
      visitors: Record<
        string,
        (node: TSESTree.Node, parent: TSESTree.Node | undefined) => void
      >;
    }
>;
```


---