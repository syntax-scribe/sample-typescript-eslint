[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `ts-estree.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 1 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 61 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Re-exports](#re-exports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/types/src/ts-estree.ts`**

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| namespace | `./generated/ast-spec` | TSESTree |


---


---

## Interfaces

### `BaseNode`

<details><summary>Interface Code</summary>

```ts
interface BaseNode {
    parent: TSESTree.Node;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.Node` | ✗ |  |

### `Program`

<details><summary>Interface Code</summary>

```ts
interface Program {
    /**
     * @remarks This never-used property exists only as a convenience for code that tries to access node parents repeatedly.
     */
    parent?: never;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `never` | ✓ |  |

### `AccessorPropertyComputedName`

<details><summary>Interface Code</summary>

```ts
interface AccessorPropertyComputedName {
    parent: TSESTree.ClassBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassBody` | ✗ |  |

### `AccessorPropertyNonComputedName`

<details><summary>Interface Code</summary>

```ts
interface AccessorPropertyNonComputedName {
    parent: TSESTree.ClassBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassBody` | ✗ |  |

### `TSAbstractAccessorPropertyComputedName`

<details><summary>Interface Code</summary>

```ts
interface TSAbstractAccessorPropertyComputedName {
    parent: TSESTree.ClassBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassBody` | ✗ |  |

### `TSAbstractAccessorPropertyNonComputedName`

<details><summary>Interface Code</summary>

```ts
interface TSAbstractAccessorPropertyNonComputedName {
    parent: TSESTree.ClassBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassBody` | ✗ |  |

### `VariableDeclaratorDefiniteAssignment`

<details><summary>Interface Code</summary>

```ts
interface VariableDeclaratorDefiniteAssignment {
    parent: TSESTree.VariableDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.VariableDeclaration` | ✗ |  |

### `VariableDeclaratorMaybeInit`

<details><summary>Interface Code</summary>

```ts
interface VariableDeclaratorMaybeInit {
    parent: TSESTree.VariableDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.VariableDeclaration` | ✗ |  |

### `VariableDeclaratorNoInit`

<details><summary>Interface Code</summary>

```ts
interface VariableDeclaratorNoInit {
    parent: TSESTree.VariableDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.VariableDeclaration` | ✗ |  |

### `UsingInForOfDeclarator`

<details><summary>Interface Code</summary>

```ts
interface UsingInForOfDeclarator {
    parent: TSESTree.VariableDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.VariableDeclaration` | ✗ |  |

### `UsingInNormalContextDeclarator`

<details><summary>Interface Code</summary>

```ts
interface UsingInNormalContextDeclarator {
    parent: TSESTree.VariableDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.VariableDeclaration` | ✗ |  |

### `CatchClause`

<details><summary>Interface Code</summary>

```ts
interface CatchClause {
    parent: TSESTree.TryStatement;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TryStatement` | ✗ |  |

### `ClassBody`

<details><summary>Interface Code</summary>

```ts
interface ClassBody {
    parent: TSESTree.ClassDeclaration | TSESTree.ClassExpression;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassDeclaration | TSESTree.ClassExpression` | ✗ |  |

### `ImportAttribute`

<details><summary>Interface Code</summary>

```ts
interface ImportAttribute {
    parent:
      | TSESTree.ExportAllDeclaration
      | TSESTree.ExportNamedDeclaration
      | TSESTree.ImportDeclaration
      | TSESTree.TSImportType;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `| TSESTree.ExportAllDeclaration
      | TSESTree.ExportNamedDeclaration
      | TSESTree.ImportDeclaration
      | TSESTree.TSImportType` | ✗ |  |

### `ImportDefaultSpecifier`

<details><summary>Interface Code</summary>

```ts
interface ImportDefaultSpecifier {
    parent: TSESTree.ImportDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ImportDeclaration` | ✗ |  |

### `ImportNamespaceSpecifier`

<details><summary>Interface Code</summary>

```ts
interface ImportNamespaceSpecifier {
    parent: TSESTree.ImportDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ImportDeclaration` | ✗ |  |

### `ImportSpecifier`

<details><summary>Interface Code</summary>

```ts
interface ImportSpecifier {
    parent:
      | TSESTree.ExportAllDeclaration
      | TSESTree.ExportNamedDeclaration
      | TSESTree.ImportDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `| TSESTree.ExportAllDeclaration
      | TSESTree.ExportNamedDeclaration
      | TSESTree.ImportDeclaration` | ✗ |  |

### `ExportDefaultDeclaration`

<details><summary>Interface Code</summary>

```ts
interface ExportDefaultDeclaration {
    parent: TSESTree.BlockStatement | TSESTree.Program | TSESTree.TSModuleBlock;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.BlockStatement | TSESTree.Program | TSESTree.TSModuleBlock` | ✗ |  |

### `ExportNamedDeclarationWithoutSourceWithMultiple`

<details><summary>Interface Code</summary>

```ts
interface ExportNamedDeclarationWithoutSourceWithMultiple {
    parent: TSESTree.BlockStatement | TSESTree.Program | TSESTree.TSModuleBlock;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.BlockStatement | TSESTree.Program | TSESTree.TSModuleBlock` | ✗ |  |

### `ExportNamedDeclarationWithoutSourceWithSingle`

<details><summary>Interface Code</summary>

```ts
interface ExportNamedDeclarationWithoutSourceWithSingle {
    parent: TSESTree.BlockStatement | TSESTree.Program | TSESTree.TSModuleBlock;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.BlockStatement | TSESTree.Program | TSESTree.TSModuleBlock` | ✗ |  |

### `ExportNamedDeclarationWithSource`

<details><summary>Interface Code</summary>

```ts
interface ExportNamedDeclarationWithSource {
    parent: TSESTree.BlockStatement | TSESTree.Program | TSESTree.TSModuleBlock;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.BlockStatement | TSESTree.Program | TSESTree.TSModuleBlock` | ✗ |  |

### `FunctionDeclarationWithName`

<details><summary>Interface Code</summary>

```ts
interface FunctionDeclarationWithName {
    parent:
      | TSESTree.BlockStatement
      | TSESTree.ExportDefaultDeclaration
      | TSESTree.ExportNamedDeclaration
      | TSESTree.Program;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `| TSESTree.BlockStatement
      | TSESTree.ExportDefaultDeclaration
      | TSESTree.ExportNamedDeclaration
      | TSESTree.Program` | ✗ |  |

### `FunctionDeclarationWithOptionalName`

<details><summary>Interface Code</summary>

```ts
interface FunctionDeclarationWithOptionalName {
    parent: TSESTree.ExportDefaultDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ExportDefaultDeclaration` | ✗ |  |

### `JSXAttribute`

<details><summary>Interface Code</summary>

```ts
interface JSXAttribute {
    parent: TSESTree.JSXOpeningElement;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.JSXOpeningElement` | ✗ |  |

### `JSXClosingElement`

<details><summary>Interface Code</summary>

```ts
interface JSXClosingElement {
    parent: TSESTree.JSXElement;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.JSXElement` | ✗ |  |

### `JSXClosingFragment`

<details><summary>Interface Code</summary>

```ts
interface JSXClosingFragment {
    parent: TSESTree.JSXFragment;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.JSXFragment` | ✗ |  |

### `JSXOpeningElement`

<details><summary>Interface Code</summary>

```ts
interface JSXOpeningElement {
    parent: TSESTree.JSXElement;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.JSXElement` | ✗ |  |

### `JSXOpeningFragment`

<details><summary>Interface Code</summary>

```ts
interface JSXOpeningFragment {
    parent: TSESTree.JSXFragment;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.JSXFragment` | ✗ |  |

### `JSXSpreadAttribute`

<details><summary>Interface Code</summary>

```ts
interface JSXSpreadAttribute {
    parent: TSESTree.JSXOpeningElement;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.JSXOpeningElement` | ✗ |  |

### `MethodDefinitionComputedName`

<details><summary>Interface Code</summary>

```ts
interface MethodDefinitionComputedName {
    parent: TSESTree.ClassBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassBody` | ✗ |  |

### `MethodDefinitionNonComputedName`

<details><summary>Interface Code</summary>

```ts
interface MethodDefinitionNonComputedName {
    parent: TSESTree.ClassBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassBody` | ✗ |  |

### `TSAbstractMethodDefinitionComputedName`

<details><summary>Interface Code</summary>

```ts
interface TSAbstractMethodDefinitionComputedName {
    parent: TSESTree.ClassBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassBody` | ✗ |  |

### `TSAbstractMethodDefinitionNonComputedName`

<details><summary>Interface Code</summary>

```ts
interface TSAbstractMethodDefinitionNonComputedName {
    parent: TSESTree.ClassBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassBody` | ✗ |  |

### `PropertyComputedName`

<details><summary>Interface Code</summary>

```ts
interface PropertyComputedName {
    parent: TSESTree.ObjectExpression | TSESTree.ObjectPattern;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ObjectExpression | TSESTree.ObjectPattern` | ✗ |  |

### `PropertyNonComputedName`

<details><summary>Interface Code</summary>

```ts
interface PropertyNonComputedName {
    parent: TSESTree.ObjectExpression | TSESTree.ObjectPattern;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ObjectExpression | TSESTree.ObjectPattern` | ✗ |  |

### `PropertyDefinitionComputedName`

<details><summary>Interface Code</summary>

```ts
interface PropertyDefinitionComputedName {
    parent: TSESTree.ClassBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassBody` | ✗ |  |

### `PropertyDefinitionNonComputedName`

<details><summary>Interface Code</summary>

```ts
interface PropertyDefinitionNonComputedName {
    parent: TSESTree.ClassBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassBody` | ✗ |  |

### `TSAbstractPropertyDefinitionComputedName`

<details><summary>Interface Code</summary>

```ts
interface TSAbstractPropertyDefinitionComputedName {
    parent: TSESTree.ClassBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassBody` | ✗ |  |

### `TSAbstractPropertyDefinitionNonComputedName`

<details><summary>Interface Code</summary>

```ts
interface TSAbstractPropertyDefinitionNonComputedName {
    parent: TSESTree.ClassBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassBody` | ✗ |  |

### `SpreadElement`

<details><summary>Interface Code</summary>

```ts
interface SpreadElement {
    parent:
      | TSESTree.ArrayExpression
      | TSESTree.CallExpression
      | TSESTree.NewExpression
      | TSESTree.ObjectExpression;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `| TSESTree.ArrayExpression
      | TSESTree.CallExpression
      | TSESTree.NewExpression
      | TSESTree.ObjectExpression` | ✗ |  |

### `StaticBlock`

<details><summary>Interface Code</summary>

```ts
interface StaticBlock {
    parent: TSESTree.ClassBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassBody` | ✗ |  |

### `SwitchCase`

<details><summary>Interface Code</summary>

```ts
interface SwitchCase {
    parent: TSESTree.SwitchStatement;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.SwitchStatement` | ✗ |  |

### `TemplateElement`

<details><summary>Interface Code</summary>

```ts
interface TemplateElement {
    parent: TSESTree.TemplateLiteral | TSESTree.TSTemplateLiteralType;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TemplateLiteral | TSESTree.TSTemplateLiteralType` | ✗ |  |

### `TSCallSignatureDeclaration`

<details><summary>Interface Code</summary>

```ts
interface TSCallSignatureDeclaration {
    parent: TSESTree.TSInterfaceBody | TSESTree.TSTypeLiteral;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TSInterfaceBody | TSESTree.TSTypeLiteral` | ✗ |  |

### `TSConstructSignatureDeclaration`

<details><summary>Interface Code</summary>

```ts
interface TSConstructSignatureDeclaration {
    parent: TSESTree.TSInterfaceBody | TSESTree.TSTypeLiteral;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TSInterfaceBody | TSESTree.TSTypeLiteral` | ✗ |  |

### `TSClassImplements`

<details><summary>Interface Code</summary>

```ts
interface TSClassImplements {
    parent: TSESTree.ClassDeclaration | TSESTree.ClassExpression;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ClassDeclaration | TSESTree.ClassExpression` | ✗ |  |

### `TSEnumBody`

<details><summary>Interface Code</summary>

```ts
interface TSEnumBody {
    parent: TSESTree.TSEnumDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TSEnumDeclaration` | ✗ |  |

### `TSEnumMemberComputedName`

<details><summary>Interface Code</summary>

```ts
interface TSEnumMemberComputedName {
    parent: TSESTree.TSEnumBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TSEnumBody` | ✗ |  |

### `TSEnumMemberNonComputedName`

<details><summary>Interface Code</summary>

```ts
interface TSEnumMemberNonComputedName {
    parent: TSESTree.TSEnumBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TSEnumBody` | ✗ |  |

### `TSIndexSignature`

<details><summary>Interface Code</summary>

```ts
interface TSIndexSignature {
    parent:
      | TSESTree.ClassBody
      | TSESTree.TSInterfaceBody
      | TSESTree.TSTypeLiteral;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `| TSESTree.ClassBody
      | TSESTree.TSInterfaceBody
      | TSESTree.TSTypeLiteral` | ✗ |  |

### `TSInterfaceBody`

<details><summary>Interface Code</summary>

```ts
interface TSInterfaceBody {
    parent: TSESTree.TSInterfaceDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TSInterfaceDeclaration` | ✗ |  |

### `TSInterfaceHeritage`

<details><summary>Interface Code</summary>

```ts
interface TSInterfaceHeritage {
    parent: TSESTree.TSInterfaceBody;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TSInterfaceBody` | ✗ |  |

### `TSMethodSignatureComputedName`

<details><summary>Interface Code</summary>

```ts
interface TSMethodSignatureComputedName {
    parent: TSESTree.TSInterfaceBody | TSESTree.TSTypeLiteral;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TSInterfaceBody | TSESTree.TSTypeLiteral` | ✗ |  |

### `TSMethodSignatureNonComputedName`

<details><summary>Interface Code</summary>

```ts
interface TSMethodSignatureNonComputedName {
    parent: TSESTree.TSInterfaceBody | TSESTree.TSTypeLiteral;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TSInterfaceBody | TSESTree.TSTypeLiteral` | ✗ |  |

### `TSModuleBlock`

<details><summary>Interface Code</summary>

```ts
interface TSModuleBlock {
    parent: TSESTree.TSModuleDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TSModuleDeclaration` | ✗ |  |

### `TSParameterProperty`

<details><summary>Interface Code</summary>

```ts
interface TSParameterProperty {
    parent: TSESTree.FunctionLike;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.FunctionLike` | ✗ |  |

### `TSPropertySignatureComputedName`

<details><summary>Interface Code</summary>

```ts
interface TSPropertySignatureComputedName {
    parent: TSESTree.TSInterfaceBody | TSESTree.TSTypeLiteral;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TSInterfaceBody | TSESTree.TSTypeLiteral` | ✗ |  |

### `TSPropertySignatureNonComputedName`

<details><summary>Interface Code</summary>

```ts
interface TSPropertySignatureNonComputedName {
    parent: TSESTree.TSInterfaceBody | TSESTree.TSTypeLiteral;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.TSInterfaceBody | TSESTree.TSTypeLiteral` | ✗ |  |

### `TSTypeParameter`

<details><summary>Interface Code</summary>

```ts
interface TSTypeParameter {
    parent:
      | TSESTree.TSInferType
      | TSESTree.TSMappedType
      | TSESTree.TSTypeParameterDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `| TSESTree.TSInferType
      | TSESTree.TSMappedType
      | TSESTree.TSTypeParameterDeclaration` | ✗ |  |

### `ExportSpecifierWithIdentifierLocal`

<details><summary>Interface Code</summary>

```ts
interface ExportSpecifierWithIdentifierLocal {
    parent: TSESTree.ExportNamedDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ExportNamedDeclaration` | ✗ |  |

### `ExportSpecifierWithStringOrLiteralLocal`

<details><summary>Interface Code</summary>

```ts
interface ExportSpecifierWithStringOrLiteralLocal {
    parent: TSESTree.ExportNamedDeclaration;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `parent` | `TSESTree.ExportNamedDeclaration` | ✗ |  |


---