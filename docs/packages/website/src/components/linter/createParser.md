[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `createParser.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 20
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/linter/createParser.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserOptions` | `@typescript-eslint/types` |
| `Parser` | `@typescript-eslint/utils/ts-eslint` |
| `ParseSettings` | `./types` |
| `PlaygroundSystem` | `./types` |
| `UpdateModel` | `./types` |
| `WebLinterModule` | `./types` |
| `defaultParseSettings` | `./config` |


---

## Functions

### `createParser(system: PlaygroundSystem, compilerOptions: ts.CompilerOptions, onUpdate: (filename: string, model: UpdateModel) => void, utils: WebLinterModule, vfs: typeof tsvfs): {
  updateConfig: (compilerOptions: ts.CompilerOptions) => void;
} & Parser.ParserModule`

<details><summary>Code</summary>

```ts
export function createParser(
  system: PlaygroundSystem,
  compilerOptions: ts.CompilerOptions,
  onUpdate: (filename: string, model: UpdateModel) => void,
  utils: WebLinterModule,
  vfs: typeof tsvfs,
): {
  updateConfig: (compilerOptions: ts.CompilerOptions) => void;
} & Parser.ParserModule {
  const registeredFiles = new Set<string>();

  const createEnv = (
    compilerOptions: ts.CompilerOptions,
  ): tsvfs.VirtualTypeScriptEnvironment => {
    return vfs.createVirtualTypeScriptEnvironment(
      system,
      [...registeredFiles],
      window.ts,
      compilerOptions,
    );
  };

  let compilerHost = createEnv(compilerOptions);

  return {
    parseForESLint: (
      text: string,
      options: ParserOptions = {},
    ): Parser.ParseResult => {
      const filePath = options.filePath ?? '/input.ts';

      // if text is empty use empty line to avoid error
      const code = text || '\n';

      if (registeredFiles.has(filePath)) {
        compilerHost.updateFile(filePath, code);
      } else {
        registeredFiles.add(filePath);
        compilerHost.createFile(filePath, code);
      }

      const parseSettings: ParseSettings = {
        ...defaultParseSettings,
        code,
        codeFullText: code,
        filePath,
      };

      const program = compilerHost.languageService.getProgram();
      if (!program) {
        throw new Error('Failed to get program');
      }

      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      const tsAst = program.getSourceFile(filePath)!;

      const converted = utils.astConverter(tsAst, parseSettings, true);

      const scopeManager = utils.analyze(converted.estree, {
        globalReturn: options.ecmaFeatures?.globalReturn ?? false,
        sourceType: options.sourceType ?? 'module',
      });

      const checker = program.getTypeChecker();
      const compilerOptions = program.getCompilerOptions();

      onUpdate(filePath, {
        storedAST: converted.estree,
        storedScope: scopeManager,
        storedTsAST: tsAst,
        typeChecker: checker,
      });

      return {
        ast: converted.estree,
        scopeManager,
        services: {
          emitDecoratorMetadata: compilerOptions.emitDecoratorMetadata ?? false,
          esTreeNodeToTSNodeMap: converted.astMaps.esTreeNodeToTSNodeMap,
          experimentalDecorators:
            compilerOptions.experimentalDecorators ?? false,
          getSymbolAtLocation: node =>
            checker.getSymbolAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            ),
          getTypeAtLocation: node =>
            checker.getTypeAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            ),
          isolatedDeclarations: compilerOptions.isolatedDeclarations ?? false,
          program,
          tsNodeToESTreeNodeMap: converted.astMaps.tsNodeToESTreeNodeMap,
        },
        visitorKeys: utils.visitorKeys,
      };
    },
    updateConfig(compilerOptions): void {
      compilerHost = createEnv(compilerOptions);
    },
  };
}
```
</details>

- **Parameters**:
  - `system: PlaygroundSystem`
  - `compilerOptions: ts.CompilerOptions`
  - `onUpdate: (filename: string, model: UpdateModel) => void`
  - `utils: WebLinterModule`
  - `vfs: typeof tsvfs`
- **Return Type**: `{
  updateConfig: (compilerOptions: ts.CompilerOptions) => void;
} & Parser.ParserModule`
- **Calls**:
  - `vfs.createVirtualTypeScriptEnvironment`
  - `createEnv`
  - `registeredFiles.has`
  - `compilerHost.updateFile`
  - `registeredFiles.add`
  - `compilerHost.createFile`
  - `compilerHost.languageService.getProgram`
  - `program.getSourceFile`
  - `utils.astConverter`
  - `utils.analyze`
  - `program.getTypeChecker`
  - `program.getCompilerOptions`
  - `onUpdate`
  - `checker.getSymbolAtLocation`
  - `converted.astMaps.esTreeNodeToTSNodeMap.get`
  - `checker.getTypeAtLocation`
- **Internal Comments**:
```
// if text is empty use empty line to avoid error (x2)
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x2)
```

### `createEnv(compilerOptions: ts.CompilerOptions): tsvfs.VirtualTypeScriptEnvironment`

<details><summary>Code</summary>

```ts
(
    compilerOptions: ts.CompilerOptions,
  ): tsvfs.VirtualTypeScriptEnvironment => {
    return vfs.createVirtualTypeScriptEnvironment(
      system,
      [...registeredFiles],
      window.ts,
      compilerOptions,
    );
  }
