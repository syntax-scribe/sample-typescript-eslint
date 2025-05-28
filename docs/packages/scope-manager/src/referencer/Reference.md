[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Reference.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 5 |
| 🧱 Classes | 1 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)
- [Enums](#enums)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/referencer/Reference.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `Scope` | `../scope` |
| `Variable` | `../variable` |
| `createIdGenerator` | `../ID` |


---

## Functions

### `Reference.isWrite(): boolean`

<details><summary>Code</summary>

```ts
public isWrite(): boolean {
    return !!(this.#flag & ReferenceFlag.Write);
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Whether the reference is writeable.
   * @public
   */
```

- **Return Type**: `boolean`
### `Reference.isRead(): boolean`

<details><summary>Code</summary>

```ts
public isRead(): boolean {
    return !!(this.#flag & ReferenceFlag.Read);
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Whether the reference is readable.
   * @public
   */
```

- **Return Type**: `boolean`
### `Reference.isReadOnly(): boolean`

<details><summary>Code</summary>

```ts
public isReadOnly(): boolean {
    return this.#flag === ReferenceFlag.Read;
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Whether the reference is read-only.
   * @public
   */
```

- **Return Type**: `boolean`
### `Reference.isWriteOnly(): boolean`

<details><summary>Code</summary>

```ts
public isWriteOnly(): boolean {
    return this.#flag === ReferenceFlag.Write;
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Whether the reference is write-only.
   * @public
   */
```

- **Return Type**: `boolean`
### `Reference.isReadWrite(): boolean`

<details><summary>Code</summary>

```ts
public isReadWrite(): boolean {
    return this.#flag === ReferenceFlag.ReadWrite;
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Whether the reference is read-write.
   * @public
   */
```

- **Return Type**: `boolean`

---

## Classes

### `Reference`

<details><summary>Class Code</summary>

```ts
export class Reference {
  /**
   * A unique ID for this instance - primarily used to help debugging and testing
   */
  public readonly $id: number = generator();

  /**
   * The read-write mode of the reference.
   */
  readonly #flag: ReferenceFlag;

  /**
   * Reference to the enclosing Scope.
   * @public
   */
  public readonly from: Scope;

  /**
   * Identifier syntax node.
   * @public
   */
  public readonly identifier: TSESTree.Identifier | TSESTree.JSXIdentifier;

  /**
   * `true` if this writing reference is a variable initializer or a default value.
   * @public
   */
  public readonly init?: boolean;

  public readonly maybeImplicitGlobal?: ReferenceImplicitGlobal | null;

  /**
   * The {@link Variable} object that this reference refers to. If such variable was not defined, this is `null`.
   * @public
   */
  public resolved: Variable | null;

  /**
   * If reference is writeable, this is the node being written to it.
   * @public
   */
  public readonly writeExpr?: TSESTree.Node | null;

  /**
   * In some cases, a reference may be a type, value or both a type and value reference.
   */
  readonly #referenceType: ReferenceTypeFlag;

  constructor(
    identifier: TSESTree.Identifier | TSESTree.JSXIdentifier,
    scope: Scope,
    flag: ReferenceFlag,
    writeExpr?: TSESTree.Node | null,
    maybeImplicitGlobal?: ReferenceImplicitGlobal | null,
    init?: boolean,
    referenceType = ReferenceTypeFlag.Value,
  ) {
    this.identifier = identifier;
    this.from = scope;
    this.resolved = null;
    this.#flag = flag;

    if (this.isWrite()) {
      this.writeExpr = writeExpr;
      this.init = init;
    }

    this.maybeImplicitGlobal = maybeImplicitGlobal;
    this.#referenceType = referenceType;
  }

  /**
   * True if this reference can reference types
   */
  public get isTypeReference(): boolean {
    return (this.#referenceType & ReferenceTypeFlag.Type) !== 0;
  }

  /**
   * True if this reference can reference values
   */
  public get isValueReference(): boolean {
    return (this.#referenceType & ReferenceTypeFlag.Value) !== 0;
  }

  /**
   * Whether the reference is writeable.
   * @public
   */
  public isWrite(): boolean {
    return !!(this.#flag & ReferenceFlag.Write);
  }

  /**
   * Whether the reference is readable.
   * @public
   */
  public isRead(): boolean {
    return !!(this.#flag & ReferenceFlag.Read);
  }

  /**
   * Whether the reference is read-only.
   * @public
   */
  public isReadOnly(): boolean {
    return this.#flag === ReferenceFlag.Read;
  }

  /**
   * Whether the reference is write-only.
   * @public
   */
  public isWriteOnly(): boolean {
    return this.#flag === ReferenceFlag.Write;
  }

  /**
   * Whether the reference is read-write.
   * @public
   */
  public isReadWrite(): boolean {
    return this.#flag === ReferenceFlag.ReadWrite;
  }
}
```
</details>

#### Methods

##### `isWrite(): boolean`

<details><summary>Code</summary>

```ts
public isWrite(): boolean {
    return !!(this.#flag & ReferenceFlag.Write);
  }
```
</details>

##### `isRead(): boolean`

<details><summary>Code</summary>

```ts
public isRead(): boolean {
    return !!(this.#flag & ReferenceFlag.Read);
  }
```
</details>

##### `isReadOnly(): boolean`

<details><summary>Code</summary>

```ts
public isReadOnly(): boolean {
    return this.#flag === ReferenceFlag.Read;
  }
```
</details>

##### `isWriteOnly(): boolean`

<details><summary>Code</summary>

```ts
public isWriteOnly(): boolean {
    return this.#flag === ReferenceFlag.Write;
  }
```
</details>

##### `isReadWrite(): boolean`

<details><summary>Code</summary>

```ts
public isReadWrite(): boolean {
    return this.#flag === ReferenceFlag.ReadWrite;
  }
```
</details>


---

## Interfaces

### `ReferenceImplicitGlobal`

<details><summary>Interface Code</summary>

```ts
export interface ReferenceImplicitGlobal {
  node: TSESTree.Node;
  pattern: TSESTree.BindingName;
  ref?: Reference;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `node` | `TSESTree.Node` | ✗ |  |
| `pattern` | `TSESTree.BindingName` | ✗ |  |
| `ref` | `Reference` | ✓ |  |


---

## Enums

### `enum ReferenceFlag`

<details><summary>Enum Code</summary>

```ts
export enum ReferenceFlag {
  Read = 0x1,
  Write = 0x2,
  ReadWrite = 0x3,
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `Read` | `1` |  |
| `Write` | `2` |  |
| `ReadWrite` | `3` |  |

### `enum ReferenceTypeFlag`

<details><summary>Enum Code</summary>

```ts
export enum ReferenceTypeFlag {
  Value = 0x1,
  Type = 0x2,
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `Value` | `1` |  |
| `Type` | `2` |  |


---