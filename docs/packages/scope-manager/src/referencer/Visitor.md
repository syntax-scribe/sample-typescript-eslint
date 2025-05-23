[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Visitor.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 1
- **Imports**: 6
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/referencer/Visitor.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `PatternVisitorCallback` | `./PatternVisitor` |
| `PatternVisitorOptions` | `./PatternVisitor` |
| `VisitorOptions` | `./VisitorBase` |
| `PatternVisitor` | `./PatternVisitor` |
| `VisitorBase` | `./VisitorBase` |


---

## Functions

### `Visitor.visitPattern(node: TSESTree.Node, callback: PatternVisitorCallback, options: VisitPatternOptions): void`

<details><summary>Code</summary>

```ts
protected visitPattern(
    node: TSESTree.Node,
    callback: PatternVisitorCallback,
    options: VisitPatternOptions = { processRightHandNodes: false },
  ): void {
    // Call the callback at left hand identifier nodes, and Collect right hand nodes.
    const visitor = new PatternVisitor(this.#options, node, callback);

    visitor.visit(node);

    // Process the right hand nodes recursively.
    if (options.processRightHandNodes) {
      visitor.rightHandNodes.forEach(this.visit, this);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `callback: PatternVisitorCallback`
  - `options: VisitPatternOptions`
- **Return Type**: `void`
- **Calls**:
  - `visitor.visit`
  - `visitor.rightHandNodes.forEach`
- **Internal Comments**:
```
// Call the callback at left hand identifier nodes, and Collect right hand nodes. (x2)
// Process the right hand nodes recursively.
```


---

## Classes

### `Visitor`

<details><summary>Class Code</summary>

```ts
export class Visitor extends VisitorBase {
  readonly #options: VisitorOptions;
  constructor(optionsOrVisitor: Visitor | VisitorOptions) {
    super(
      optionsOrVisitor instanceof Visitor
        ? optionsOrVisitor.#options
        : optionsOrVisitor,
    );

    this.#options =
      optionsOrVisitor instanceof Visitor
        ? optionsOrVisitor.#options
        : optionsOrVisitor;
  }

  protected visitPattern(
    node: TSESTree.Node,
    callback: PatternVisitorCallback,
    options: VisitPatternOptions = { processRightHandNodes: false },
  ): void {
    // Call the callback at left hand identifier nodes, and Collect right hand nodes.
    const visitor = new PatternVisitor(this.#options, node, callback);

    visitor.visit(node);

    // Process the right hand nodes recursively.
    if (options.processRightHandNodes) {
      visitor.rightHandNodes.forEach(this.visit, this);
    }
  }
}
```
</details>

#### Methods

##### `visitPattern(node: TSESTree.Node, callback: PatternVisitorCallback, options: VisitPatternOptions): void`

<details><summary>Code</summary>

```ts
protected visitPattern(
    node: TSESTree.Node,
    callback: PatternVisitorCallback,
    options: VisitPatternOptions = { processRightHandNodes: false },
  ): void {
    // Call the callback at left hand identifier nodes, and Collect right hand nodes.
    const visitor = new PatternVisitor(this.#options, node, callback);

    visitor.visit(node);

    // Process the right hand nodes recursively.
    if (options.processRightHandNodes) {
      visitor.rightHandNodes.forEach(this.visit, this);
    }
  }
```
</details>


---

## Interfaces

### `VisitPatternOptions`

<details><summary>Interface Code</summary>

```ts
interface VisitPatternOptions extends PatternVisitorOptions {
  processRightHandNodes?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `processRightHandNodes` | `boolean` | ✓ |  |


---

## Type Aliases

> No type aliases found in this file.


---