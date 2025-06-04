[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Visitor.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 1 |
| 🔄 Re-exports | 1 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Re-exports](#re-exports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `visitor` | `PatternVisitor` | const | `new PatternVisitor(this.#options, node, callback)` | ✗ |


---

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| named | `./VisitorBase` | VisitorBase, VisitorOptions |


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