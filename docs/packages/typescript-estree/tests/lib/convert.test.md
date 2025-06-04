[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `convert.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 6 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 17 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `instance` | `Converter` | const | `new Converter(ast)` | ✗ |
| `instance` | `Converter` | const | `new Converter(ast)` | ✗ |
| `instance` | `Converter` | const | `new Converter(ast)` | ✗ |
| `instance` | `Converter` | const | `new Converter(ast)` | ✗ |
| `instance` | `Converter` | const | `new Converter(ast)` | ✗ |
| `instance` | `Converter` | const | `new Converter(ast, {
        errorOnUnknownASTType: true,
      })` | ✗ |
| `instance` | `Converter` | const | `new Converter(ast, {
      shouldPreserveNodeMaps: true,
    })` | ✗ |
| `instance` | `Converter` | const | `new Converter(ast, {
      shouldPreserveNodeMaps: true,
    })` | ✗ |
| `instance` | `Converter` | const | `new Converter(ast, {
      shouldPreserveNodeMaps: true,
    })` | ✗ |
| `instance` | `Converter` | const | `new Converter(ast, {
        shouldPreserveNodeMaps: true,
      })` | ✗ |
| `tsNode` | `ts.KeywordToken<ts.SyntaxKind.AbstractKeyword>` | const | `{
        ...ts.factory.createToken(ts.SyntaxKind.AbstractKeyword),
        end: 10,
        pos: 0,
      }` | ✗ |
| `jsDocCode` | `readonly ["const x: function(new: number, string);", "const x: function(this: number, string);", "var g: function(number, number): number;"]` | const | `[
      'const x: function(new: number, string);',
      'const x: function(this: number, string);',
      'var g: function(number, number): number;',
    ] as const` | ✗ |
| `instance` | `Converter` | const | `new Converter(ast)` | ✗ |
| `code` | `"const;"` | const | `'const;'` | ✗ |
| `instance` | `Converter` | const | `new Converter(ast)` | ✗ |
| `instance` | `Converter` | const | `new Converter(ast, {
        allowInvalidAST: true,
      })` | ✗ |
| `instance` | `Converter` | const | `new Converter(ast, {
          shouldPreserveNodeMaps: true,
          ...converterOptions,
        })` | ✗ |


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