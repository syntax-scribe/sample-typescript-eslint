[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `LoadedEditor.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 📦 Imports | 23 |
| 📊 Variables & Constants | 5 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/website/src/components/editor/LoadedEditor.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Monaco` | `monaco-editor` |
| `React` | `react` |
| `useColorMode` | `@docusaurus/theme-common` |
| `useCallback` | `react` |
| `useEffect` | `react` |
| `useMemo` | `react` |
| `useRef` | `react` |
| `useState` | `react` |
| `LintCodeAction` | `../linter/utils` |
| `TabType` | `../types` |
| `CommonEditorProps` | `./types` |
| `SandboxServices` | `./useSandboxServices` |
| `useResizeObserver` | `../hooks/useResizeObserver` |
| `createCompilerOptions` | `../lib/createCompilerOptions` |
| `debounce` | `../lib/debounce` |
| `getEslintJsonSchema` | `../lib/jsonSchema` |
| `getRuleJsonSchemaWithErrorLevel` | `../lib/jsonSchema` |
| `getTypescriptJsonSchema` | `../lib/jsonSchema` |
| `parseTSConfig` | `../lib/parseConfig` |
| `tryParseEslintModule` | `../lib/parseConfig` |
| `parseLintResults` | `../linter/utils` |
| `parseMarkers` | `../linter/utils` |
| `createProvideCodeActions` | `./createProvideCodeActions` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `codeActions` | `any` | const | `useRef(new Map<string, LintCodeAction[]>()).current` | ✗ |
| `tabsDefault` | `{ code: any; eslintrc: any; tsconfig: any; }` | const | `{
      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      code: editor.getModel()!,
      eslintrc: monaco.editor.createModel(
        eslintrc,
        'json',
        monaco.Uri.file('/.eslintrc'),
      ),
      tsconfig: monaco.editor.createModel(
        tsconfig,
        'json',
        monaco.Uri.file('/tsconfig.json'),
      ),
    }` | ✗ |
| `model` | `any` | const | `editor.getModel()!` | ✗ |
| `newPath` | `string` | const | ``/input${fileType}`` | ✗ |
| `closable` | `any[]` | const | `[
      system.watchFile('/tsconfig.json', filename => {
        onChange({ tsconfig: system.readFile(filename) });
      }),
      system.watchFile('/.eslintrc', filename => {
        onChange({ eslintrc: system.readFile(filename) });
      }),
      system.watchFile('/input.*', filename => {
        onChange({ code: system.readFile(filename) });
      }),
    ]` | ✗ |


---

## Functions

### `applyEdit(model: Monaco.editor.ITextModel, editor: Monaco.editor.ICodeEditor, edit: Monaco.editor.IIdentifiedSingleEditOperation): void`

<details><summary>Code</summary>

```ts
function applyEdit(
  model: Monaco.editor.ITextModel,
  editor: Monaco.editor.ICodeEditor,
  edit: Monaco.editor.IIdentifiedSingleEditOperation,
): void {
  if (model.isAttachedToEditor()) {
    editor.executeEdits('eslint', [edit]);
  } else {
    model.pushEditOperations([], [edit], () => null);
  }
}
```
</details>

- **Parameters**:
  - `model: Monaco.editor.ITextModel`
  - `editor: Monaco.editor.ICodeEditor`
  - `edit: Monaco.editor.IIdentifiedSingleEditOperation`
- **Return Type**: `void`
- **Calls**:
  - `model.isAttachedToEditor`
  - `editor.executeEdits`
  - `model.pushEditOperations`
### `LoadedEditor({
  activeTab,
  code,
  eslintrc,
  fileType,
  onASTChange,
  onChange,
  onMarkersChange,
  onSelect,
  sandboxInstance: { editor, monaco },
  selectedRange,
  showAST,
  sourceType,
  system,
  tsconfig,
  webLinter,
}: any): any`

<details><summary>Code</summary>

```ts
({
  activeTab,
  code,
  eslintrc,
  fileType,
  onASTChange,
  onChange,
  onMarkersChange,
  onSelect,
  sandboxInstance: { editor, monaco },
  selectedRange,
  showAST,
  sourceType,
  system,
  tsconfig,
  webLinter,
}) => {
  const { colorMode } = useColorMode();
  const [_, setDecorations] = useState<string[]>([]);

  const codeActions = useRef(new Map<string, LintCodeAction[]>()).current;
  const [tabs] = useState<Record<TabType, Monaco.editor.ITextModel>>(() => {
    const tabsDefault = {
      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      code: editor.getModel()!,
      eslintrc: monaco.editor.createModel(
        eslintrc,
        'json',
        monaco.Uri.file('/.eslintrc'),
      ),
      tsconfig: monaco.editor.createModel(
        tsconfig,
        'json',
        monaco.Uri.file('/tsconfig.json'),
      ),
    };
    tabsDefault.code.updateOptions({ insertSpaces: true, tabSize: 2 });
    tabsDefault.eslintrc.updateOptions({ insertSpaces: true, tabSize: 2 });
    tabsDefault.tsconfig.updateOptions({ insertSpaces: true, tabSize: 2 });
    return tabsDefault;
  });

  const updateMarkers = useCallback(() => {
    // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
    const model = editor.getModel()!;
    const markers = monaco.editor.getModelMarkers({
      resource: model.uri,
    });
    onMarkersChange(parseMarkers(markers, codeActions, editor));
  }, [codeActions, onMarkersChange, editor, monaco.editor]);

  useEffect(() => {
    webLinter.updateParserOptions(sourceType);
  }, [webLinter, sourceType]);

  useEffect(() => {
    const newPath = `/input${fileType}`;
    if (tabs.code.uri.path !== newPath) {
      const code = tabs.code.getValue();
      const newModel = monaco.editor.createModel(
        code,
        undefined,
        monaco.Uri.file(newPath),
      );
      newModel.updateOptions({ insertSpaces: true, tabSize: 2 });
      if (tabs.code.isAttachedToEditor()) {
        editor.setModel(newModel);
      }
      tabs.code.dispose();
      tabs.code = newModel;
      system.writeFile(newPath, code);
    }
  }, [fileType, editor, system, monaco, tabs]);

  useEffect(() => {
    const config = createCompilerOptions(
      parseTSConfig(tsconfig).compilerOptions,
    );
    monaco.languages.typescript.typescriptDefaults.setCompilerOptions(
      config as Monaco.languages.typescript.CompilerOptions,
    );
  }, [monaco, tsconfig]);

  useEffect(() => {
    if (editor.getModel()?.uri.path !== tabs[activeTab].uri.path) {
      editor.setModel(tabs[activeTab]);
      updateMarkers();
    }
  }, [activeTab, editor, tabs, updateMarkers]);

  useEffect(() => {
    const disposable = webLinter.onLint((uri, messages) => {
      const model = monaco.editor.getModel(monaco.Uri.file(uri));
      if (!model) {
        return;
      }
      const diagnostics = parseLintResults(messages, codeActions, ruleId =>
        monaco.Uri.parse(webLinter.rules.get(ruleId)?.url ?? ''),
      );
      monaco.editor.setModelMarkers(model, 'eslint', diagnostics);
      updateMarkers();
    });
    return (): void => disposable();
  }, [webLinter, monaco, codeActions, updateMarkers]);

  useEffect(() => {
    const disposable = webLinter.onParse((uri, model) => {
      onASTChange(model);
    });
    return (): void => disposable();
  }, [webLinter, onASTChange]);

  useEffect(() => {
    const createRuleUri = (name: string): string =>
      monaco.Uri.parse(`/rules/${name.replace('@', '')}.json`).toString();

    // configure the JSON language support with schemas and schema associations
    monaco.languages.json.jsonDefaults.setDiagnosticsOptions({
      allowComments: true,
      enableSchemaRequest: false,
      schemas: [
        ...[...webLinter.rules.values()].map(rule => ({
          schema: getRuleJsonSchemaWithErrorLevel(rule.name, rule.schema),
          uri: createRuleUri(rule.name),
        })),
        {
          fileMatch: ['/.eslintrc'], // associate with our model
          schema: getEslintJsonSchema(webLinter, createRuleUri),
          uri: monaco.Uri.file('eslint-schema.json').toString(), // id of the first schema
        },
        {
          fileMatch: ['/tsconfig.json'], // associate with our model
          schema: getTypescriptJsonSchema(),
          uri: monaco.Uri.file('ts-schema.json').toString(), // id of the first schema
        },
      ],
      validate: true,
    });
  }, [monaco, webLinter]);

  useEffect(() => {
    const disposable = monaco.languages.registerCodeActionProvider(
      'typescript',
      createProvideCodeActions(codeActions),
    );
    return (): void => disposable.dispose();
  }, [codeActions, monaco]);

  useEffect(() => {
    const disposable = editor.onDidPaste(() => {
      if (tabs.eslintrc.isAttachedToEditor()) {
        const value = tabs.eslintrc.getValue();
        const newValue = tryParseEslintModule(value);
        if (newValue !== value) {
          tabs.eslintrc.setValue(newValue);
        }
      }
    });
    return (): void => {
      disposable.dispose();
    };
  }, [editor, tabs.eslintrc]);

  useEffect(() => {
    const disposable = editor.onDidChangeCursorPosition(
      debounce(e => {
        if (tabs.code.isAttachedToEditor()) {
          const position = tabs.code.getOffsetAt(e.position);
          console.info('[Editor] updating cursor', position);
          onSelect(position);
        }
      }, 150),
    );
    return (): void => disposable.dispose();
  }, [onSelect, editor, tabs.code]);

  useEffect(() => {
    const disposable = editor.addAction({
      contextMenuGroupId: 'snippets',
      contextMenuOrder: 1.5,
      id: 'fix-eslint-problems',
      keybindings: [monaco.KeyMod.CtrlCmd | monaco.KeyCode.KeyS],
      label: 'Fix eslint problems',
      run(editor) {
        const editorModel = editor.getModel();
        if (editorModel) {
          const fixed = webLinter.triggerFix(editor.getValue());
          if (fixed?.fixed) {
            applyEdit(editorModel, editor, {
              range: editorModel.getFullModelRange(),
              text: fixed.output,
            });
          }
        }
      },
    });
    return (): void => disposable.dispose();
  }, [editor, monaco, webLinter]);

  useEffect(() => {
    const closable = [
      system.watchFile('/tsconfig.json', filename => {
        onChange({ tsconfig: system.readFile(filename) });
      }),
      system.watchFile('/.eslintrc', filename => {
        onChange({ eslintrc: system.readFile(filename) });
      }),
      system.watchFile('/input.*', filename => {
        onChange({ code: system.readFile(filename) });
      }),
    ];

    return (): void => {
      closable.forEach(c => c.close());
    };
  }, [system, onChange]);

  useEffect(() => {
    const disposable = editor.onDidChangeModelContent(() => {
      const model = editor.getModel();
      if (model) {
        system.writeFile(model.uri.path, model.getValue());
      }
    });
    return (): void => disposable.dispose();
  }, [editor, system]);

  useEffect(() => {
    const disposable = monaco.editor.onDidChangeMarkers(() => {
      updateMarkers();
    });
    return (): void => disposable.dispose();
  }, [monaco.editor, updateMarkers]);

  const resize = useMemo(() => {
    return debounce(() => editor.layout(), 1);
  }, [editor]);

  const container = editor.getContainerDomNode();

  useResizeObserver(container, () => {
    resize();
  });

  useEffect(() => {
    if (!editor.hasTextFocus() && code !== tabs.code.getValue()) {
      applyEdit(tabs.code, editor, {
        range: tabs.code.getFullModelRange(),
        text: code,
      });
    }
  }, [code, editor, tabs.code]);

  useEffect(() => {
    if (!editor.hasTextFocus() && tsconfig !== tabs.tsconfig.getValue()) {
      applyEdit(tabs.tsconfig, editor, {
        range: tabs.tsconfig.getFullModelRange(),
        text: tsconfig,
      });
    }
  }, [editor, tabs.tsconfig, tsconfig]);

  useEffect(() => {
    if (!editor.hasTextFocus() && eslintrc !== tabs.eslintrc.getValue()) {
      applyEdit(tabs.eslintrc, editor, {
        range: tabs.eslintrc.getFullModelRange(),
        text: eslintrc,
      });
    }
  }, [eslintrc, editor, tabs.eslintrc]);

  useEffect(() => {
    monaco.editor.setTheme(colorMode === 'dark' ? 'vs-dark' : 'vs-light');
  }, [colorMode, monaco]);

  useEffect(() => {
    setDecorations(prevDecorations =>
      tabs.code.deltaDecorations(
        prevDecorations,
        selectedRange && showAST
          ? [
              {
                options: {
                  inlineClassName: 'myLineDecoration',
                  stickiness: 1,
                },
                range: monaco.Range.fromPositions(
                  tabs.code.getPositionAt(selectedRange[0]),
                  tabs.code.getPositionAt(selectedRange[1]),
                ),
              },
            ]
          : [],
      ),
    );
  }, [selectedRange, monaco, showAST, tabs.code]);

  useEffect(() => {
    webLinter.triggerLint(tabs.code.uri.path);
  }, [webLinter, fileType, sourceType, tabs.code]);

  return null;
}
```
</details>

- **Parameters**:
  - `{
  activeTab,
  code,
  eslintrc,
  fileType,
  onASTChange,
  onChange,
  onMarkersChange,
  onSelect,
  sandboxInstance: { editor, monaco },
  selectedRange,
  showAST,
  sourceType,
  system,
  tsconfig,
  webLinter,
}: any`
- **Return Type**: `any`
- **Calls**:
  - `useColorMode (from @docusaurus/theme-common)`
  - `useState (from react)`
  - `useRef (from react)`
  - `editor.getModel`
  - `monaco.editor.createModel`
  - `monaco.Uri.file`
  - `tabsDefault.code.updateOptions`
  - `tabsDefault.eslintrc.updateOptions`
  - `tabsDefault.tsconfig.updateOptions`
  - `useCallback (from react)`
  - `monaco.editor.getModelMarkers`
  - `onMarkersChange`
  - `parseMarkers (from ../linter/utils)`
  - `useEffect (from react)`
  - `webLinter.updateParserOptions`
  - `tabs.code.getValue`
  - `newModel.updateOptions`
  - `tabs.code.isAttachedToEditor`
  - `editor.setModel`
  - `tabs.code.dispose`
  - `system.writeFile`
  - `createCompilerOptions (from ../lib/createCompilerOptions)`
  - `parseTSConfig (from ../lib/parseConfig)`
  - `monaco.languages.typescript.typescriptDefaults.setCompilerOptions`
  - `updateMarkers`
  - `webLinter.onLint`
  - `monaco.editor.getModel`
  - `parseLintResults (from ../linter/utils)`
  - `monaco.Uri.parse`
  - `webLinter.rules.get`
  - `monaco.editor.setModelMarkers`
  - `disposable`
  - `webLinter.onParse`
  - `onASTChange`
  - `monaco.Uri.parse(`/rules/${name.replace('@', '')}.json`).toString`
  - `monaco.languages.json.jsonDefaults.setDiagnosticsOptions`
  - `[...webLinter.rules.values()].map`
  - `webLinter.rules.values`
  - `getRuleJsonSchemaWithErrorLevel (from ../lib/jsonSchema)`
  - `createRuleUri`
  - `getEslintJsonSchema (from ../lib/jsonSchema)`
  - `monaco.Uri.file('eslint-schema.json').toString`
  - `getTypescriptJsonSchema (from ../lib/jsonSchema)`
  - `monaco.Uri.file('ts-schema.json').toString`
  - `monaco.languages.registerCodeActionProvider`
  - `createProvideCodeActions (from ./createProvideCodeActions)`
  - `disposable.dispose`
  - `editor.onDidPaste`
  - `tabs.eslintrc.isAttachedToEditor`
  - `tabs.eslintrc.getValue`
  - `tryParseEslintModule (from ../lib/parseConfig)`
  - `tabs.eslintrc.setValue`
  - `editor.onDidChangeCursorPosition`
  - `debounce (from ../lib/debounce)`
  - `tabs.code.getOffsetAt`
  - `console.info`
  - `onSelect`
  - `editor.addAction`
  - `webLinter.triggerFix`
  - `editor.getValue`
  - `applyEdit`
  - `editorModel.getFullModelRange`
  - `system.watchFile`
  - `onChange`
  - `system.readFile`
  - `closable.forEach`
  - `c.close`
  - `editor.onDidChangeModelContent`
  - `model.getValue`
  - `monaco.editor.onDidChangeMarkers`
  - `useMemo (from react)`
  - `editor.layout`
  - `editor.getContainerDomNode`
  - `useResizeObserver (from ../hooks/useResizeObserver)`
  - `resize`
  - `editor.hasTextFocus`
  - `tabs.code.getFullModelRange`
  - `tabs.tsconfig.getValue`
  - `tabs.tsconfig.getFullModelRange`
  - `tabs.eslintrc.getFullModelRange`
  - `monaco.editor.setTheme`
  - `setDecorations`
  - `tabs.code.deltaDecorations`
  - `monaco.Range.fromPositions`
  - `tabs.code.getPositionAt`
  - `webLinter.triggerLint`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x4)
// configure the JSON language support with schemas and schema associations (x7)
```

### `createRuleUri(name: string): string`

<details><summary>Code</summary>

```ts
(name: string): string =>
      monaco.Uri.parse(`/rules/${name.replace('@', '')}.json`).toString()
```
</details>

- **Parameters**:
  - `name: string`
- **Return Type**: `string`
- **Calls**:
  - `monaco.Uri.parse(`/rules/${name.replace('@', '')}.json`).toString`

---

## Type Aliases

### `LoadedEditorProps`

```ts
type LoadedEditorProps = CommonEditorProps & SandboxServices;
```


---