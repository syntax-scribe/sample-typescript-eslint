[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `printAST.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 6 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 6 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/rule-schema-to-typescript-types/src/printAST.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `naturalCompare` | `natural-compare` |
| `AST` | `./types` |
| `TupleAST` | `./types` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `commentLines` | `string[]` | const | `[]` | ✗ |
| `properties` | `any[]` | const | `[]` | ✗ |
| `elements` | `any[]` | const | `[]` | ✗ |
| `code` | `string` | const | ``${printComment(result)} | ${result.code}`` | ✗ |
| `aElement` | `TupleAST` | const | `a.element` | ✗ |
| `bElement` | `TupleAST` | const | `b.element as TupleAST` | ✗ |


---

## Functions

### `printTypeAlias(aliasName: string, ast: AST): string`

<details><summary>Code</summary>

```ts
export function printTypeAlias(aliasName: string, ast: AST): string {
  return `${printComment(ast)}type ${aliasName} = ${printAST(ast).code}`;
}
```
</details>

- **Parameters**:
  - `aliasName: string`
  - `ast: AST`
- **Return Type**: `string`
- **Calls**:
  - `printComment`
  - `printAST`
### `printASTWithComment(ast: AST): string`

<details><summary>Code</summary>

```ts
export function printASTWithComment(ast: AST): string {
  const result = printAST(ast);
  return `${printComment(result)}${result.code}`;
}
```
</details>

- **Parameters**:
  - `ast: AST`
- **Return Type**: `string`
- **Calls**:
  - `printAST`
  - `printComment`
### `printComment({
  commentLines: commentLinesIn,
}: {
  readonly commentLines?: string[] | null | undefined;
}): string`

<details><summary>Code</summary>

```ts
function printComment({
  commentLines: commentLinesIn,
}: {
  readonly commentLines?: string[] | null | undefined;
}): string {
  if (commentLinesIn == null || commentLinesIn.length === 0) {
    return '';
  }

  const commentLines: string[] = [];
  for (const line of commentLinesIn) {
    commentLines.push(...line.split('\n'));
  }

  if (commentLines.length === 1) {
    return `/** ${commentLines[0]} */\n`;
  }

  return ['/**', ...commentLines.map(l => ` * ${l}`), ' */', ''].join('\n');
}
```
</details>

- **Parameters**:
  - `{
  commentLines: commentLinesIn,
}: {
  readonly commentLines?: string[] | null | undefined;
}`
- **Return Type**: `string`
- **Calls**:
  - `commentLines.push`
  - `line.split`
  - `['/**', ...commentLines.map(l => ` * ${l}`), ' */', ''].join`
  - `commentLines.map`
### `printAST(ast: AST): CodeWithComments`

<details><summary>Code</summary>

```ts
function printAST(ast: AST): CodeWithComments {
  switch (ast.type) {
    case 'array': {
      const code = printAndMaybeParenthesise(ast.elementType);
      return {
        code: `${code.code}[]`,
        commentLines: [...ast.commentLines, ...code.commentLines],
      };
    }

    case 'literal':
      return {
        code: ast.code,
        commentLines: ast.commentLines,
      };

    case 'object': {
      const properties = [];
      // sort the properties so that we get consistent output regardless
      // of import declaration order
      const sortedPropertyDefs = ast.properties.sort((a, b) =>
        naturalCompare(a.name, b.name),
      );
      for (const property of sortedPropertyDefs) {
        const result = printAST(property.type);
        properties.push(
          `${printComment(result)}${property.name}${
            property.optional ? '?:' : ':'
          } ${result.code}`,
        );
      }

      if (ast.indexSignature) {
        const result = printAST(ast.indexSignature);
        properties.push(`${printComment(result)}[k: string]: ${result.code}`);
      }
      return {
        // force insert a newline so prettier consistently prints all objects as multiline
        code: `{\n${properties.join(';\n')}}`,
        commentLines: ast.commentLines,
      };
    }

    case 'tuple': {
      const elements = [];
      for (const element of ast.elements) {
        elements.push(printASTWithComment(element));
      }
      if (ast.spreadType) {
        const result = printAndMaybeParenthesise(ast.spreadType);
        elements.push(`${printComment(result)}...${result.code}[]`);
      }

      return {
        code: `[${elements.join(',')}]`,
        commentLines: ast.commentLines,
      };
    }

    case 'type-reference':
      return {
        code: ast.typeName,
        commentLines: ast.commentLines,
      };

    case 'union':
      return {
        code: ast.elements
          .map(element => {
            const result = printAST(element);
            const code = `${printComment(result)} | ${result.code}`;
            return {
              code,
              element,
            };
          })
          // sort the union members so that we get consistent output regardless
          // of declaration order
          .sort((a, b) => compareElements(a, b))
          .map(el => el.code)
          .join('\n'),
        commentLines: ast.commentLines,
      };
  }
}
```
</details>

- **Parameters**:
  - `ast: AST`
- **Return Type**: `CodeWithComments`
- **Calls**:
  - `printAndMaybeParenthesise`
  - `ast.properties.sort`
  - `naturalCompare (from natural-compare)`
  - `printAST`
  - `properties.push`
  - `printComment`
  - `properties.join`
  - `elements.push`
  - `printASTWithComment`
  - `elements.join`
  - `ast.elements
          .map(element => {
            const result = printAST(element);
            const code = `${printComment(result)} | ${result.code}`;
            return {
              code,
              element,
            };
          })
          // sort the union members so that we get consistent output regardless
          // of declaration order
          .sort((a, b) => compareElements(a, b))
          .map(el => el.code)
          .join`
- **Internal Comments**:
```
// sort the properties so that we get consistent output regardless (x2)
// of import declaration order (x2)
// force insert a newline so prettier consistently prints all objects as multiline (x2)
```

### `compareElements(a: Element, b: Element): number`

<details><summary>Code</summary>

```ts
function compareElements(a: Element, b: Element): number {
  if (a.element.type !== b.element.type) {
    return naturalCompare(a.code, b.code);
  }

  switch (a.element.type) {
    case 'array':
    case 'literal':
    case 'type-reference':
    case 'object':
    case 'union':
      return naturalCompare(a.code, b.code);

    case 'tuple': {
      // natural compare will sort longer tuples before shorter ones
      // which is the opposite of what we want, so we sort first by length THEN
      // by code to ensure shorter tuples come first
      const aElement = a.element;
      const bElement = b.element as TupleAST;
      if (aElement.elements.length !== bElement.elements.length) {
        return aElement.elements.length - bElement.elements.length;
      }
      return naturalCompare(a.code, b.code);
    }
  }
}
```
</details>

- **Parameters**:
  - `a: Element`
  - `b: Element`
- **Return Type**: `number`
- **Calls**:
  - `naturalCompare (from natural-compare)`
- **Internal Comments**:
```
// natural compare will sort longer tuples before shorter ones (x2)
// which is the opposite of what we want, so we sort first by length THEN (x2)
// by code to ensure shorter tuples come first (x2)
```

### `printAndMaybeParenthesise(ast: AST): CodeWithComments`

<details><summary>Code</summary>

```ts
function printAndMaybeParenthesise(ast: AST): CodeWithComments {
  const printed = printAST(ast);
  if (ast.type === 'union') {
    return {
      code: `(${printed.code})`,
      commentLines: printed.commentLines,
    };
  }
  return {
    code: printed.code,
    commentLines: printed.commentLines,
  };
}
```
</details>

- **Parameters**:
  - `ast: AST`
- **Return Type**: `CodeWithComments`
- **Calls**:
  - `printAST`

---

## Interfaces

### `CodeWithComments`

<details><summary>Interface Code</summary>

```ts
interface CodeWithComments {
  code: string;
  commentLines: string[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `code` | `string` | ✗ |  |
| `commentLines` | `string[]` | ✗ |  |

### `Element`

<details><summary>Interface Code</summary>

```ts
interface Element {
  code: string;
  element: AST;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `code` | `string` | ✗ |  |
| `element` | `AST` | ✗ |  |


---