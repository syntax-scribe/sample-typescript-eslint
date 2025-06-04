[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `esnext.disposable.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 6 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/lib/esnext.disposable.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `LibDefinition` | `../variable` |
| `TYPE` | `./base-config` |
| `TYPE_VALUE` | `./base-config` |
| `es2015_iterable` | `./es2015.iterable` |
| `es2015_symbol` | `./es2015.symbol` |
| `es2018_asynciterable` | `./es2018.asynciterable` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `esnext_disposable` | `LibDefinition` | const | `{
  libs: [es2015_symbol, es2015_iterable, es2018_asynciterable],
  variables: [
    ['SymbolConstructor', TYPE],
    ['Disposable', TYPE],
    ['AsyncDisposable', TYPE],
    ['SuppressedError', TYPE_VALUE],
    ['SuppressedErrorConstructor', TYPE],
    ['DisposableStack', TYPE_VALUE],
    ['DisposableStackConstructor', TYPE],
    ['AsyncDisposableStack', TYPE_VALUE],
    ['AsyncDisposableStackConstructor', TYPE],
    ['IteratorObject', TYPE],
    ['AsyncIteratorObject', TYPE],
  ],
}` | ✓ |


---