[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `createProvideTwoslashInlay.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 5 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 8 |
| ⚡ Async/Await Patterns | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Async/Await Patterns](#asyncawait-patterns)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/components/editor/createProvideTwoslashInlay.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Monaco` | `monaco-editor` |
| `SandboxInstance` | `./useSandboxServices` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `match` | `RegExpExecArray | null` | let/var | `null` | ✗ |
| `matches` | `RegExpExecArray[]` | const | `[]` | ✗ |
| `twoslashQueryRegex` | `RegExp` | const | `/^(\s*\/\/\s*\^\?)\s*$/gm` | ✗ |
| `worker` | `TypeScriptWorker` | let/var | `await sandbox.getWorkerProcess()` | ✗ |
| `results` | `Monaco.languages.InlayHint[]` | let/var | `[]` | ✗ |
| `end` | `number` | let/var | `queryMatch.index + queryMatch[1].length - 1` | ✗ |
| `inspectionPos` | `any` | let/var | `new sandbox.monaco.Position(
          endPos.lineNumber - 1,
          endPos.column,
        )` | ✗ |
| `hint` | `any` | let/var | `await (worker.getQuickInfoAtPosition(
          `file://${model.uri.path}`,
          inspectionOff,
        ) as Promise<ts.QuickInfo | undefined>)` | ✗ |


---

## Async/Await Patterns

| Type | Function | Await Expressions | Promise Chains |
|------|----------|-------------------|----------------|
| promise-chain | `createTwoslashInlayProvider` | *none* | Promise.all |
| await-expression | `createTwoslashInlayProvider` | sandbox.getWorkerProcess(), Promise.all(
        queryMatches.map(q => resolveInlayHint(q)),
      ), (worker.getQuickInfoAtPosition(
          `file://${model.uri.path}`,
          inspectionOff,
        ) as Promise<ts.QuickInfo | undefined>) | *none* |
| async-function | `resolveInlayHint` | (worker.getQuickInfoAtPosition(
          `file://${model.uri.path}`,
          inspectionOff,
        ) as Promise<ts.QuickInfo | undefined>) | *none* |


---

## Functions

### `findTwoshashQueries(code: string): RegExpExecArray[]`

<details><summary>Code</summary>

