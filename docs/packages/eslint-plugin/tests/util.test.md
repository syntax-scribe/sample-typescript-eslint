[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `util.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/util.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `isDefinitionFile` | `../src/util` |
| `upperCaseFirst` | `../src/util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `invalid` | `readonly ["test.js", "test.jsx", "README.md", "test.d.js", "test.ts.js", "test.ts.map", "test.ts-js", "test.ts", "ts", "test.tsx", "test.TS", "test.TSX", "test.d.tsx", "test.D.TSX"]` | const | `[
      'test.js',
      'test.jsx',
      'README.md',
      'test.d.js',
      'test.ts.js',
      'test.ts.map',
      'test.ts-js',
      'test.ts',
      'ts',
      'test.tsx',
      'test.TS',
      'test.TSX',
      // yes, it's not a definition file if it's a `.d.tsx`!
      'test.d.tsx',
      'test.D.TSX',
    ] as const` | ✗ |
| `valid` | `readonly ["test.d.ts", "test.D.TS"]` | const | `['test.d.ts', 'test.D.TS'] as const` | ✗ |


---