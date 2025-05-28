[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `createParserServices.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 5 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/createParserServices.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ASTMaps` | `./convert` |
| `ParserServices` | `./parser-options` |


---

## Functions

### `createParserServices(astMaps: ASTMaps, program: ts.Program | null): ParserServices`

<details><summary>Code</summary>

```ts
export function createParserServices(
  astMaps: ASTMaps,
  program: ts.Program | null,
): ParserServices {
  if (!program) {
    return {
      emitDecoratorMetadata: undefined,
      experimentalDecorators: undefined,
      isolatedDeclarations: undefined,
      program,
      // we always return the node maps because
      // (a) they don't require type info and
      // (b) they can be useful when using some of TS's internal non-type-aware AST utils
      ...astMaps,
    };
  }

  const checker = program.getTypeChecker();
  const compilerOptions = program.getCompilerOptions();

  return {
    program,
    // not set in the config is the same as off
    emitDecoratorMetadata: compilerOptions.emitDecoratorMetadata ?? false,
    experimentalDecorators: compilerOptions.experimentalDecorators ?? false,
    isolatedDeclarations: compilerOptions.isolatedDeclarations ?? false,
    ...astMaps,
    getSymbolAtLocation: node =>
      checker.getSymbolAtLocation(astMaps.esTreeNodeToTSNodeMap.get(node)),
    getTypeAtLocation: node =>
      checker.getTypeAtLocation(astMaps.esTreeNodeToTSNodeMap.get(node)),
  };
}
```
</details>

- **Parameters**:
  - `astMaps: ASTMaps`
  - `program: ts.Program | null`
- **Return Type**: `ParserServices`
- **Calls**:
  - `program.getTypeChecker`
  - `program.getCompilerOptions`
  - `checker.getSymbolAtLocation`
  - `astMaps.esTreeNodeToTSNodeMap.get`
  - `checker.getTypeAtLocation`
- **Internal Comments**:
```
// we always return the node maps because
// (a) they don't require type info and
// (b) they can be useful when using some of TS's internal non-type-aware AST utils
// not set in the config is the same as off (x2)
```

### `getSymbolAtLocation(node: TSESTree.Node): any`

<details><summary>Code</summary>

```ts
node =>
      checker.getSymbolAtLocation(astMaps.esTreeNodeToTSNodeMap.get(node))
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `any`
- **Calls**:
  - `checker.getSymbolAtLocation`
### `getTypeAtLocation(node: TSESTree.Node): any`

<details><summary>Code</summary>

```ts
node =>
      checker.getTypeAtLocation(astMaps.esTreeNodeToTSNodeMap.get(node))
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `any`
- **Calls**:
  - `checker.getTypeAtLocation`
### `getSymbolAtLocation(node: TSESTree.Node): any`

<details><summary>Code</summary>

```ts
node =>
      checker.getSymbolAtLocation(astMaps.esTreeNodeToTSNodeMap.get(node))
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `any`
- **Calls**:
  - `checker.getSymbolAtLocation`
### `getTypeAtLocation(node: TSESTree.Node): any`

<details><summary>Code</summary>

```ts
node =>
      checker.getTypeAtLocation(astMaps.esTreeNodeToTSNodeMap.get(node))
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `any`
- **Calls**:
  - `checker.getTypeAtLocation`

---