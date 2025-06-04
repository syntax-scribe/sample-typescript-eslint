[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-mixed-enums.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 5 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 3 |
| 📐 Interfaces | 1 |
| 🎯 Enums | 1 |


## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Enums](#enums)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-mixed-enums.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Scope` | `@typescript-eslint/scope-manager` |
| `TSESTree` | `@typescript-eslint/utils` |
| `DefinitionType` | `@typescript-eslint/scope-manager` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `found` | `CollectedDefinitions` | const | `{
        imports: [],
        previousSibling: undefined,
      }` | ✗ |
| `valueDeclaration` | `any` | const | `type.getSymbol()?.valueDeclaration` | ✗ |
| `declarations` | `any` | const | `typeChecker
          .getSymbolAtLocation(tsNode)!
          .getDeclarations()!` | ✗ |


---

## Functions

### `collectNodeDefinitions(node: TSESTree.TSEnumDeclaration): CollectedDefinitions`

<details><summary>Code</summary>

```ts
function collectNodeDefinitions(
      node: TSESTree.TSEnumDeclaration,
    ): CollectedDefinitions {
      const { name } = node.id;
      const found: CollectedDefinitions = {
        imports: [],
        previousSibling: undefined,
      };
      let scope: Scope | null = context.sourceCode.getScope(node);

      for (const definition of scope.upper?.set.get(name)?.defs ?? []) {
        if (
          definition.node.type === AST_NODE_TYPES.TSEnumDeclaration &&
          definition.node.range[0] < node.range[0] &&
          definition.node.body.members.length > 0
        ) {
          found.previousSibling = definition.node;
          break;
        }
      }

      while (scope) {
        scope.set.get(name)?.defs.forEach(definition => {
          if (definition.type === DefinitionType.ImportBinding) {
            found.imports.push(definition.node);
          }
        });

        scope = scope.upper;
      }

      return found;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumDeclaration`
- **Return Type**: `CollectedDefinitions`
- **Calls**:
  - `context.sourceCode.getScope`
  - `scope.upper?.set.get`
  - `scope.set.get(name)?.defs.forEach`
  - `found.imports.push`
### `getAllowedTypeForNode(node: ts.Node): AllowedType`

<details><summary>Code</summary>

```ts
function getAllowedTypeForNode(node: ts.Node): AllowedType {
      return tsutils.isTypeFlagSet(
        typeChecker.getTypeAtLocation(node),
        ts.TypeFlags.StringLike,
      )
        ? AllowedType.String
        : AllowedType.Number;
    }
```
</details>

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `AllowedType`
- **Calls**:
  - `tsutils.isTypeFlagSet`
  - `typeChecker.getTypeAtLocation`
### `getTypeFromImported(imported: TSESTree.Node): AllowedType | undefined`

<details><summary>Code</summary>

```ts
function getTypeFromImported(
      imported: TSESTree.Node,
    ): AllowedType | undefined {
      const type = typeChecker.getTypeAtLocation(
        parserServices.esTreeNodeToTSNodeMap.get(imported),
      );

      const valueDeclaration = type.getSymbol()?.valueDeclaration;
      if (
        !valueDeclaration ||
        !ts.isEnumDeclaration(valueDeclaration) ||
        valueDeclaration.members.length === 0
      ) {
        return undefined;
      }

      return getAllowedTypeForNode(valueDeclaration.members[0]);
    }
```
</details>

- **Parameters**:
  - `imported: TSESTree.Node`
- **Return Type**: `AllowedType | undefined`
- **Calls**:
  - `typeChecker.getTypeAtLocation`
  - `parserServices.esTreeNodeToTSNodeMap.get`
  - `type.getSymbol`
  - `ts.isEnumDeclaration`
  - `getAllowedTypeForNode`
### `getMemberType(member: TSESTree.TSEnumMember): AllowedType`

<details><summary>Code</summary>

```ts
function getMemberType(member: TSESTree.TSEnumMember): AllowedType {
      if (!member.initializer) {
        return AllowedType.Number;
      }

      switch (member.initializer.type) {
        case AST_NODE_TYPES.Literal:
          switch (typeof member.initializer.value) {
            case 'number':
              return AllowedType.Number;
            case 'string':
              return AllowedType.String;
            default:
              return AllowedType.Unknown;
          }

        case AST_NODE_TYPES.TemplateLiteral:
          return AllowedType.String;

        default:
          return getAllowedTypeForNode(
            parserServices.esTreeNodeToTSNodeMap.get(member.initializer),
          );
      }
    }
```
</details>

- **Parameters**:
  - `member: TSESTree.TSEnumMember`
- **Return Type**: `AllowedType`
- **Calls**:
  - `getAllowedTypeForNode`
  - `parserServices.esTreeNodeToTSNodeMap.get`
### `getDesiredTypeForDefinition(node: TSESTree.TSEnumDeclaration): AllowedType | ts.TypeFlags.Unknown | undefined`

<details><summary>Code</summary>

```ts
function getDesiredTypeForDefinition(
      node: TSESTree.TSEnumDeclaration,
    ): AllowedType | ts.TypeFlags.Unknown | undefined {
      const { imports, previousSibling } = collectNodeDefinitions(node);

      // Case: Merged ambiently via module augmentation
      // import { MyEnum } from 'other-module';
      // declare module 'other-module' {
      //   enum MyEnum { A }
      // }
      for (const imported of imports) {
        const typeFromImported = getTypeFromImported(imported);
        if (typeFromImported != null) {
          return typeFromImported;
        }
      }

      // Case: Multiple enum declarations in the same file
      // enum MyEnum { A }
      // enum MyEnum { B }
      if (previousSibling) {
        return getMemberType(previousSibling.body.members[0]);
      }

      // Case: Namespace declaration merging
      // namespace MyNamespace {
      //   export enum MyEnum { A }
      // }
      // namespace MyNamespace {
      //   export enum MyEnum { B }
      // }
      if (
        node.parent.type === AST_NODE_TYPES.ExportNamedDeclaration &&
        node.parent.parent.type === AST_NODE_TYPES.TSModuleBlock
      ) {
        // https://github.com/typescript-eslint/typescript-eslint/issues/8352
        // TODO: We don't need to dip into the TypeScript type checker here!
        // Merged namespaces must all exist in the same file.
        // We could instead compare this file's nodes to find the merges.
        const tsNode = parserServices.esTreeNodeToTSNodeMap.get(node.id);
        // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
        const declarations = typeChecker
          .getSymbolAtLocation(tsNode)!
          .getDeclarations()!;

        const [{ initializer }] = (declarations[0] as ts.EnumDeclaration)
          .members;
        return initializer &&
          tsutils.isTypeFlagSet(
            typeChecker.getTypeAtLocation(initializer),
            ts.TypeFlags.StringLike,
          )
          ? AllowedType.String
          : AllowedType.Number;
      }

      // Finally, we default to the type of the first enum member
      return getMemberType(node.body.members[0]);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumDeclaration`
- **Return Type**: `AllowedType | ts.TypeFlags.Unknown | undefined`
- **Calls**:
  - `collectNodeDefinitions`
  - `getTypeFromImported`
  - `getMemberType`
  - `parserServices.esTreeNodeToTSNodeMap.get`
  - `typeChecker
          .getSymbolAtLocation(tsNode)!
          .getDeclarations`
  - `tsutils.isTypeFlagSet`
  - `typeChecker.getTypeAtLocation`
- **Internal Comments**:
```
// Case: Merged ambiently via module augmentation
// import { MyEnum } from 'other-module';
// declare module 'other-module' {
//   enum MyEnum { A }
// } (x3)
// Case: Multiple enum declarations in the same file
// enum MyEnum { A }
// enum MyEnum { B }
// Case: Namespace declaration merging
// namespace MyNamespace { (x2)
//   export enum MyEnum { A }
//   export enum MyEnum { B }
// https://github.com/typescript-eslint/typescript-eslint/issues/8352 (x2)
// TODO: We don't need to dip into the TypeScript type checker here! (x2)
// Merged namespaces must all exist in the same file. (x2)
// We could instead compare this file's nodes to find the merges. (x2)
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x2)
// Finally, we default to the type of the first enum member
```


---

## Interfaces

### `CollectedDefinitions`

<details><summary>Interface Code</summary>

```ts
interface CollectedDefinitions {
      imports: TSESTree.Node[];
      previousSibling: TSESTree.TSEnumDeclaration | undefined;
    }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `imports` | `TSESTree.Node[]` | ✗ |  |
| `previousSibling` | `TSESTree.TSEnumDeclaration | undefined` | ✗ |  |


---

## Enums

### `enum AllowedType`

<details><summary>Enum Code</summary>

```ts
enum AllowedType {
  Number,
  String,
  Unknown,
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `Number` | *auto* |  |
| `String` | *auto* |  |
| `Unknown` | *auto* |  |


---