[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `utils.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 7 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 6 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/linter/utils.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `Monaco` | `monaco-editor` |
| `ErrorGroup` | `../types` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `result` | `Record<string, ErrorGroup>` | const | `{}` | ✗ |
| `fixers` | `{ fix(): void; isPreferred: boolean; message: string; }[]` | const | `fixes.get(uri)?.map(item => ({
        fix(): void {
          const model = editor.getModel();
          if (model) {
            editor.executeEdits('eslint', [createEditOperation(model, item)]);
          }
        },
        isPreferred: item.isPreferred,
        message: item.message,
      })) ?? []` | ✗ |
| `group` | `any` | const | `marker.owner === 'eslint'
        ? code.value
        : marker.owner === 'typescript'
          ? 'TypeScript'
          : marker.owner` | ✗ |
| `markers` | `Monaco.editor.IMarkerData[]` | const | `[]` | ✗ |
| `marker` | `Monaco.editor.IMarkerData` | const | `{
      code: message.ruleId
        ? {
            target: ruleUri(message.ruleId),
            value: message.ruleId,
          }
        : 'Internal error',
      endColumn,
      endLineNumber,
      message: message.message,
      severity:
        message.severity === 2
          ? 8 // MarkerSeverity.Error
          : 4, // MarkerSeverity.Warning
      source: 'ESLint',
      startColumn,
      startLineNumber,
    }` | ✗ |
| `fixes` | `LintCodeAction[]` | const | `[]` | ✗ |


---

## Functions

### `ensurePositiveInt(value: number | undefined, defaultValue: number): number`

<details><summary>Code</summary>

```ts
export function ensurePositiveInt(
  value: number | undefined,
  defaultValue: number,
): number {
  return Math.max(1, (value ?? defaultValue) | 0);
}
```
</details>

- **Parameters**:
  - `value: number | undefined`
  - `defaultValue: number`
- **Return Type**: `number`
- **Calls**:
  - `Math.max`
### `createURI(marker: Monaco.editor.IMarkerData): string`

<details><summary>Code</summary>

```ts
export function createURI(marker: Monaco.editor.IMarkerData): string {
  return `[${[
    marker.startLineNumber,
    marker.startColumn,
    marker.startColumn,
    marker.endLineNumber,
    marker.endColumn,
    (typeof marker.code === 'string' ? marker.code : marker.code?.value) ?? '',
  ].join('|')}]`;
}
```
</details>

- **Parameters**:
  - `marker: Monaco.editor.IMarkerData`
- **Return Type**: `string`
- **Calls**:
  - `[
    marker.startLineNumber,
    marker.startColumn,
    marker.startColumn,
    marker.endLineNumber,
    marker.endColumn,
    (typeof marker.code === 'string' ? marker.code : marker.code?.value) ?? '',
  ].join`
### `createEditOperation(model: Monaco.editor.ITextModel, action: LintCodeAction): { range: Monaco.IRange; text: string }`

<details><summary>Code</summary>

```ts
export function createEditOperation(
  model: Monaco.editor.ITextModel,
  action: LintCodeAction,
): { range: Monaco.IRange; text: string } {
  const start = model.getPositionAt(action.fix.range[0]);
  const end = model.getPositionAt(action.fix.range[1]);
  return {
    range: {
      endColumn: end.column,
      endLineNumber: end.lineNumber,
      startColumn: start.column,
      startLineNumber: start.lineNumber,
    },
    text: action.fix.text,
  };
}
```
</details>

- **Parameters**:
  - `model: Monaco.editor.ITextModel`
  - `action: LintCodeAction`
- **Return Type**: `{ range: Monaco.IRange; text: string }`
- **Calls**:
  - `model.getPositionAt`
### `normalizeCode(code: Monaco.editor.IMarker['code']): {
  target?: string;
  value: string;
}`

<details><summary>Code</summary>

```ts
function normalizeCode(code: Monaco.editor.IMarker['code']): {
  target?: string;
  value: string;
} {
  if (!code) {
    return { value: '' };
  }
  if (typeof code === 'string') {
    return { value: code };
  }
  return {
    target: code.target.toString(),
    value: code.value,
  };
}
```
</details>

- **Parameters**:
  - `code: Monaco.editor.IMarker['code']`
- **Return Type**: `{
  target?: string;
  value: string;
}`
- **Calls**:
  - `code.target.toString`
### `parseMarkers(markers: Monaco.editor.IMarker[], fixes: Map<string, LintCodeAction[]>, editor: Monaco.editor.IStandaloneCodeEditor): ErrorGroup[]`

<details><summary>Code</summary>

```ts
export function parseMarkers(
  markers: Monaco.editor.IMarker[],
  fixes: Map<string, LintCodeAction[]>,
  editor: Monaco.editor.IStandaloneCodeEditor,
): ErrorGroup[] {
  const result: Record<string, ErrorGroup> = {};
  for (const marker of markers) {
    const code = normalizeCode(marker.code);
    const uri = createURI(marker);

    const fixers =
      fixes.get(uri)?.map(item => ({
        fix(): void {
          const model = editor.getModel();
          if (model) {
            editor.executeEdits('eslint', [createEditOperation(model, item)]);
          }
        },
        isPreferred: item.isPreferred,
        message: item.message,
      })) ?? [];

    const group =
      marker.owner === 'eslint'
        ? code.value
        : marker.owner === 'typescript'
          ? 'TypeScript'
          : marker.owner;

    // eslint-disable-next-line @typescript-eslint/no-unnecessary-condition
    result[group] ||= {
      group,
      items: [],
      uri: code.target,
    };

    result[group].items.push({
      fixer: fixers.find(item => item.isPreferred),
      location: `${marker.startLineNumber}:${marker.startColumn} - ${marker.endLineNumber}:${marker.endColumn}`,
      message:
        (marker.owner !== 'eslint' && marker.owner !== 'json' && code.value
          ? `${code.value}: `
          : '') + marker.message,
      severity: marker.severity,
      suggestions: fixers.filter(item => !item.isPreferred),
    });
  }

  return Object.values(result).sort((a, b) => a.group.localeCompare(b.group));
}
```
</details>

- **Parameters**:
  - `markers: Monaco.editor.IMarker[]`
  - `fixes: Map<string, LintCodeAction[]>`
  - `editor: Monaco.editor.IStandaloneCodeEditor`
- **Return Type**: `ErrorGroup[]`
- **Calls**:
  - `normalizeCode`
  - `createURI`
  - `fixes.get(uri)?.map`
  - `editor.getModel`
  - `editor.executeEdits`
  - `createEditOperation`
  - `result[group].items.push`
  - `fixers.find`
  - `fixers.filter`
  - `Object.values(result).sort`
  - `a.group.localeCompare`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-unnecessary-condition (x4)
```

### `parseLintResults(messages: TSESLint.Linter.LintMessage[], codeActions: Map<string, LintCodeAction[]>, ruleUri: (ruleId: string) => Monaco.Uri): Monaco.editor.IMarkerData[]`

<details><summary>Code</summary>

```ts
export function parseLintResults(
  messages: TSESLint.Linter.LintMessage[],
  codeActions: Map<string, LintCodeAction[]>,
  ruleUri: (ruleId: string) => Monaco.Uri,
): Monaco.editor.IMarkerData[] {
  const markers: Monaco.editor.IMarkerData[] = [];

  codeActions.clear();

  for (const message of messages) {
    const startLineNumber = ensurePositiveInt(message.line, 1);
    const startColumn = ensurePositiveInt(message.column, 1);
    const endLineNumber = ensurePositiveInt(message.endLine, startLineNumber);
    const endColumn = ensurePositiveInt(message.endColumn, startColumn + 1);

    const marker: Monaco.editor.IMarkerData = {
      code: message.ruleId
        ? {
            target: ruleUri(message.ruleId),
            value: message.ruleId,
          }
        : 'Internal error',
      endColumn,
      endLineNumber,
      message: message.message,
      severity:
        message.severity === 2
          ? 8 // MarkerSeverity.Error
          : 4, // MarkerSeverity.Warning
      source: 'ESLint',
      startColumn,
      startLineNumber,
    };
    const markerUri = createURI(marker);

    const fixes: LintCodeAction[] = [];
    if (message.fix) {
      fixes.push({
        fix: message.fix,
        isPreferred: true,
        message: `Fix this ${message.ruleId ?? 'unknown'} problem`,
      });
    }
    if (message.suggestions) {
      for (const suggestion of message.suggestions) {
        fixes.push({
          code: message.ruleId,
          fix: suggestion.fix,
          isPreferred: false,
          message: suggestion.desc,
        });
      }
    }
    if (fixes.length > 0) {
      codeActions.set(markerUri, fixes);
    }

    markers.push(marker);
  }

  return markers;
}
```
</details>

- **Parameters**:
  - `messages: TSESLint.Linter.LintMessage[]`
  - `codeActions: Map<string, LintCodeAction[]>`
  - `ruleUri: (ruleId: string) => Monaco.Uri`
- **Return Type**: `Monaco.editor.IMarkerData[]`
- **Calls**:
  - `codeActions.clear`
  - `ensurePositiveInt`
  - `ruleUri`
  - `createURI`
  - `fixes.push`
  - `codeActions.set`
  - `markers.push`
### `getPathRegExp(path: string): RegExp`

<details><summary>Code</summary>

```ts
export function getPathRegExp(path: string): RegExp {
  const escapedPath = path.replaceAll('.', '\\.').replaceAll('*', '[^/]+');
  return new RegExp(`^${escapedPath}$`, '');
}
```
</details>

- **Parameters**:
  - `path: string`
- **Return Type**: `RegExp`
- **Calls**:
  - `path.replaceAll('.', '\\.').replaceAll`

---

## Interfaces

### `LintCodeAction`

<details><summary>Interface Code</summary>

```ts
export interface LintCodeAction {
  code?: string | null;
  fix: {
    range: Readonly<[number, number]>;
    text: string;
  };
  isPreferred: boolean;
  message: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `code` | `string | null` | ✓ |  |
| `fix` | `{
    range: Readonly<[number, number]>;
    text: string;
  }` | ✗ |  |
| `isPreferred` | `boolean` | ✗ |  |
| `message` | `string` | ✗ |  |


---