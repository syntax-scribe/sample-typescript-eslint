[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Node.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 7
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/util/serializers/Node.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `NewPlugin` | `@vitest/pretty-format` |
| `AST_NODE_TYPES` | `../../../src/index.js` |


---

## Functions

### `sortKeys(node: Node): (keyof typeof node)[]`

<details><summary>Code</summary>

```ts
function sortKeys<Node extends TSESTree.Node>(
  node: Node,
): (keyof typeof node)[] {
  const keySet = new Set(Object.keys(node));

  // type place as first key
  keySet.delete('type');
  // range and loc we place after all properties
  keySet.delete('range');
  keySet.delete('loc');

  // babel keys
  keySet.delete('start');
  keySet.delete('end');
  if (node.type === AST_NODE_TYPES.Program) {
    keySet.delete('interpreter');
  }

  return [...keySet].sort((a, b) =>
    a.localeCompare(b),
  ) as (keyof typeof node)[];
}
```
</details>

- **Parameters**:
  - `node: Node`
- **Return Type**: `(keyof typeof node)[]`
- **Calls**:
  - `Object.keys`
  - `keySet.delete`
  - `[...keySet].sort`
  - `a.localeCompare`
- **Internal Comments**:
```
// type place as first key (x4)
// range and loc we place after all properties (x4)
// babel keys (x4)
```

### `stringifyLineAndColumn(loc: TSESTree.Position): string`

<details><summary>Code</summary>

```ts
function stringifyLineAndColumn(loc: TSESTree.Position): string {
  return `{ column: ${loc.column.toString()}, line: ${loc.line.toString()} }`;
}
```
</details>

- **Parameters**:
  - `loc: TSESTree.Position`
- **Return Type**: `string`
- **Calls**:
  - `loc.column.toString`
  - `loc.line.toString`
### `isObject(val: unknown): val is Record<string, unknown>`

<details><summary>Code</summary>

```ts
function isObject(val: unknown): val is Record<string, unknown> {
  return val != null && typeof val === 'object';
}
```
</details>

- **Parameters**:
  - `val: unknown`
- **Return Type**: `val is Record<string, unknown>`
### `hasValidType(type: unknown): type is string`

<details><summary>Code</summary>

```ts
function hasValidType(type: unknown): type is string {
  return typeof type === 'string';
}
```
</details>

- **Parameters**:
  - `type: unknown`
- **Return Type**: `type is string`
### `printValue(value: unknown): string`

<details><summary>Code</summary>

```ts
(value: unknown): string =>
      printer(value, config, childIndentation, depth, refs)
```
</details>

- **Parameters**:
  - `value: unknown`
- **Return Type**: `string`
- **Calls**:
  - `printer`
### `serialize(node: Record<string, unknown> & TSESTree.Node, config: any, indentation: any, depth: any, refs: any, printer: any): string`

<details><summary>Code</summary>

```ts
serialize(
    node: Record<string, unknown> & TSESTree.Node,
    config,
    indentation,
    depth,
    refs,
    printer,
  ) {
    const keys = sortKeys(node);
    const { loc, range, type } = node;

    const outputLines = [];
    const childIndentation = indentation + config.indent;

    const printValue = (value: unknown): string =>
      printer(value, config, childIndentation, depth, refs);

    outputLines.push(`${type} {`);
    outputLines.push(`${childIndentation}type: ${printValue(type)},`);

    for (const key of keys) {
      const value = node[key];
      // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish -- intentional strict equality
      if (value === undefined) {
        continue;
      }

      outputLines.push(`${childIndentation}${key}: ${printValue(value)},`);
    }

    outputLines.push('');
    outputLines.push(`${childIndentation}range: [${range.join(', ')}],`);
    outputLines.push(
      `${childIndentation}loc: {`,
      `${childIndentation}${config.indent}start: ${stringifyLineAndColumn(
        loc.start,
      )},`,
      `${childIndentation}${config.indent}end: ${stringifyLineAndColumn(
        loc.end,
      )},`,
      `${childIndentation}},`,
    );
    outputLines.push(`${indentation}}`);

    return outputLines.join('\n');
  }
```
</details>

- **Parameters**:
  - `node: Record<string, unknown> & TSESTree.Node`
  - `config: any`
  - `indentation: any`
  - `depth: any`
  - `refs: any`
  - `printer: any`
- **Return Type**: `string`
- **Calls**:
  - `sortKeys`
  - `printer`
  - `outputLines.push`
  - `printValue`
  - `range.join`
  - `stringifyLineAndColumn`
  - `outputLines.join`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish -- intentional strict equality
```

### `test(val: unknown): boolean`

<details><summary>Code</summary>

```ts
test(val: unknown) {
    return isObject(val) && hasValidType(val.type);
  }
```
</details>

- **Parameters**:
  - `val: unknown`
- **Return Type**: `boolean`
- **Calls**:
  - `isObject`
  - `hasValidType`

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