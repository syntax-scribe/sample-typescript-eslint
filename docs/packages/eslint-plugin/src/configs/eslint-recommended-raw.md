[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `eslint-recommended-raw.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
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

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/configs/eslint-recommended-raw.ts`**

## Functions

### `config(style: 'glob' | 'minimatch'): {
  files: string[];
  rules: Record<string, 'error' | 'off' | 'warn'>;
}`

<details><summary>Code</summary>

```ts
(
  style: 'glob' | 'minimatch',
): {
  files: string[];
  rules: Record<string, 'error' | 'off' | 'warn'>;
} => ({
  files:
    style === 'glob'
      ? // classic configs use glob syntax
        ['*.ts', '*.tsx', '*.mts', '*.cts']
      : // flat configs use minimatch syntax
        ['**/*.ts', '**/*.tsx', '**/*.mts', '**/*.cts'],
  rules: {
    'constructor-super': 'off', // ts(2335) & ts(2377)
    'getter-return': 'off', // ts(2378)
    'no-class-assign': 'off', // ts(2629)
    'no-const-assign': 'off', // ts(2588)
    'no-dupe-args': 'off', // ts(2300)
    'no-dupe-class-members': 'off', // ts(2393) & ts(2300)
    'no-dupe-keys': 'off', // ts(1117)
    'no-func-assign': 'off', // ts(2630)
    'no-import-assign': 'off', // ts(2632) & ts(2540)
    // TODO - remove this once we no longer support ESLint v8
    'no-new-native-nonconstructor': 'off', // ts(7009)
    'no-new-symbol': 'off', // ts(7009)
    'no-obj-calls': 'off', // ts(2349)
    'no-redeclare': 'off', // ts(2451)
    'no-setter-return': 'off', // ts(2408)
    'no-this-before-super': 'off', // ts(2376) & ts(17009)
    'no-undef': 'off', // ts(2304) & ts(2552)
    'no-unreachable': 'off', // ts(7027)
    'no-unsafe-negation': 'off', // ts(2365) & ts(2322) & ts(2358)
    'no-var': 'error', // ts transpiles let/const to var, so no need for vars any more
    'no-with': 'off', // ts(1101) & ts(2410)
    'prefer-const': 'error', // ts provides better types with const
    'prefer-rest-params': 'error', // ts provides better types with rest args over arguments
    'prefer-spread': 'error', // ts transpiles spread to apply, so no need for manual apply
  },
})
```
</details>

- **Parameters**:
  - `style: 'glob' | 'minimatch'`
- **Return Type**: `{
  files: string[];
  rules: Record<string, 'error' | 'off' | 'warn'>;
}`

---