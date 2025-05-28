[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `PatternVisitor.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 13 |
| 🧱 Classes | 1 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Classes](#classes)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/referencer/PatternVisitor.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `VisitorOptions` | `./VisitorBase` |
| `VisitorBase` | `./VisitorBase` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `nodeType` | `any` | const | `node.type` | ✗ |


---

## Functions

### `PatternVisitor.isPattern(node: TSESTree.Node): node is
    | TSESTree.ArrayPattern
    | TSESTree.AssignmentPattern
    | TSESTree.Identifier
    | TSESTree.ObjectPattern
    | TSESTree.RestElement
    | TSESTree.SpreadElement`

<details><summary>Code</summary>

```ts
public static isPattern(
    node: TSESTree.Node,
  ): node is
    | TSESTree.ArrayPattern
    | TSESTree.AssignmentPattern
    | TSESTree.Identifier
    | TSESTree.ObjectPattern
    | TSESTree.RestElement
    | TSESTree.SpreadElement {
    const nodeType = node.type;

    return (
      nodeType === AST_NODE_TYPES.Identifier ||
      nodeType === AST_NODE_TYPES.ObjectPattern ||
      nodeType === AST_NODE_TYPES.ArrayPattern ||
      nodeType === AST_NODE_TYPES.SpreadElement ||
      nodeType === AST_NODE_TYPES.RestElement ||
      nodeType === AST_NODE_TYPES.AssignmentPattern
    );
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is
    | TSESTree.ArrayPattern
    | TSESTree.AssignmentPattern
    | TSESTree.Identifier
    | TSESTree.ObjectPattern
    | TSESTree.RestElement
    | TSESTree.SpreadElement`
### `PatternVisitor.ArrayExpression(node: TSESTree.ArrayExpression): void`

<details><summary>Code</summary>

```ts
protected ArrayExpression(node: TSESTree.ArrayExpression): void {
    node.elements.forEach(this.visit, this);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ArrayExpression`
- **Return Type**: `void`
- **Calls**:
  - `node.elements.forEach`
### `PatternVisitor.ArrayPattern(pattern: TSESTree.ArrayPattern): void`

<details><summary>Code</summary>

```ts
protected ArrayPattern(pattern: TSESTree.ArrayPattern): void {
    for (const element of pattern.elements) {
      this.visit(element);
    }
  }
```
</details>

- **Parameters**:
  - `pattern: TSESTree.ArrayPattern`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
### `PatternVisitor.AssignmentExpression(node: TSESTree.AssignmentExpression): void`

<details><summary>Code</summary>

```ts
protected AssignmentExpression(node: TSESTree.AssignmentExpression): void {
    this.#assignments.push(node);
    this.visit(node.left);
    this.rightHandNodes.push(node.right);
    this.#assignments.pop();
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.AssignmentExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.#assignments.push`
  - `this.visit`
  - `this.rightHandNodes.push`
  - `this.#assignments.pop`
### `PatternVisitor.AssignmentPattern(pattern: TSESTree.AssignmentPattern): void`

<details><summary>Code</summary>

```ts
protected AssignmentPattern(pattern: TSESTree.AssignmentPattern): void {
    this.#assignments.push(pattern);
    this.visit(pattern.left);
    this.rightHandNodes.push(pattern.right);
    this.#assignments.pop();
  }
```
</details>

- **Parameters**:
  - `pattern: TSESTree.AssignmentPattern`
- **Return Type**: `void`
- **Calls**:
  - `this.#assignments.push`
  - `this.visit`
  - `this.rightHandNodes.push`
  - `this.#assignments.pop`
### `PatternVisitor.CallExpression(node: TSESTree.CallExpression): void`

<details><summary>Code</summary>

```ts
protected CallExpression(node: TSESTree.CallExpression): void {
    // arguments are right hand nodes.
    node.arguments.forEach(a => {
      this.rightHandNodes.push(a);
    });
    this.visit(node.callee);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression`
- **Return Type**: `void`
- **Calls**:
  - `node.arguments.forEach`
  - `this.rightHandNodes.push`
  - `this.visit`
- **Internal Comments**:
```
// arguments are right hand nodes. (x5)
```

### `PatternVisitor.Decorator(): void`

<details><summary>Code</summary>

```ts
protected Decorator(): void {
    // don't visit any decorators when exploring a pattern
  }
```
</details>

- **Return Type**: `void`
### `PatternVisitor.Identifier(pattern: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
protected Identifier(pattern: TSESTree.Identifier): void {
    const lastRestElement = this.#restElements.at(-1);

    this.#callback(pattern, {
      assignments: this.#assignments,
      rest: lastRestElement?.argument === pattern,
      topLevel: pattern === this.#rootPattern,
    });
  }
```
</details>

- **Parameters**:
  - `pattern: TSESTree.Identifier`
- **Return Type**: `void`
- **Calls**:
  - `this.#restElements.at`
  - `this.#callback`
### `PatternVisitor.MemberExpression(node: TSESTree.MemberExpression): void`

<details><summary>Code</summary>

```ts
protected MemberExpression(node: TSESTree.MemberExpression): void {
    // Computed property's key is a right hand node.
    if (node.computed) {
      this.rightHandNodes.push(node.property);
    }

    // the object is only read, write to its property.
    this.rightHandNodes.push(node.object);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.MemberExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.rightHandNodes.push`
- **Internal Comments**:
```
// Computed property's key is a right hand node.
// the object is only read, write to its property. (x5)
```

### `PatternVisitor.Property(property: TSESTree.Property): void`

<details><summary>Code</summary>

```ts
protected Property(property: TSESTree.Property): void {
    // Computed property's key is a right hand node.
    if (property.computed) {
      this.rightHandNodes.push(property.key);
    }

    // If it's shorthand, its key is same as its value.
    // If it's shorthand and has its default value, its key is same as its value.left (the value is AssignmentPattern).
    // If it's not shorthand, the name of new variable is its value's.
    this.visit(property.value);
  }
```
</details>

- **Parameters**:
  - `property: TSESTree.Property`
- **Return Type**: `void`
- **Calls**:
  - `this.rightHandNodes.push`
  - `this.visit`
- **Internal Comments**:
```
// Computed property's key is a right hand node.
// If it's shorthand, its key is same as its value. (x4)
// If it's shorthand and has its default value, its key is same as its value.left (the value is AssignmentPattern). (x4)
// If it's not shorthand, the name of new variable is its value's. (x4)
```

### `PatternVisitor.RestElement(pattern: TSESTree.RestElement): void`

<details><summary>Code</summary>

```ts
protected RestElement(pattern: TSESTree.RestElement): void {
    this.#restElements.push(pattern);
    this.visit(pattern.argument);
    this.#restElements.pop();
  }
```
</details>

- **Parameters**:
  - `pattern: TSESTree.RestElement`
- **Return Type**: `void`
- **Calls**:
  - `this.#restElements.push`
  - `this.visit`
  - `this.#restElements.pop`
### `PatternVisitor.SpreadElement(node: TSESTree.SpreadElement): void`

<details><summary>Code</summary>

```ts
protected SpreadElement(node: TSESTree.SpreadElement): void {
    this.visit(node.argument);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.SpreadElement`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
### `PatternVisitor.TSTypeAnnotation(): void`

<details><summary>Code</summary>

```ts
protected TSTypeAnnotation(): void {
    // we don't want to visit types
  }
```
</details>

- **Return Type**: `void`

---

## Classes

### `PatternVisitor`

<details><summary>Class Code</summary>

```ts
export class PatternVisitor extends VisitorBase {
  readonly #assignments: (
    | TSESTree.AssignmentExpression
    | TSESTree.AssignmentPattern
  )[] = [];
  readonly #callback: PatternVisitorCallback;
  readonly #restElements: TSESTree.RestElement[] = [];
  readonly #rootPattern: TSESTree.Node;

  public readonly rightHandNodes: TSESTree.Node[] = [];

  constructor(
    options: PatternVisitorOptions,
    rootPattern: TSESTree.Node,
    callback: PatternVisitorCallback,
  ) {
    super(options);
    this.#rootPattern = rootPattern;
    this.#callback = callback;
  }

  public static isPattern(
    node: TSESTree.Node,
  ): node is
    | TSESTree.ArrayPattern
    | TSESTree.AssignmentPattern
    | TSESTree.Identifier
    | TSESTree.ObjectPattern
    | TSESTree.RestElement
    | TSESTree.SpreadElement {
    const nodeType = node.type;

    return (
      nodeType === AST_NODE_TYPES.Identifier ||
      nodeType === AST_NODE_TYPES.ObjectPattern ||
      nodeType === AST_NODE_TYPES.ArrayPattern ||
      nodeType === AST_NODE_TYPES.SpreadElement ||
      nodeType === AST_NODE_TYPES.RestElement ||
      nodeType === AST_NODE_TYPES.AssignmentPattern
    );
  }

  protected ArrayExpression(node: TSESTree.ArrayExpression): void {
    node.elements.forEach(this.visit, this);
  }

  protected ArrayPattern(pattern: TSESTree.ArrayPattern): void {
    for (const element of pattern.elements) {
      this.visit(element);
    }
  }

  protected AssignmentExpression(node: TSESTree.AssignmentExpression): void {
    this.#assignments.push(node);
    this.visit(node.left);
    this.rightHandNodes.push(node.right);
    this.#assignments.pop();
  }

  protected AssignmentPattern(pattern: TSESTree.AssignmentPattern): void {
    this.#assignments.push(pattern);
    this.visit(pattern.left);
    this.rightHandNodes.push(pattern.right);
    this.#assignments.pop();
  }

  protected CallExpression(node: TSESTree.CallExpression): void {
    // arguments are right hand nodes.
    node.arguments.forEach(a => {
      this.rightHandNodes.push(a);
    });
    this.visit(node.callee);
  }

  protected Decorator(): void {
    // don't visit any decorators when exploring a pattern
  }

  protected Identifier(pattern: TSESTree.Identifier): void {
    const lastRestElement = this.#restElements.at(-1);

    this.#callback(pattern, {
      assignments: this.#assignments,
      rest: lastRestElement?.argument === pattern,
      topLevel: pattern === this.#rootPattern,
    });
  }

  protected MemberExpression(node: TSESTree.MemberExpression): void {
    // Computed property's key is a right hand node.
    if (node.computed) {
      this.rightHandNodes.push(node.property);
    }

    // the object is only read, write to its property.
    this.rightHandNodes.push(node.object);
  }

  protected Property(property: TSESTree.Property): void {
    // Computed property's key is a right hand node.
    if (property.computed) {
      this.rightHandNodes.push(property.key);
    }

    // If it's shorthand, its key is same as its value.
    // If it's shorthand and has its default value, its key is same as its value.left (the value is AssignmentPattern).
    // If it's not shorthand, the name of new variable is its value's.
    this.visit(property.value);
  }

  protected RestElement(pattern: TSESTree.RestElement): void {
    this.#restElements.push(pattern);
    this.visit(pattern.argument);
    this.#restElements.pop();
  }

  protected SpreadElement(node: TSESTree.SpreadElement): void {
    this.visit(node.argument);
  }

  protected TSTypeAnnotation(): void {
    // we don't want to visit types
  }
}
```
</details>

#### Methods

##### `isPattern(node: TSESTree.Node): node is
    | TSESTree.ArrayPattern
    | TSESTree.AssignmentPattern
    | TSESTree.Identifier
    | TSESTree.ObjectPattern
    | TSESTree.RestElement
    | TSESTree.SpreadElement`

<details><summary>Code</summary>

```ts
public static isPattern(
    node: TSESTree.Node,
  ): node is
    | TSESTree.ArrayPattern
    | TSESTree.AssignmentPattern
    | TSESTree.Identifier
    | TSESTree.ObjectPattern
    | TSESTree.RestElement
    | TSESTree.SpreadElement {
    const nodeType = node.type;

    return (
      nodeType === AST_NODE_TYPES.Identifier ||
      nodeType === AST_NODE_TYPES.ObjectPattern ||
      nodeType === AST_NODE_TYPES.ArrayPattern ||
      nodeType === AST_NODE_TYPES.SpreadElement ||
      nodeType === AST_NODE_TYPES.RestElement ||
      nodeType === AST_NODE_TYPES.AssignmentPattern
    );
  }
```
</details>

##### `ArrayExpression(node: TSESTree.ArrayExpression): void`

<details><summary>Code</summary>

```ts
protected ArrayExpression(node: TSESTree.ArrayExpression): void {
    node.elements.forEach(this.visit, this);
  }
```
</details>

##### `ArrayPattern(pattern: TSESTree.ArrayPattern): void`

<details><summary>Code</summary>

```ts
protected ArrayPattern(pattern: TSESTree.ArrayPattern): void {
    for (const element of pattern.elements) {
      this.visit(element);
    }
  }
```
</details>

##### `AssignmentExpression(node: TSESTree.AssignmentExpression): void`

<details><summary>Code</summary>

```ts
protected AssignmentExpression(node: TSESTree.AssignmentExpression): void {
    this.#assignments.push(node);
    this.visit(node.left);
    this.rightHandNodes.push(node.right);
    this.#assignments.pop();
  }
```
</details>

##### `AssignmentPattern(pattern: TSESTree.AssignmentPattern): void`

<details><summary>Code</summary>

```ts
protected AssignmentPattern(pattern: TSESTree.AssignmentPattern): void {
    this.#assignments.push(pattern);
    this.visit(pattern.left);
    this.rightHandNodes.push(pattern.right);
    this.#assignments.pop();
  }
```
</details>

##### `CallExpression(node: TSESTree.CallExpression): void`

<details><summary>Code</summary>

```ts
protected CallExpression(node: TSESTree.CallExpression): void {
    // arguments are right hand nodes.
    node.arguments.forEach(a => {
      this.rightHandNodes.push(a);
    });
    this.visit(node.callee);
  }
```
</details>

##### `Decorator(): void`

<details><summary>Code</summary>

```ts
protected Decorator(): void {
    // don't visit any decorators when exploring a pattern
  }
```
</details>

##### `Identifier(pattern: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
protected Identifier(pattern: TSESTree.Identifier): void {
    const lastRestElement = this.#restElements.at(-1);

    this.#callback(pattern, {
      assignments: this.#assignments,
      rest: lastRestElement?.argument === pattern,
      topLevel: pattern === this.#rootPattern,
    });
  }
```
</details>

##### `MemberExpression(node: TSESTree.MemberExpression): void`

<details><summary>Code</summary>

```ts
protected MemberExpression(node: TSESTree.MemberExpression): void {
    // Computed property's key is a right hand node.
    if (node.computed) {
      this.rightHandNodes.push(node.property);
    }

    // the object is only read, write to its property.
    this.rightHandNodes.push(node.object);
  }
```
</details>

##### `Property(property: TSESTree.Property): void`

<details><summary>Code</summary>

```ts
protected Property(property: TSESTree.Property): void {
    // Computed property's key is a right hand node.
    if (property.computed) {
      this.rightHandNodes.push(property.key);
    }

    // If it's shorthand, its key is same as its value.
    // If it's shorthand and has its default value, its key is same as its value.left (the value is AssignmentPattern).
    // If it's not shorthand, the name of new variable is its value's.
    this.visit(property.value);
  }
```
</details>

##### `RestElement(pattern: TSESTree.RestElement): void`

<details><summary>Code</summary>

```ts
protected RestElement(pattern: TSESTree.RestElement): void {
    this.#restElements.push(pattern);
    this.visit(pattern.argument);
    this.#restElements.pop();
  }
```
</details>

##### `SpreadElement(node: TSESTree.SpreadElement): void`

<details><summary>Code</summary>

```ts
protected SpreadElement(node: TSESTree.SpreadElement): void {
    this.visit(node.argument);
  }
```
</details>

##### `TSTypeAnnotation(): void`

<details><summary>Code</summary>

```ts
protected TSTypeAnnotation(): void {
    // we don't want to visit types
  }
```
</details>


---

## Type Aliases

### `PatternVisitorCallback`

```ts
type PatternVisitorCallback = (
  pattern: TSESTree.Identifier,
  info: {
    assignments: (TSESTree.AssignmentExpression | TSESTree.AssignmentPattern)[];
    rest: boolean;
    topLevel: boolean;
  },
) => void;
```

### `PatternVisitorOptions`

```ts
type PatternVisitorOptions = VisitorOptions;
```


---