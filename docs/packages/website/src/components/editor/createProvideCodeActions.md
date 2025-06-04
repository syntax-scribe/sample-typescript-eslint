[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `createProvideCodeActions.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/components/editor/createProvideCodeActions.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Monaco` | `monaco-editor` |
| `LintCodeAction` | `../linter/utils` |
| `createEditOperation` | `../linter/utils` |
| `createURI` | `../linter/utils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `actions` | `Monaco.languages.CodeAction[]` | const | `[]` | ✗ |
| `messages` | `LintCodeAction[]` | const | `fixes.get(createURI(marker)) ?? []` | ✗ |


---

## Functions

### `createProvideCodeActions(fixes: Map<string, LintCodeAction[]>): Monaco.languages.CodeActionProvider`

<details><summary>Code</summary>

```ts
export function createProvideCodeActions(
  fixes: Map<string, LintCodeAction[]>,
): Monaco.languages.CodeActionProvider {
  return {
    provideCodeActions(
      model,
      _range,
      context,
    ): Monaco.languages.ProviderResult<Monaco.languages.CodeActionList> {
      if (context.only !== 'quickfix') {
        return {
          actions: [],
          dispose(): void {
            /* nop */
          },
        };
      }
      const actions: Monaco.languages.CodeAction[] = [];
      for (const marker of context.markers) {
        const messages = fixes.get(createURI(marker)) ?? [];
        for (const message of messages) {
          const editOperation = createEditOperation(model, message);
          actions.push({
            diagnostics: [marker],
            edit: {
              edits: [
                {
                  resource: model.uri,
                  // monaco for ts >= 4.8
                  textEdit: editOperation,
                  // @ts-expect-error monaco for ts < 4.8
                  edit: editOperation,
                },
              ],
            },
            isPreferred: message.isPreferred,
            kind: 'quickfix',
            title: message.message + (message.code ? ` (${message.code})` : ''),
          });
        }
      }
      return {
        actions,
        dispose(): void {
          /* nop */
        },
      };
    },
  };
}
```
</details>

- **Parameters**:
  - `fixes: Map<string, LintCodeAction[]>`
- **Return Type**: `Monaco.languages.CodeActionProvider`
- **Calls**:
  - `fixes.get`
  - `createURI (from ../linter/utils)`
  - `createEditOperation (from ../linter/utils)`
  - `actions.push`
- **Internal Comments**:
```
// monaco for ts >= 4.8 (x2)
// @ts-expect-error monaco for ts < 4.8 (x2)
```


---