```ts
function findTwoshashQueries(code: string): RegExpExecArray[] {
  let match: RegExpExecArray | null = null;
  const matches: RegExpExecArray[] = [];
  // RegExp that matches '^<spaces>//?<spaces>$'
  const twoslashQueryRegex = /^(\s*\/\/\s*\^\?)\s*$/gm;
  while ((match = twoslashQueryRegex.exec(code))) {
    matches.push(match);
  }
  return matches;
}
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `RegExpExecArray[]`
- **Calls**:
  - `twoslashQueryRegex.exec`
  - `matches.push`
- **Internal Comments**:
```
// RegExp that matches '^<spaces>//?<spaces>$' (x2)
```

### `createTwoslashInlayProvider(sandbox: SandboxInstance): Monaco.languages.InlayHintsProvider`

<details><summary>Code</summary>

```ts
export function createTwoslashInlayProvider(
  sandbox: SandboxInstance,
): Monaco.languages.InlayHintsProvider {
  return {
    provideInlayHints: async (
      model,
      _,
      cancel,
    ): Promise<Monaco.languages.InlayHintList> => {
      const worker = await sandbox.getWorkerProcess();
      if (model.isDisposed() || cancel.isCancellationRequested) {
        return {
          dispose(): void {
            /* nop */
          },
          hints: [],
        };
      }

      const queryMatches = findTwoshashQueries(model.getValue());

      const results: Monaco.languages.InlayHint[] = [];

      for (const result of await Promise.all(
        queryMatches.map(q => resolveInlayHint(q)),
      )) {
        if (result) {
          results.push(result);
        }
      }

      return {
        dispose(): void {
          /* nop */
        },
        hints: results,
      };

      async function resolveInlayHint(
        queryMatch: RegExpExecArray,
      ): Promise<Monaco.languages.InlayHint | undefined> {
        const end = queryMatch.index + queryMatch[1].length - 1;
        const endPos = model.getPositionAt(end);
        const inspectionPos = new sandbox.monaco.Position(
          endPos.lineNumber - 1,
          endPos.column,
        );
        const inspectionOff = model.getOffsetAt(inspectionPos);

        const hint = await (worker.getQuickInfoAtPosition(
          `file://${model.uri.path}`,
          inspectionOff,
        ) as Promise<ts.QuickInfo | undefined>);
        if (!hint?.displayParts) {
          return;
        }

        let text = hint.displayParts
          .map(d => d.text)
          .join('')
          .replaceAll(/\r?\n\s*/g, ' ');
        if (text.length > 120) {
          text = `${text.slice(0, 119)}...`;
        }

        return {
          kind: sandbox.monaco.languages.InlayHintKind.Type,
          label: text,
          paddingLeft: true,
          position: new sandbox.monaco.Position(
            endPos.lineNumber,
            endPos.column + 1,
          ),
        };
      }
    },
  };
}
```
</details>

- **Parameters**:
  - `sandbox: SandboxInstance`
- **Return Type**: `Monaco.languages.InlayHintsProvider`
- **Calls**:
  - `sandbox.getWorkerProcess`
  - `model.isDisposed`
  - `findTwoshashQueries`
  - `model.getValue`
  - `Promise.all`
  - `queryMatches.map`
  - `resolveInlayHint`
  - `results.push`
  - `model.getPositionAt`
  - `model.getOffsetAt`
  - `worker.getQuickInfoAtPosition`
  - `hint.displayParts
          .map(d => d.text)
          .join('')
          .replaceAll`
  - `text.slice`
### `provideInlayHints(model: any, _: any, cancel: any): Promise<Monaco.languages.InlayHintList>`

<details><summary>Code</summary>

```ts
async (
      model,
      _,
      cancel,
    ): Promise<Monaco.languages.InlayHintList> => {
      const worker = await sandbox.getWorkerProcess();
      if (model.isDisposed() || cancel.isCancellationRequested) {
        return {
          dispose(): void {
            /* nop */
          },
          hints: [],
        };
      }

      const queryMatches = findTwoshashQueries(model.getValue());

      const results: Monaco.languages.InlayHint[] = [];

      for (const result of await Promise.all(
        queryMatches.map(q => resolveInlayHint(q)),
      )) {
        if (result) {
          results.push(result);
        }
      }

      return {
        dispose(): void {
          /* nop */
        },
        hints: results,
      };

      async function resolveInlayHint(
        queryMatch: RegExpExecArray,
      ): Promise<Monaco.languages.InlayHint | undefined> {
        const end = queryMatch.index + queryMatch[1].length - 1;
        const endPos = model.getPositionAt(end);
        const inspectionPos = new sandbox.monaco.Position(
          endPos.lineNumber - 1,
          endPos.column,
        );
        const inspectionOff = model.getOffsetAt(inspectionPos);

        const hint = await (worker.getQuickInfoAtPosition(
          `file://${model.uri.path}`,
          inspectionOff,
        ) as Promise<ts.QuickInfo | undefined>);
        if (!hint?.displayParts) {
          return;
        }

        let text = hint.displayParts
          .map(d => d.text)
          .join('')
          .replaceAll(/\r?\n\s*/g, ' ');
        if (text.length > 120) {
          text = `${text.slice(0, 119)}...`;
        }

        return {
          kind: sandbox.monaco.languages.InlayHintKind.Type,
          label: text,
          paddingLeft: true,
          position: new sandbox.monaco.Position(
            endPos.lineNumber,
            endPos.column + 1,
          ),
        };
      }
    }
