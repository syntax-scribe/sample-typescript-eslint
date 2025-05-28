[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `utils.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 11 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
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
📂 **`packages/website/src/components/ast/utils.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `ParentNodeType` | `./types` |
| `tsEnumFlagToString` | `./tsUtils` |
| `tsEnumToString` | `./tsUtils` |


---

## Functions

### `objType(obj: unknown): string`

<details><summary>Code</summary>

```ts
(obj: unknown): string =>
  typeof obj === 'object' &&
  obj &&
  Symbol.iterator in obj &&
  typeof obj[Symbol.iterator] === 'function'
    ? 'Iterable'
    : Object.prototype.toString.call(obj).slice(8, -1)
```
</details>

- **Parameters**:
  - `obj: unknown`
- **Return Type**: `string`
### `isRecord(value: unknown): value is Record<string, unknown>`

<details><summary>Code</summary>

```ts
export function isRecord(value: unknown): value is Record<string, unknown> {
  return objType(value) === 'Object';
}
```
</details>

- **Parameters**:
  - `value: unknown`
- **Return Type**: `value is Record<string, unknown>`
- **Calls**:
  - `objType`
### `isESNode(value: object): value is TSESTree.BaseNode`

<details><summary>Code</summary>

```ts
export function isESNode(value: object): value is TSESTree.BaseNode {
  return 'type' in value && 'loc' in value && 'range' in value;
}
```
</details>

- **Parameters**:
  - `value: object`
- **Return Type**: `value is TSESTree.BaseNode`
### `isTSNode(value: object): value is ts.Node`

<details><summary>Code</summary>

```ts
export function isTSNode(value: object): value is ts.Node {
  return 'kind' in value && 'pos' in value && 'flags' in value;
}
```
</details>

- **Parameters**:
  - `value: object`
- **Return Type**: `value is ts.Node`
### `getNodeType(value: unknown): ParentNodeType`

<details><summary>Code</summary>

```ts
export function getNodeType(value: unknown): ParentNodeType {
  if (Boolean(value) && isRecord(value)) {
    if (isESNode(value)) {
      return 'esNode';
    }
    if ('$id' in value && 'childScopes' in value && 'type' in value) {
      return 'scope';
    }
    if (
      'scopes' in value &&
      'nodeToScope' in value &&
      'declaredVariables' in value
    ) {
      return 'scopeManager';
    }
    if ('references' in value && 'identifiers' in value && 'name' in value) {
      return 'scopeVariable';
    }
    if ('$id' in value && 'type' in value && 'node' in value) {
      return 'scopeDefinition';
    }
    if (
      '$id' in value &&
      'resolved' in value &&
      'identifier' in value &&
      'from' in value
    ) {
      return 'scopeReference';
    }
    if ('kind' in value && 'pos' in value && 'flags' in value) {
      return 'tsNode';
    }
    if ('getSymbol' in value) {
      return 'tsType';
    }
    if ('getDeclarations' in value && value.getDeclarations != null) {
      return 'tsSymbol';
    }
    if ('getParameters' in value && value.getParameters != null) {
      return 'tsSignature';
    }
  }
  return undefined;
}
```
</details>

- **Parameters**:
  - `value: unknown`
- **Return Type**: `ParentNodeType`
- **Calls**:
  - `Boolean`
  - `isRecord`
  - `isESNode`
### `ucFirst(value: string): string`

<details><summary>Code</summary>

```ts
export function ucFirst(value: string): string {
  if (value.length > 0) {
    return value.slice(0, 1).toUpperCase() + value.slice(1);
  }
  return value;
}
```
</details>

- **Parameters**:
  - `value: string`
- **Return Type**: `string`
- **Calls**:
  - `value.slice(0, 1).toUpperCase`
  - `value.slice`
### `getTypeName(value: Record<string, unknown>, valueType: ParentNodeType): string | undefined`

<details><summary>Code</summary>

```ts
export function getTypeName(
  value: Record<string, unknown>,
  valueType: ParentNodeType,
): string | undefined {
  switch (valueType) {
    case 'esNode':
      return String(value.type);
    case 'scope':
      return `${ucFirst(String(value.type))}Scope$${String(value.$id)}`;
    case 'scopeDefinition':
      return `Definition#${String(value.type)}$${String(value.$id)}`;
    case 'scopeManager':
      return 'ScopeManager';
    case 'scopeReference':
      return `Reference#${String(
        isRecord(value.identifier) ? value.identifier.name : 'unknown',
      )}$${String(value.$id)}`;
    case 'scopeVariable':
      return `Variable#${String(value.name)}$${String(value.$id)}`;
    case 'tsNode':
      return tsEnumToString('SyntaxKind', Number(value.kind));
    case 'tsSignature':
      return '[Signature]';
    case 'tsSymbol':
      return `Symbol(${String(value.escapedName)})`;
    case 'tsType':
      return '[Type]';
  }
  return undefined;
}
```
</details>

- **Parameters**:
  - `value: Record<string, unknown>`
  - `valueType: ParentNodeType`
- **Return Type**: `string | undefined`
- **Calls**:
  - `String`
  - `ucFirst`
  - `isRecord`
  - `tsEnumToString (from ./tsUtils)`
  - `Number`
### `getTooltipLabel(value: unknown, propName: string, parentType: ParentNodeType): string | undefined`

<details><summary>Code</summary>

```ts
export function getTooltipLabel(
  value: unknown,
  propName?: string,
  parentType?: ParentNodeType,
): string | undefined {
  if (typeof value === 'number') {
    switch (parentType) {
      case 'tsNode': {
        switch (propName) {
          case 'flags':
            return tsEnumFlagToString('NodeFlags', value);
          case 'kind':
            return `SyntaxKind.${tsEnumToString('SyntaxKind', value)}`;
          case 'languageVariant':
            return `LanguageVariant.${tsEnumToString(
              'LanguageVariant',
              value,
            )}`;
          case 'languageVersion':
            return `ScriptTarget.${tsEnumToString('ScriptTarget', value)}`;
          case 'modifierFlagsCache':
            return tsEnumFlagToString('ModifierFlags', value);
          case 'numericLiteralFlags':
            return tsEnumFlagToString('TokenFlags', value);
          case 'scriptKind':
            return `ScriptKind.${tsEnumToString('ScriptKind', value)}`;
          case 'transformFlags':
            return tsEnumFlagToString('TransformFlags', value);
        }
        break;
      }
      case 'tsType':
        if (propName === 'flags') {
          return tsEnumFlagToString('TypeFlags', value);
        }
        if (propName === 'objectFlags') {
          return tsEnumFlagToString('ObjectFlags', value);
        }
        break;
      case 'tsSymbol':
        if (propName === 'flags') {
          return tsEnumFlagToString('SymbolFlags', value);
        }
        break;
    }
  }
  return undefined;
}
```
</details>

- **Parameters**:
  - `value: unknown`
  - `propName: string`
  - `parentType: ParentNodeType`
- **Return Type**: `string | undefined`
- **Calls**:
  - `tsEnumFlagToString (from ./tsUtils)`
  - `tsEnumToString (from ./tsUtils)`
### `getValidRange(range: unknown): [number, number] | undefined`

<details><summary>Code</summary>

```ts
function getValidRange(range: unknown): [number, number] | undefined {
  if (
    Array.isArray(range) &&
    typeof range[0] === 'number' &&
    typeof range[1] === 'number'
  ) {
    return range as [number, number];
  }
  return undefined;
}
```
</details>

- **Parameters**:
  - `range: unknown`
- **Return Type**: `[number, number] | undefined`
- **Calls**:
  - `Array.isArray`
### `getRange(value: unknown, valueType: ParentNodeType): [number, number] | undefined`

<details><summary>Code</summary>

```ts
export function getRange(
  value: unknown,
  valueType?: ParentNodeType,
): [number, number] | undefined {
  if (Boolean(value) && isRecord(value)) {
    switch (valueType) {
      case 'esNode':
        return getValidRange(value.range);
      case 'scope':
        if (isRecord(value.block)) {
          return getValidRange(value.block.range);
        }
        break;
      case 'scopeDefinition':
        if (isRecord(value.node)) {
          return getValidRange(value.node.range);
        }
        break;
      case 'scopeReference':
        if (isRecord(value.identifier)) {
          return getValidRange(value.identifier.range);
        }
        break;
      case 'scopeVariable':
        if (
          Array.isArray(value.identifiers) &&
          value.identifiers.length > 0 &&
          isRecord(value.identifiers[0])
        ) {
          return getValidRange(value.identifiers[0].range);
        }
        break;
      case 'tsNode':
        return getValidRange([value.pos, value.end]);
    }
  }
  return undefined;
}
```
</details>

- **Parameters**:
  - `value: unknown`
  - `valueType: ParentNodeType`
- **Return Type**: `[number, number] | undefined`
- **Calls**:
  - `Boolean`
  - `isRecord`
  - `getValidRange`
  - `Array.isArray`
### `filterProperties(key: string, value: unknown, type: ParentNodeType, showTokens: boolean): boolean`

<details><summary>Code</summary>

```ts
export function filterProperties(
  key: string,
  value: unknown,
  type: ParentNodeType,
  showTokens?: boolean,
): boolean {
  if (
    // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish -- I don't know whether this is safe to fix
    value === undefined ||
    typeof value === 'function' ||
    key.startsWith('_')
  ) {
    return false;
  }

  switch (type) {
    case 'esNode': {
      return key !== 'tokens' || !!showTokens;
    }
    case 'scopeManager':
      return (
        key !== 'declaredVariables' &&
        key !== 'nodeToScope' &&
        key !== 'currentScope'
      );
    case 'tsNode':
      return (
        key !== 'nextContainer' &&
        key !== 'parseDiagnostics' &&
        key !== 'bindDiagnostics' &&
        key !== 'lineMap' &&
        key !== 'flowNode' &&
        key !== 'endFlowNode' &&
        key !== 'jsDocCache' &&
        key !== 'jsDoc' &&
        key !== 'symbol'
      );
    case 'tsType':
      return (
        key !== 'checker' &&
        key !== 'constructSignatures' &&
        key !== 'callSignatures'
      );
    case 'tsSignature':
      return key !== 'checker';
  }

  return true;
}
```
</details>

- **Parameters**:
  - `key: string`
  - `value: unknown`
  - `type: ParentNodeType`
  - `showTokens: boolean`
- **Return Type**: `boolean`
- **Calls**:
  - `key.startsWith`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish -- I don't know whether this is safe to fix (x4)
```


---