```
</details>

- **Parameters**:
  - `compilerOptions: ts.CompilerOptions`
- **Return Type**: `tsvfs.VirtualTypeScriptEnvironment`
- **Calls**:
  - `vfs.createVirtualTypeScriptEnvironment`
### `parseForESLint(text: string, options: ParserOptions): Parser.ParseResult`

<details><summary>Code</summary>

```ts
(
      text: string,
      options: ParserOptions = {},
    ): Parser.ParseResult => {
      const filePath = options.filePath ?? '/input.ts';

      // if text is empty use empty line to avoid error
      const code = text || '\n';

      if (registeredFiles.has(filePath)) {
        compilerHost.updateFile(filePath, code);
      } else {
        registeredFiles.add(filePath);
        compilerHost.createFile(filePath, code);
      }

      const parseSettings: ParseSettings = {
        ...defaultParseSettings,
        code,
        codeFullText: code,
        filePath,
      };

      const program = compilerHost.languageService.getProgram();
      if (!program) {
        throw new Error('Failed to get program');
      }

      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      const tsAst = program.getSourceFile(filePath)!;

      const converted = utils.astConverter(tsAst, parseSettings, true);

      const scopeManager = utils.analyze(converted.estree, {
        globalReturn: options.ecmaFeatures?.globalReturn ?? false,
        sourceType: options.sourceType ?? 'module',
      });

      const checker = program.getTypeChecker();
      const compilerOptions = program.getCompilerOptions();

      onUpdate(filePath, {
        storedAST: converted.estree,
        storedScope: scopeManager,
        storedTsAST: tsAst,
        typeChecker: checker,
      });

      return {
        ast: converted.estree,
        scopeManager,
        services: {
          emitDecoratorMetadata: compilerOptions.emitDecoratorMetadata ?? false,
          esTreeNodeToTSNodeMap: converted.astMaps.esTreeNodeToTSNodeMap,
          experimentalDecorators:
            compilerOptions.experimentalDecorators ?? false,
          getSymbolAtLocation: node =>
            checker.getSymbolAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            ),
          getTypeAtLocation: node =>
            checker.getTypeAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            ),
          isolatedDeclarations: compilerOptions.isolatedDeclarations ?? false,
          program,
          tsNodeToESTreeNodeMap: converted.astMaps.tsNodeToESTreeNodeMap,
        },
        visitorKeys: utils.visitorKeys,
      };
    }
