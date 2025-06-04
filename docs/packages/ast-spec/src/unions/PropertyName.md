[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `PropertyName.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📑 Type Aliases | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/PropertyName.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Identifier` | `../expression/Identifier/spec` |
| `NumberLiteral` | `../expression/literal/NumberLiteral/spec` |
| `StringLiteral` | `../expression/literal/StringLiteral/spec` |
| `PrivateIdentifier` | `../special/PrivateIdentifier/spec` |
| `Expression` | `../unions/Expression` |


---

## Type Aliases

### `PropertyName`

```ts
type PropertyName = | ClassPropertyNameNonComputed
  | PropertyNameComputed
  | PropertyNameNonComputed;
```

### `PropertyNameComputed`

```ts
type PropertyNameComputed = Expression;
```

### `PropertyNameNonComputed`

```ts
type PropertyNameNonComputed = | Identifier
  | NumberLiteral
  | StringLiteral;
```

### `ClassPropertyNameNonComputed`

```ts
type ClassPropertyNameNonComputed = | PrivateIdentifier
  // only class properties can have private identifiers as their names
  | PropertyNameNonComputed;
```


---