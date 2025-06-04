[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `MethodDefinitionBase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 9 |
| 📐 Interfaces | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/MethodDefinitionBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `FunctionExpression` | `../expression/FunctionExpression/spec` |
| `TSEmptyBodyFunctionExpression` | `../expression/TSEmptyBodyFunctionExpression/spec` |
| `Decorator` | `../special/Decorator/spec` |
| `ClassPropertyNameNonComputed` | `../unions/PropertyName` |
| `PropertyName` | `../unions/PropertyName` |
| `PropertyNameComputed` | `../unions/PropertyName` |
| `PropertyNameNonComputed` | `../unions/PropertyName` |
| `Accessibility` | `./Accessibility` |
| `BaseNode` | `./BaseNode` |


---

## Interfaces

### `MethodDefinitionBase`

<details><summary>Interface Code</summary>

```ts
interface MethodDefinitionBase extends BaseNode {
  accessibility: Accessibility | undefined;
  computed: boolean;
  decorators: Decorator[];
  key: PropertyName;
  kind: 'constructor' | 'get' | 'method' | 'set';
  optional: boolean;
  override: boolean;
  static: boolean;
  value: FunctionExpression | TSEmptyBodyFunctionExpression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `accessibility` | `Accessibility | undefined` | ✗ |  |
| `computed` | `boolean` | ✗ |  |
| `decorators` | `Decorator[]` | ✗ |  |
| `key` | `PropertyName` | ✗ |  |
| `kind` | `'constructor' | 'get' | 'method' | 'set'` | ✗ |  |
| `optional` | `boolean` | ✗ |  |
| `override` | `boolean` | ✗ |  |
| `static` | `boolean` | ✗ |  |
| `value` | `FunctionExpression | TSEmptyBodyFunctionExpression` | ✗ |  |

### `MethodDefinitionComputedNameBase`

<details><summary>Interface Code</summary>

```ts
export interface MethodDefinitionComputedNameBase extends MethodDefinitionBase {
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

### `MethodDefinitionNonComputedNameBase`

<details><summary>Interface Code</summary>

```ts
export interface MethodDefinitionNonComputedNameBase
  extends MethodDefinitionBase {
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

### `ClassMethodDefinitionNonComputedNameBase`

<details><summary>Interface Code</summary>

```ts
export interface ClassMethodDefinitionNonComputedNameBase
  extends MethodDefinitionBase {
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