[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `PropertyDefinitionBase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 9 |
| 📐 Interfaces | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/PropertyDefinitionBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Decorator` | `../special/Decorator/spec` |
| `TSTypeAnnotation` | `../special/TSTypeAnnotation/spec` |
| `Expression` | `../unions/Expression` |
| `ClassPropertyNameNonComputed` | `../unions/PropertyName` |
| `PropertyName` | `../unions/PropertyName` |
| `PropertyNameComputed` | `../unions/PropertyName` |
| `PropertyNameNonComputed` | `../unions/PropertyName` |
| `Accessibility` | `./Accessibility` |
| `BaseNode` | `./BaseNode` |


---

## Interfaces

### `PropertyDefinitionBase`

<details><summary>Interface Code</summary>

```ts
interface PropertyDefinitionBase extends BaseNode {
  accessibility: Accessibility | undefined;
  computed: boolean;
  declare: boolean;
  decorators: Decorator[];
  definite: boolean;
  key: PropertyName;
  optional: boolean;
  override: boolean;
  readonly: boolean;
  static: boolean;
  typeAnnotation: TSTypeAnnotation | undefined;
  value: Expression | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `accessibility` | `Accessibility | undefined` | ✗ |  |
| `computed` | `boolean` | ✗ |  |
| `declare` | `boolean` | ✗ |  |
| `decorators` | `Decorator[]` | ✗ |  |
| `definite` | `boolean` | ✗ |  |
| `key` | `PropertyName` | ✗ |  |
| `optional` | `boolean` | ✗ |  |
| `override` | `boolean` | ✗ |  |
| `readonly` | `boolean` | ✗ |  |
| `static` | `boolean` | ✗ |  |
| `typeAnnotation` | `TSTypeAnnotation | undefined` | ✗ |  |
| `value` | `Expression | null` | ✗ |  |

### `PropertyDefinitionComputedNameBase`

<details><summary>Interface Code</summary>

```ts
export interface PropertyDefinitionComputedNameBase
  extends PropertyDefinitionBase {
  computed: true;
  key: PropertyNameComputed;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `computed` | `true` | ✗ |  |
| `key` | `PropertyNameComputed` | ✗ |  |

### `PropertyDefinitionNonComputedNameBase`

<details><summary>Interface Code</summary>

```ts
export interface PropertyDefinitionNonComputedNameBase
  extends PropertyDefinitionBase {
  computed: false;
  key: PropertyNameNonComputed;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `computed` | `false` | ✗ |  |
| `key` | `PropertyNameNonComputed` | ✗ |  |

### `ClassPropertyDefinitionNonComputedNameBase`

<details><summary>Interface Code</summary>

```ts
export interface ClassPropertyDefinitionNonComputedNameBase
  extends PropertyDefinitionBase {
  computed: false;
  key: ClassPropertyNameNonComputed;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `computed` | `false` | ✗ |  |
| `key` | `ClassPropertyNameNonComputed` | ✗ |  |


---