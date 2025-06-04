[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `types.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📐 Interfaces | 7 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/rule-schema-to-typescript-types/src/types.ts`**

## Interfaces

### `BaseASTNode`

<details><summary>Interface Code</summary>

```ts
interface BaseASTNode {
  readonly commentLines: string[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `commentLines` | `string[]` | ✗ |  |

### `ArrayAST`

<details><summary>Interface Code</summary>

```ts
export interface ArrayAST extends BaseASTNode {
  readonly elementType: AST;
  readonly type: 'array';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `elementType` | `AST` | ✗ |  |
| `type` | `'array'` | ✗ |  |

### `LiteralAST`

<details><summary>Interface Code</summary>

```ts
export interface LiteralAST extends BaseASTNode {
  readonly code: string;
  readonly type: 'literal';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `code` | `string` | ✗ |  |
| `type` | `'literal'` | ✗ |  |

### `ObjectAST`

<details><summary>Interface Code</summary>

```ts
export interface ObjectAST extends BaseASTNode {
  readonly indexSignature: AST | null;
  readonly properties: {
    readonly name: string;
    readonly optional: boolean;
    readonly type: AST;
  }[];
  readonly type: 'object';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `indexSignature` | `AST | null` | ✗ |  |
| `properties` | `{
    readonly name: string;
    readonly optional: boolean;
    readonly type: AST;
  }[]` | ✗ |  |
| `type` | `'object'` | ✗ |  |

### `TupleAST`

<details><summary>Interface Code</summary>

```ts
export interface TupleAST extends BaseASTNode {
  readonly elements: AST[];
  readonly spreadType: AST | null;
  readonly type: 'tuple';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `elements` | `AST[]` | ✗ |  |
| `spreadType` | `AST | null` | ✗ |  |
| `type` | `'tuple'` | ✗ |  |

### `TypeReferenceAST`

<details><summary>Interface Code</summary>

```ts
export interface TypeReferenceAST extends BaseASTNode {
  readonly type: 'type-reference';
  readonly typeName: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `'type-reference'` | ✗ |  |
| `typeName` | `string` | ✗ |  |

### `UnionAST`

<details><summary>Interface Code</summary>

```ts
export interface UnionAST extends BaseASTNode {
  readonly elements: AST[];
  readonly type: 'union';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `elements` | `AST[]` | ✗ |  |
| `type` | `'union'` | ✗ |  |


---

## Type Aliases

### `RefMap`

```ts
type RefMap = ReadonlyMap<
  // ref path
  string,
  // type name
  string
>;
```

### `AST`

```ts
type AST = | ArrayAST
  | LiteralAST
  | ObjectAST
  | TupleAST
  | TypeReferenceAST
  | UnionAST;
```


---