```
</details>

- **Parameters**:
  - `model: any`
  - `_: any`
  - `cancel: any`
- **Return Type**: `Promise<Monaco.languages.InlayHintList>`
- **Calls**:
  - `sandbox.getWorkerProcess`
  - `model.isDisposed`
  - `findTwoshashQueries`
  - `model.getValue`
  - `Promise.all`
  - `queryMatches.map`
  - `resolveInlayHint`
  - `results.push`
  - `model.getPositionAt`
  - `model.getOffsetAt`
  - `worker.getQuickInfoAtPosition`
  - `hint.displayParts
          .map(d => d.text)
          .join('')
          .replaceAll`
  - `text.slice`
### `resolveInlayHint(queryMatch: RegExpExecArray): Promise<Monaco.languages.InlayHint | undefined>`

<details><summary>Code</summary>

```ts
async function resolveInlayHint(
        queryMatch: RegExpExecArray,
      ): Promise<Monaco.languages.InlayHint | undefined> {
        const end = queryMatch.index + queryMatch[1].length - 1;
        const endPos = model.getPositionAt(end);
        const inspectionPos = new sandbox.monaco.Position(
          endPos.lineNumber - 1,
          endPos.column,
        );
        const inspectionOff = model.getOffsetAt(inspectionPos);

        const hint = await (worker.getQuickInfoAtPosition(
          `file://${model.uri.path}`,
          inspectionOff,
        ) as Promise<ts.QuickInfo | undefined>);
        if (!hint?.displayParts) {
          return;
        }

        let text = hint.displayParts
          .map(d => d.text)
          .join('')
          .replaceAll(/\r?\n\s*/g, ' ');
        if (text.length > 120) {
          text = `${text.slice(0, 119)}...`;
        }

        return {
          kind: sandbox.monaco.languages.InlayHintKind.Type,
          label: text,
          paddingLeft: true,
          position: new sandbox.monaco.Position(
            endPos.lineNumber,
            endPos.column + 1,
          ),
        };
      }
```
</details>

- **Parameters**:
  - `queryMatch: RegExpExecArray`
- **Return Type**: `Promise<Monaco.languages.InlayHint | undefined>`
- **Calls**:
  - `model.getPositionAt`
  - `model.getOffsetAt`
  - `worker.getQuickInfoAtPosition`
  - `hint.displayParts
          .map(d => d.text)
          .join('')
          .replaceAll`
  - `text.slice`
### `provideInlayHints(model: any, _: any, cancel: any): Promise<Monaco.languages.InlayHintList>`

<details><summary>Code</summary>

```ts
async (
      model,
      _,
      cancel,
    ): Promise<Monaco.languages.InlayHintList> => {
      const worker = await sandbox.getWorkerProcess();
      if (model.isDisposed() || cancel.isCancellationRequested) {
        return {
          dispose(): void {
            /* nop */
          },
          hints: [],
        };
      }

      const queryMatches = findTwoshashQueries(model.getValue());

      const results: Monaco.languages.InlayHint[] = [];

      for (const result of await Promise.all(
        queryMatches.map(q => resolveInlayHint(q)),
      )) {
        if (result) {
          results.push(result);
        }
      }

      return {
        dispose(): void {
          /* nop */
        },
        hints: results,
      };

      async function resolveInlayHint(
        queryMatch: RegExpExecArray,
      ): Promise<Monaco.languages.InlayHint | undefined> {
        const end = queryMatch.index + queryMatch[1].length - 1;
        const endPos = model.getPositionAt(end);
        const inspectionPos = new sandbox.monaco.Position(
          endPos.lineNumber - 1,
          endPos.column,
        );
        const inspectionOff = model.getOffsetAt(inspectionPos);

        const hint = await (worker.getQuickInfoAtPosition(
          `file://${model.uri.path}`,
          inspectionOff,
        ) as Promise<ts.QuickInfo | undefined>);
        if (!hint?.displayParts) {
          return;
        }

        let text = hint.displayParts
          .map(d => d.text)
          .join('')
          .replaceAll(/\r?\n\s*/g, ' ');
        if (text.length > 120) {
          text = `${text.slice(0, 119)}...`;
        }

        return {
          kind: sandbox.monaco.languages.InlayHintKind.Type,
          label: text,
          paddingLeft: true,
          position: new sandbox.monaco.Position(
            endPos.lineNumber,
            endPos.column + 1,
          ),
        };
      }
    }
```
</details>

- **Parameters**:
  - `model: any`
  - `_: any`
  - `cancel: any`
- **Return Type**: `Promise<Monaco.languages.InlayHintList>`
- **Calls**:
  - `sandbox.getWorkerProcess`
  - `model.isDisposed`
  - `findTwoshashQueries`
  - `model.getValue`
  - `Promise.all`
  - `queryMatches.map`
  - `resolveInlayHint`
  - `results.push`
  - `model.getPositionAt`
  - `model.getOffsetAt`
  - `worker.getQuickInfoAtPosition`
  - `hint.displayParts
          .map(d => d.text)
          .join('')
          .replaceAll`
  - `text.slice`

---