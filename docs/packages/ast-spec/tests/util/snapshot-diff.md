[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `snapshot-diff.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/util/snapshot-diff.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `format` | `@vitest/pretty-format` |
| `diff` | `@vitest/utils/diff` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `NO_DIFF_MESSAGE` | `"Compared values have no visual difference."` | const | `'Compared values have no visual difference.'` | ✗ |
| `OPTIONS` | `{ plugins: any[]; }` | const | `{
    plugins: [
      NodeSerializer.serializer,
      // by default vitest will quote the string with double quotes
      // this means the diff string will have double quotes escaped and look ugly
      // this is a single-quote string serializer which won't clash with the outer double quotes
      // so we get a nicer looking diff because of it!
      StringSerializer.serializer,
    ],
  }` | ✗ |


---

## Functions

### `identity(value: T): T`

<details><summary>Code</summary>

```ts
function identity<T>(value: T): T {
  return value;
}
```
</details>

- **Parameters**:
  - `value: T`
- **Return Type**: `T`
### `diffStrings(valueA: unknown, valueB: unknown, valueAName: string, valueBName: string): string | undefined`

<details><summary>Code</summary>

```ts
function diffStrings(
  valueA: unknown,
  valueB: unknown,
  valueAName: string,
  valueBName: string,
): string | undefined {
  if (Object.is(valueA, valueB)) {
    return NO_DIFF_MESSAGE;
  }

  return diff(valueA, valueB, {
    expand: false,
    // we want to show the entire file in the diff
    // that way you don't have to try and figure out what lines map to which sections
    aAnnotation: valueAName,
    aColor: identity,
    bAnnotation: valueBName,
    bColor: identity,
    changeColor: identity,
    commonColor: identity,
    contextLines: Number.MAX_SAFE_INTEGER,
    patchColor: identity,
  });
}
```
</details>

- **Parameters**:
  - `valueA: unknown`
  - `valueB: unknown`
  - `valueAName: string`
  - `valueBName: string`
- **Return Type**: `string | undefined`
- **Calls**:
  - `Object.is`
  - `diff (from @vitest/utils/diff)`
- **Internal Comments**:
```
// we want to show the entire file in the diff (x2)
// that way you don't have to try and figure out what lines map to which sections (x2)
```

### `snapshotDiff(valueAName: string, valueA: unknown, valueBName: string, valueB: unknown): string`

<details><summary>Code</summary>

```ts
export function snapshotDiff(
  valueAName: string,
  valueA: unknown,
  valueBName: string,
  valueB: unknown,
): string {
  const OPTIONS = {
    plugins: [
      NodeSerializer.serializer,
      // by default vitest will quote the string with double quotes
      // this means the diff string will have double quotes escaped and look ugly
      // this is a single-quote string serializer which won't clash with the outer double quotes
      // so we get a nicer looking diff because of it!
      StringSerializer.serializer,
    ],
  };

  const difference = diffStrings(
    format(valueA, OPTIONS),
    format(valueB, OPTIONS),
    valueAName,
    valueBName,
  );

  if (difference == null) {
    throw new Error('Unexpected null when diffing snapshots.');
  }

  return `Snapshot Diff:\n${difference}`;
}
```
</details>

- **Parameters**:
  - `valueAName: string`
  - `valueA: unknown`
  - `valueBName: string`
  - `valueB: unknown`
- **Return Type**: `string`
- **Calls**:
  - `diffStrings`
  - `format (from @vitest/pretty-format)`
- **Internal Comments**:
```
// by default vitest will quote the string with double quotes (x2)
// this means the diff string will have double quotes escaped and look ugly (x2)
// this is a single-quote string serializer which won't clash with the outer double quotes (x2)
// so we get a nicer looking diff because of it! (x2)
```

### `diffHasChanges(diff: string): boolean`

<details><summary>Code</summary>

```ts
export function diffHasChanges(diff: string): boolean {
  return !diff.includes(NO_DIFF_MESSAGE);
}
```
</details>

- **Parameters**:
  - `diff: string`
- **Return Type**: `boolean`
- **Calls**:
  - `diff.includes`

---