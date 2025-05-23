[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `convert.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 6
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/tests/lib/convert.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `TSNode` | `../../src` |
| `ConverterOptions` | `../../src/convert` |
| `Converter` | `../../src/convert` |


---

## Functions

### `convertCode(code: string): ts.SourceFile`

<details><summary>Code</summary>

```ts
function convertCode(code: string): ts.SourceFile {
    return ts.createSourceFile(
      'text.ts',
      code,
      ts.ScriptTarget.ESNext,
      true,
      ts.ScriptKind.TSX,
    );
  }
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `ts.SourceFile`
- **Calls**:
  - `ts.createSourceFile`
### `fakeUnknownKind(node: ts.Node): void`

<details><summary>Code</summary>

```ts
function fakeUnknownKind(node: ts.Node): void {
        ts.forEachChild(node, fakeUnknownKind);
        // @ts-expect-error -- intentionally writing to a readonly field
        node.kind = ts.SyntaxKind.UnparsedPrologue;
      }
```
</details>

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `void`
- **Calls**:
  - `ts.forEachChild`
- **Internal Comments**:
```
// @ts-expect-error -- intentionally writing to a readonly field (x4)
```

### `checkMaps(child: ts.Node | ts.SourceFile): void`

<details><summary>Code</summary>

```ts
function checkMaps(child: ts.Node | ts.SourceFile): void {
      child.forEachChild(node => {
        if (
          node.kind !== ts.SyntaxKind.EndOfFileToken &&
          node.kind !== ts.SyntaxKind.JsxAttributes &&
          node.kind !== ts.SyntaxKind.VariableDeclaration
        ) {
          expect(node).toBe(
            maps.esTreeNodeToTSNodeMap.get(
              maps.tsNodeToESTreeNodeMap.get(node as TSNode),
            ),
          );
        }
        checkMaps(node);
      });
    }
```
</details>

- **Parameters**:
  - `child: ts.Node | ts.SourceFile`
- **Return Type**: `void`
- **Calls**:
  - `child.forEachChild`
  - `expect(node).toBe`
  - `maps.esTreeNodeToTSNodeMap.get`
  - `maps.tsNodeToESTreeNodeMap.get`
  - `checkMaps`
### `checkMaps(child: ts.Node | ts.SourceFile): void`

<details><summary>Code</summary>

```ts
function checkMaps(child: ts.Node | ts.SourceFile): void {
      child.forEachChild(node => {
        if (
          node.kind !== ts.SyntaxKind.EndOfFileToken &&
          node.kind !== ts.SyntaxKind.JsxAttributes
        ) {
          expect(node).toBe(
            maps.esTreeNodeToTSNodeMap.get(
              maps.tsNodeToESTreeNodeMap.get(node as TSNode),
            ),
          );
        }
        checkMaps(node);
      });
    }
```
</details>

- **Parameters**:
  - `child: ts.Node | ts.SourceFile`
- **Return Type**: `void`
- **Calls**:
  - `child.forEachChild`
  - `expect(node).toBe`
  - `maps.esTreeNodeToTSNodeMap.get`
  - `maps.tsNodeToESTreeNodeMap.get`
  - `checkMaps`
### `checkMaps(child: ts.Node | ts.SourceFile): void`

<details><summary>Code</summary>

```ts
function checkMaps(child: ts.Node | ts.SourceFile): void {
      child.forEachChild(node => {
        if (node.kind !== ts.SyntaxKind.EndOfFileToken) {
          expect(ast).toBe(
            maps.esTreeNodeToTSNodeMap.get(maps.tsNodeToESTreeNodeMap.get(ast)),
          );
        }
        checkMaps(node);
      });
    }
```
</details>

- **Parameters**:
  - `child: ts.Node | ts.SourceFile`
- **Return Type**: `void`
- **Calls**:
  - `child.forEachChild`
  - `expect(ast).toBe`
  - `maps.esTreeNodeToTSNodeMap.get`
  - `maps.tsNodeToESTreeNodeMap.get`
  - `checkMaps`
### `makeNodeGetter(code: string, tsToEsNode: (statement: S) => TSNode): (converterOptions?: ConverterOptions) => TNode`

<details><summary>Code</summary>

```ts
<
        // Small convenience for testing the nodes:
        // eslint-disable-next-line @typescript-eslint/no-unnecessary-type-parameters
        S extends ts.Statement,
        // eslint-disable-next-line @typescript-eslint/no-unnecessary-type-parameters
        TNode extends TSESTree.Node,
      >(
        code: string,
        tsToEsNode: (statement: S) => TSNode,
      ) =>
      (converterOptions?: ConverterOptions): TNode => {
        const ast = convertCode(code);
        const instance = new Converter(ast, {
          shouldPreserveNodeMaps: true,
          ...converterOptions,
        });

        instance.convertProgram();

        return instance
          .getASTMaps()
          .tsNodeToESTreeNodeMap.get(tsToEsNode(ast.statements[0] as S));
      }
```
</details>

- **Parameters**:
  - `code: string`
  - `tsToEsNode: (statement: S) => TSNode`
- **Return Type**: `(converterOptions?: ConverterOptions) => TNode`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---