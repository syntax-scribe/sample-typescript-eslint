[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `createLinter.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 8
- **Classes**: 0
- **Imports**: 16
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/linter/createLinter.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `ClassicConfig` | `@typescript-eslint/utils/ts-eslint` |
| `Linter` | `@typescript-eslint/utils/ts-eslint` |
| `SourceType` | `@typescript-eslint/utils/ts-eslint` |
| `LinterOnLint` | `./types` |
| `LinterOnParse` | `./types` |
| `PlaygroundSystem` | `./types` |
| `WebLinterModule` | `./types` |
| `createCompilerOptions` | `../lib/createCompilerOptions` |
| `createEventsBinder` | `../lib/createEventsBinder` |
| `parseESLintRC` | `../lib/parseConfig` |
| `parseTSConfig` | `../lib/parseConfig` |
| `defaultEslintConfig` | `./config` |
| `PARSER_NAME` | `./config` |
| `createParser` | `./createParser` |


---

## Functions

### `createLinter(system: PlaygroundSystem, webLinterModule: WebLinterModule, vfs: typeof tsvfs): CreateLinter`

<details><summary>Code</summary>

```ts
export function createLinter(
  system: PlaygroundSystem,
  webLinterModule: WebLinterModule,
  vfs: typeof tsvfs,
): CreateLinter {
  const rules: CreateLinter['rules'] = new Map();
  const configs = new Map(Object.entries(webLinterModule.configs));
  let compilerOptions: ts.CompilerOptions = {};
  const eslintConfig: ClassicConfig.Config = { ...defaultEslintConfig };

  const onLint = createEventsBinder<LinterOnLint>();
  const onParse = createEventsBinder<LinterOnParse>();

  const linter = webLinterModule.createLinter();

  const parser = createParser(
    system,
    compilerOptions,
    (filename, model): void => {
      onParse.trigger(filename, model);
    },
    webLinterModule,
    vfs,
  );

  linter.defineParser(PARSER_NAME, parser);

  linter.getRules().forEach((item, name) => {
    rules.set(name, {
      description: item.meta?.docs?.description,
      name,
      schema: item.meta?.schema ?? [],
      url: item.meta?.docs?.url,
    });
  });

  const triggerLint = (filename: string): void => {
    console.info('[Editor] linting triggered for file', filename);
    const code = system.readFile(filename) ?? '\n';
    try {
      const messages = linter.verify(code, eslintConfig, filename);
      onLint.trigger(filename, messages);
    } catch (e) {
      const lintMessage: Linter.LintMessage = {
        column: 1,
        line: 1,
        message: String(e instanceof Error ? e.stack : e),
        nodeType: '',
        ruleId: '',
        severity: 2,
        source: 'eslint',
      };
      if (typeof e === 'object' && e && 'currentNode' in e) {
        const node = e.currentNode as TSESTree.Node;
        lintMessage.column = node.loc.start.column + 1;
        lintMessage.line = node.loc.start.line;
        lintMessage.endColumn = node.loc.end.column + 1;
        lintMessage.endLine = node.loc.end.line;
      }
      onLint.trigger(filename, [lintMessage]);
    }
  };

  const triggerFix = (filename: string): Linter.FixReport | undefined => {
    const code = system.readFile(filename);
    if (code) {
      return linter.verifyAndFix(code, eslintConfig, {
        filename,
        fix: true,
      });
    }
    return undefined;
  };

  const updateParserOptions = (sourceType?: SourceType): void => {
    eslintConfig.parserOptions ??= {};
    eslintConfig.parserOptions.sourceType = sourceType ?? 'module';
  };

  const resolveEslintConfig = (
    cfg: Partial<ClassicConfig.Config>,
  ): ClassicConfig.Config => {
    const config = { rules: {} };
    if (cfg.extends) {
      const cfgExtends = Array.isArray(cfg.extends)
        ? cfg.extends
        : [cfg.extends];
      for (const extendsName of cfgExtends) {
        const maybeConfig = configs.get(extendsName);
        if (maybeConfig) {
          const resolved = resolveEslintConfig(maybeConfig);
          if (resolved.rules) {
            Object.assign(config.rules, resolved.rules);
          }
        }
      }
    }
    if (cfg.rules) {
      Object.assign(config.rules, cfg.rules);
    }
    return config;
  };

  const applyEslintConfig = (fileName: string): void => {
    try {
      const file = system.readFile(fileName) ?? '{}';
      const parsed = resolveEslintConfig(parseESLintRC(file));
      eslintConfig.rules = parsed.rules;
      console.log('[Editor] Updating', fileName, eslintConfig);
    } catch (e) {
      console.error(e);
    }
  };

  const applyTSConfig = (fileName: string): void => {
    try {
      const file = system.readFile(fileName) ?? '{}';
      const parsed = parseTSConfig(file).compilerOptions;
      compilerOptions = createCompilerOptions(parsed);
      console.log('[Editor] Updating', fileName, compilerOptions);
      parser.updateConfig(compilerOptions);
    } catch (e) {
      console.error(e);
    }
  };

  const triggerLintAll = (): void => {
    system.searchFiles('/input.*').forEach(triggerLint);
  };

  system.watchFile('/input.*', triggerLint);
  system.watchFile('/.eslintrc', filename => {
    applyEslintConfig(filename);
    triggerLintAll();
  });
  system.watchFile('/tsconfig.json', filename => {
    applyTSConfig(filename);
    triggerLintAll();
  });

  applyEslintConfig('/.eslintrc');
  applyTSConfig('/tsconfig.json');

  return {
    configs: [...configs.keys()],
    onLint: onLint.register,
    onParse: onParse.register,
    rules,
    triggerFix,
    triggerLint,
    updateParserOptions,
  };
}
```
</details>

- **Parameters**:
  - `system: PlaygroundSystem`
  - `webLinterModule: WebLinterModule`
  - `vfs: typeof tsvfs`
- **Return Type**: `CreateLinter`
- **Calls**:
  - `Object.entries`
  - `createEventsBinder (from ../lib/createEventsBinder)`
  - `webLinterModule.createLinter`
  - `createParser (from ./createParser)`
  - `onParse.trigger`
  - `linter.defineParser`
  - `linter.getRules().forEach`
  - `rules.set`
  - `console.info`
  - `system.readFile`
  - `linter.verify`
  - `onLint.trigger`
  - `String`
  - `linter.verifyAndFix`
  - `Array.isArray`
  - `configs.get`
  - `resolveEslintConfig`
  - `Object.assign`
  - `parseESLintRC (from ../lib/parseConfig)`
  - `console.log`
  - `console.error`
  - `parseTSConfig (from ../lib/parseConfig)`
  - `createCompilerOptions (from ../lib/createCompilerOptions)`
  - `parser.updateConfig`
  - `system.searchFiles('/input.*').forEach`
  - `system.watchFile`
  - `applyEslintConfig`
  - `triggerLintAll`
  - `applyTSConfig`
  - `configs.keys`
### `triggerLint(filename: string): void`

<details><summary>Code</summary>

```ts
(filename: string): void => {
    console.info('[Editor] linting triggered for file', filename);
    const code = system.readFile(filename) ?? '\n';
    try {
      const messages = linter.verify(code, eslintConfig, filename);
      onLint.trigger(filename, messages);
    } catch (e) {
      const lintMessage: Linter.LintMessage = {
        column: 1,
        line: 1,
        message: String(e instanceof Error ? e.stack : e),
        nodeType: '',
        ruleId: '',
        severity: 2,
        source: 'eslint',
      };
      if (typeof e === 'object' && e && 'currentNode' in e) {
        const node = e.currentNode as TSESTree.Node;
        lintMessage.column = node.loc.start.column + 1;
        lintMessage.line = node.loc.start.line;
        lintMessage.endColumn = node.loc.end.column + 1;
        lintMessage.endLine = node.loc.end.line;
      }
      onLint.trigger(filename, [lintMessage]);
    }
  }
```
</details>

- **Parameters**:
  - `filename: string`
- **Return Type**: `void`
- **Calls**:
  - `console.info`
  - `system.readFile`
  - `linter.verify`
  - `onLint.trigger`
  - `String`
### `triggerFix(filename: string): Linter.FixReport | undefined`

<details><summary>Code</summary>

```ts
(filename: string): Linter.FixReport | undefined => {
    const code = system.readFile(filename);
    if (code) {
      return linter.verifyAndFix(code, eslintConfig, {
        filename,
        fix: true,
      });
    }
    return undefined;
  }
```
</details>

- **Parameters**:
  - `filename: string`
- **Return Type**: `Linter.FixReport | undefined`
- **Calls**:
  - `system.readFile`
  - `linter.verifyAndFix`
### `updateParserOptions(sourceType: SourceType): void`

<details><summary>Code</summary>

```ts
(sourceType?: SourceType): void => {
    eslintConfig.parserOptions ??= {};
    eslintConfig.parserOptions.sourceType = sourceType ?? 'module';
  }
```
</details>

- **Parameters**:
  - `sourceType: SourceType`
- **Return Type**: `void`
### `resolveEslintConfig(cfg: Partial<ClassicConfig.Config>): ClassicConfig.Config`

<details><summary>Code</summary>

```ts
(
    cfg: Partial<ClassicConfig.Config>,
  ): ClassicConfig.Config => {
    const config = { rules: {} };
    if (cfg.extends) {
      const cfgExtends = Array.isArray(cfg.extends)
        ? cfg.extends
        : [cfg.extends];
      for (const extendsName of cfgExtends) {
        const maybeConfig = configs.get(extendsName);
        if (maybeConfig) {
          const resolved = resolveEslintConfig(maybeConfig);
          if (resolved.rules) {
            Object.assign(config.rules, resolved.rules);
          }
        }
      }
    }
    if (cfg.rules) {
      Object.assign(config.rules, cfg.rules);
    }
    return config;
  }
```
</details>

- **Parameters**:
  - `cfg: Partial<ClassicConfig.Config>`
- **Return Type**: `ClassicConfig.Config`
- **Calls**:
  - `Array.isArray`
  - `configs.get`
  - `resolveEslintConfig`
  - `Object.assign`
### `applyEslintConfig(fileName: string): void`

<details><summary>Code</summary>

```ts
(fileName: string): void => {
    try {
      const file = system.readFile(fileName) ?? '{}';
      const parsed = resolveEslintConfig(parseESLintRC(file));
      eslintConfig.rules = parsed.rules;
      console.log('[Editor] Updating', fileName, eslintConfig);
    } catch (e) {
      console.error(e);
    }
  }
```
</details>

- **Parameters**:
  - `fileName: string`
- **Return Type**: `void`
- **Calls**:
  - `system.readFile`
  - `resolveEslintConfig`
  - `parseESLintRC (from ../lib/parseConfig)`
  - `console.log`
  - `console.error`
### `applyTSConfig(fileName: string): void`

<details><summary>Code</summary>

```ts
(fileName: string): void => {
    try {
      const file = system.readFile(fileName) ?? '{}';
      const parsed = parseTSConfig(file).compilerOptions;
      compilerOptions = createCompilerOptions(parsed);
      console.log('[Editor] Updating', fileName, compilerOptions);
      parser.updateConfig(compilerOptions);
    } catch (e) {
      console.error(e);
    }
  }
```
</details>

- **Parameters**:
  - `fileName: string`
- **Return Type**: `void`
- **Calls**:
  - `system.readFile`
  - `parseTSConfig (from ../lib/parseConfig)`
  - `createCompilerOptions (from ../lib/createCompilerOptions)`
  - `console.log`
  - `parser.updateConfig`
  - `console.error`
### `triggerLintAll(): void`

<details><summary>Code</summary>

```ts
(): void => {
    system.searchFiles('/input.*').forEach(triggerLint);
  }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `system.searchFiles('/input.*').forEach`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `CreateLinter`

<details><summary>Interface Code</summary>

```ts
export interface CreateLinter {
  configs: string[];
  onLint(cb: LinterOnLint): () => void;
  onParse(cb: LinterOnParse): () => void;
  rules: Map<
    string,
    {
      description?: string;
      name: string;
      schema: JSONSchema.JSONSchema4 | readonly JSONSchema.JSONSchema4[];
      url?: string;
    }
  >;
  triggerFix(filename: string): Linter.FixReport | undefined;
  triggerLint(filename: string): void;
  updateParserOptions(sourceType?: SourceType): void;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `configs` | `string[]` | ✗ |  |
| `rules` | `Map<
    string,
    {
      description?: string;
      name: string;
      schema: JSONSchema.JSONSchema4 | readonly JSONSchema.JSONSchema4[];
      url?: string;
    }
  >` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---