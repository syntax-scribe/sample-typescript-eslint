[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `tsUtils.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 📊 Variables & Constants | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/ast/tsUtils.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `result` | `Record<number, string>` | const | `{}` | ✗ |
| `tsEnumCache` | `TsParsedEnums | undefined` | let/var | `*not shown*` | ✗ |


---

## Functions

### `extractEnum(obj: Record<number, number | string>): Record<number, string>`

<details><summary>Code</summary>

```ts
export function extractEnum(
  obj: Record<number, number | string>,
): Record<number, string> {
  const result: Record<number, string> = {};
  const keys = Object.entries(obj);
  for (const [name, value] of keys) {
    if (typeof value === 'number' && !(value in result)) {
      result[value] = name;
    }
  }
  return result;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Extract the enum values from the TypeScript enum.
 * typescript enum's have duplicates, and we always want to take first one.
 * e.g. SyntaxKind.EqualsToken = 63, SyntaxKind.FirstAssignment = 63
 */
```

- **Parameters**:
  - `obj: Record<number, number | string>`
- **Return Type**: `Record<number, string>`
- **Calls**:
  - `Object.entries`
### `getTsEnum(type: keyof TsParsedEnums): Record<number, string>`

<details><summary>Code</summary>

```ts
function getTsEnum(type: keyof TsParsedEnums): Record<number, string> {
  tsEnumCache ??= {
    LanguageVariant: extractEnum(window.ts.LanguageVariant),
    ModifierFlags: extractEnum(window.ts.ModifierFlags),
    NodeFlags: extractEnum(window.ts.NodeFlags),
    ObjectFlags: extractEnum(window.ts.ObjectFlags),
    ScriptKind: extractEnum(window.ts.ScriptKind),
    ScriptTarget: extractEnum(window.ts.ScriptTarget),
    SymbolFlags: extractEnum(window.ts.SymbolFlags),
    SyntaxKind: extractEnum(window.ts.SyntaxKind),
    TokenFlags: extractEnum(window.ts.TokenFlags),
    TypeFlags: extractEnum(window.ts.TypeFlags),
    // @ts-expect-error: non public API
    // eslint-disable-next-line @typescript-eslint/no-unsafe-argument
    TransformFlags: extractEnum(window.ts.TransformFlags),
  };
  return tsEnumCache[type];
}
```
</details>

- **JSDoc**:
```ts
/**
 * Get the TypeScript enum values.
 */
```

- **Parameters**:
  - `type: keyof TsParsedEnums`
- **Return Type**: `Record<number, string>`
- **Calls**:
  - `extractEnum`
- **Internal Comments**:
```
// @ts-expect-error: non public API (x2)
// eslint-disable-next-line @typescript-eslint/no-unsafe-argument (x2)
```

### `tsEnumToString(type: keyof TsParsedEnums, value: number): string | undefined`

<details><summary>Code</summary>

```ts
export function tsEnumToString(
  type: keyof TsParsedEnums,
  value: number,
): string | undefined {
  return getTsEnum(type)[value];
}
```
</details>

- **JSDoc**:
```ts
/**
 * Convert a TypeScript enum value to a string.
 */
```

- **Parameters**:
  - `type: keyof TsParsedEnums`
  - `value: number`
- **Return Type**: `string | undefined`
- **Calls**:
  - `getTsEnum`
### `tsEnumFlagToString(type: keyof TsParsedEnums, value: number): string | undefined`

<details><summary>Code</summary>

```ts
export function tsEnumFlagToString(
  type: keyof TsParsedEnums,
  value: number,
): string | undefined {
  return Object.entries(getTsEnum(type))
    .filter(([f]) => (Number(f) & value) !== 0)
    .map(([, name]) => `${type}.${name}`)
    .join('\n');
}
```
</details>

- **JSDoc**:
```ts
/**
 * Convert a TypeScript enum flag value to a concatenated string of the flags.
 */
```

- **Parameters**:
  - `type: keyof TsParsedEnums`
  - `value: number`
- **Return Type**: `string | undefined`
- **Calls**:
  - `Object.entries(getTsEnum(type))
    .filter(([f]) => (Number(f) & value) !== 0)
    .map(([, name]) => `${type}.${name}`)
    .join`

---

## Interfaces

### `TsParsedEnums`

<details><summary>Interface Code</summary>

```ts
interface TsParsedEnums {
  LanguageVariant: Record<number, string>;
  ModifierFlags: Record<number, string>;
  NodeFlags: Record<number, string>;
  ObjectFlags: Record<number, string>;
  ScriptKind: Record<number, string>;
  ScriptTarget: Record<number, string>;
  SymbolFlags: Record<number, string>;
  SyntaxKind: Record<number, string>;
  TokenFlags: Record<number, string>;
  TransformFlags: Record<number, string>;
  TypeFlags: Record<number, string>;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `LanguageVariant` | `Record<number, string>` | ✗ |  |
| `ModifierFlags` | `Record<number, string>` | ✗ |  |
| `NodeFlags` | `Record<number, string>` | ✗ |  |
| `ObjectFlags` | `Record<number, string>` | ✗ |  |
| `ScriptKind` | `Record<number, string>` | ✗ |  |
| `ScriptTarget` | `Record<number, string>` | ✗ |  |
| `SymbolFlags` | `Record<number, string>` | ✗ |  |
| `SyntaxKind` | `Record<number, string>` | ✗ |  |
| `TokenFlags` | `Record<number, string>` | ✗ |  |
| `TransformFlags` | `Record<number, string>` | ✗ |  |
| `TypeFlags` | `Record<number, string>` | ✗ |  |


---