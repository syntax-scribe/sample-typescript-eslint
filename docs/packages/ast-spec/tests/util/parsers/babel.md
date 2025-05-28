[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `babel.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 2 |
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
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/util/parsers/babel.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserOptions` | `@babel/core` |
| `parse` | `@babel/eslint-parser` |
| `Fixture` | `./parser-types.js` |
| `ParserResponse` | `./parser-types.js` |
| `ParserResponseType` | `./parser-types.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `PLUGINS` | `NonNullable<ParserOptions['plugins']>` | const | `[
  'decoratorAutoAccessors',
  // TODO - enable classFeatures instead of classProperties when we support it
  // 'classFeatures',
  'classProperties',
  'decorators-legacy',
  'explicitResourceManagement',
  'importAssertions',
  'typescript',
]` | ✗ |
| `plugins` | `any[]` | const | `[...PLUGINS]` | ✗ |


---

## Functions

### `parseBabel(fixture: Pick<Fixture, 'contents' | 'isJSX'>): ParserResponse`

<details><summary>Code</summary>

```ts
export function parseBabel(
  fixture: Pick<Fixture, 'contents' | 'isJSX'>,
): ParserResponse {
  const plugins = [...PLUGINS];
  if (fixture.isJSX) {
    plugins.push('jsx');
  }

  try {
    const result = parse(fixture.contents, {
      allowImportExportEverywhere: true,
      babelOptions: {
        parserOpts: {
          plugins,
        },
      },
      ecmaFeatures: {
        globalReturn: true,
      },
      requireConfigFile: false,
      sourceType: 'unambiguous',
    });
    const { comments: __, tokens, ...ast } = result;

    return {
      ast,
      error: 'NO ERROR',
      tokens,
      type: ParserResponseType.NoError,
    };
  } catch (error: unknown) {
    return {
      error,
      type: ParserResponseType.Error,
    };
  }
}
```
</details>

- **Parameters**:
  - `fixture: Pick<Fixture, 'contents' | 'isJSX'>`
- **Return Type**: `ParserResponse`
- **Calls**:
  - `plugins.push`
  - `parse (from @babel/eslint-parser)`

---