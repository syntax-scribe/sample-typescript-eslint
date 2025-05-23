[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `optimizeAST.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-schema-to-typescript-types/src/optimizeAST.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST` | `./types` |
| `UnionAST` | `./types` |


---

## Functions

### `optimizeAST(ast: AST | null): void`

<details><summary>Code</summary>

```ts
export function optimizeAST(ast: AST | null): void {
  if (ast == null) {
    return;
  }

  switch (ast.type) {
    case 'array': {
      optimizeAST(ast.elementType);
      return;
    }

    case 'literal':
      return;

    case 'object': {
      for (const property of ast.properties) {
        optimizeAST(property.type);
      }
      optimizeAST(ast.indexSignature);
      return;
    }

    case 'tuple': {
      for (const element of ast.elements) {
        optimizeAST(element);
      }
      optimizeAST(ast.spreadType);
      return;
    }

    case 'type-reference':
      return;

    case 'union': {
      const elements = unwrapUnions(ast);
      for (const element of elements) {
        optimizeAST(element);
      }

      // hacky way to deduplicate union members
      const uniqueElementsMap = new Map<string, AST>();
      for (const element of elements) {
        uniqueElementsMap.set(JSON.stringify(element), element);
      }
      const uniqueElements = [...uniqueElementsMap.values()];

      // @ts-expect-error -- purposely overwriting the property with a flattened list
      ast.elements = uniqueElements;
      return;
    }
  }
}
```
</details>

- **Parameters**:
  - `ast: AST | null`
- **Return Type**: `void`
- **Calls**:
  - `optimizeAST`
  - `unwrapUnions`
  - `uniqueElementsMap.set`
  - `JSON.stringify`
  - `uniqueElementsMap.values`
- **Internal Comments**:
```
// hacky way to deduplicate union members (x2)
// @ts-expect-error -- purposely overwriting the property with a flattened list (x4)
```

### `unwrapUnions(union: UnionAST): AST[]`

<details><summary>Code</summary>

```ts
function unwrapUnions(union: UnionAST): AST[] {
  const elements: AST[] = [];
  for (const element of union.elements) {
    if (element.type === 'union') {
      elements.push(...unwrapUnions(element));
    } else {
      elements.push(element);
    }
  }

  if (elements.length > 0) {
    // preserve the union's comment lines by prepending them to the first element's lines
    elements[0].commentLines.unshift(...union.commentLines);
  }

  return elements;
}
```
</details>

- **Parameters**:
  - `union: UnionAST`
- **Return Type**: `AST[]`
- **Calls**:
  - `elements.push`
  - `unwrapUnions`
  - `elements[0].commentLines.unshift`
- **Internal Comments**:
```
// preserve the union's comment lines by prepending them to the first element's lines (x6)
```


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