```
</details>

- **Parameters**:
  - `text: string`
  - `options: ParserOptions`
- **Return Type**: `Parser.ParseResult`
- **Calls**:
  - `registeredFiles.has`
  - `compilerHost.updateFile`
  - `registeredFiles.add`
  - `compilerHost.createFile`
  - `compilerHost.languageService.getProgram`
  - `program.getSourceFile`
  - `utils.astConverter`
  - `utils.analyze`
  - `program.getTypeChecker`
  - `program.getCompilerOptions`
  - `onUpdate`
  - `checker.getSymbolAtLocation`
  - `converted.astMaps.esTreeNodeToTSNodeMap.get`
  - `checker.getTypeAtLocation`
- **Internal Comments**:
```
// if text is empty use empty line to avoid error (x2)
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x2)
```

### `getSymbolAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getSymbolAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getSymbolAtLocation`
### `getTypeAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getTypeAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getTypeAtLocation`
### `getSymbolAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getSymbolAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getSymbolAtLocation`
### `getTypeAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getTypeAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getTypeAtLocation`
### `getSymbolAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getSymbolAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getSymbolAtLocation`
### `getTypeAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getTypeAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getTypeAtLocation`
### `getSymbolAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getSymbolAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getSymbolAtLocation`
### `getTypeAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getTypeAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getTypeAtLocation`
### `parseForESLint(text: string, options: ParserOptions): Parser.ParseResult`

<details><summary>Code</summary>

```ts
(
      text: string,
      options: ParserOptions = {},
    ): Parser.ParseResult => {
      const filePath = options.filePath ?? '/input.ts';

      // if text is empty use empty line to avoid error
      const code = text || '\n';

      if (registeredFiles.has(filePath)) {
        compilerHost.updateFile(filePath, code);
      } else {
        registeredFiles.add(filePath);
        compilerHost.createFile(filePath, code);
      }

      const parseSettings: ParseSettings = {
        ...defaultParseSettings,
        code,
        codeFullText: code,
        filePath,
      };

      const program = compilerHost.languageService.getProgram();
      if (!program) {
        throw new Error('Failed to get program');
      }

      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      const tsAst = program.getSourceFile(filePath)!;

      const converted = utils.astConverter(tsAst, parseSettings, true);

      const scopeManager = utils.analyze(converted.estree, {
        globalReturn: options.ecmaFeatures?.globalReturn ?? false,
        sourceType: options.sourceType ?? 'module',
      });

      const checker = program.getTypeChecker();
      const compilerOptions = program.getCompilerOptions();

      onUpdate(filePath, {
        storedAST: converted.estree,
        storedScope: scopeManager,
        storedTsAST: tsAst,
        typeChecker: checker,
      });

      return {
        ast: converted.estree,
        scopeManager,
        services: {
          emitDecoratorMetadata: compilerOptions.emitDecoratorMetadata ?? false,
          esTreeNodeToTSNodeMap: converted.astMaps.esTreeNodeToTSNodeMap,
          experimentalDecorators:
            compilerOptions.experimentalDecorators ?? false,
          getSymbolAtLocation: node =>
            checker.getSymbolAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            ),
          getTypeAtLocation: node =>
            checker.getTypeAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            ),
          isolatedDeclarations: compilerOptions.isolatedDeclarations ?? false,
          program,
          tsNodeToESTreeNodeMap: converted.astMaps.tsNodeToESTreeNodeMap,
        },
        visitorKeys: utils.visitorKeys,
      };
    }
```
</details>

- **Parameters**:
  - `text: string`
  - `options: ParserOptions`
- **Return Type**: `Parser.ParseResult`
- **Calls**:
  - `registeredFiles.has`
  - `compilerHost.updateFile`
  - `registeredFiles.add`
  - `compilerHost.createFile`
  - `compilerHost.languageService.getProgram`
  - `program.getSourceFile`
  - `utils.astConverter`
  - `utils.analyze`
  - `program.getTypeChecker`
  - `program.getCompilerOptions`
  - `onUpdate`
  - `checker.getSymbolAtLocation`
  - `converted.astMaps.esTreeNodeToTSNodeMap.get`
  - `checker.getTypeAtLocation`
- **Internal Comments**:
```
// if text is empty use empty line to avoid error (x2)
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x2)
```

### `getSymbolAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getSymbolAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getSymbolAtLocation`
### `getTypeAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getTypeAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getTypeAtLocation`
### `getSymbolAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getSymbolAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getSymbolAtLocation`
### `getTypeAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getTypeAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getTypeAtLocation`
### `getSymbolAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getSymbolAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getSymbolAtLocation`
### `getTypeAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getTypeAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getTypeAtLocation`
### `getSymbolAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getSymbolAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getSymbolAtLocation`
### `getTypeAtLocation(node: any): any`

<details><summary>Code</summary>

```ts
node =>
            checker.getTypeAtLocation(
              converted.astMaps.esTreeNodeToTSNodeMap.get(node),
            )
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `any`
- **Calls**:
  - `checker.getTypeAtLocation`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---