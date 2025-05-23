[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `parse.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 11
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/tests/lib/parse.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `CacheDurationSeconds` | `@typescript-eslint/types` |
| `debug` | `debug` |
| `join` | `node:path` |
| `resolve` | `node:path` |
| `TSESTreeOptions` | `../../src/parser-options` |
| `clearGlobResolutionCache` | `../../src/parseSettings/resolveProjectList` |


---

## Functions

### `alignErrorPath(error: Error): never`

<details><summary>Code</summary>

```ts
function alignErrorPath(error: Error): never {
  error.message = error.message.replaceAll(/\\(?!")/g, '/');
  throw error;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Aligns paths between environments, node for windows uses `\`, for linux and mac uses `/`
 */
```

- **Parameters**:
  - `error: Error`
- **Return Type**: `never`
- **Calls**:
  - `error.message.replaceAll`
### `checkNodeMaps(setting: boolean): void`

<details><summary>Code</summary>

```ts
function checkNodeMaps(setting: boolean): void {
      it('without project', () => {
        const parseResult = parser.parseAndGenerateServices(code, {
          ...baseConfig,
          preserveNodeMaps: setting,
        });

        expect(
          parseResult.services.esTreeNodeToTSNodeMap.has(
            parseResult.ast.body[0],
          ),
        ).toBe(setting);
      });

      it('with project', () => {
        const parseResult = parser.parseAndGenerateServices(code, {
          ...projectConfig,
          preserveNodeMaps: setting,
        });

        expect(
          parseResult.services.esTreeNodeToTSNodeMap.has(
            parseResult.ast.body[0],
          ),
        ).toBe(setting);
      });
    }
```
</details>

- **Parameters**:
  - `setting: boolean`
- **Return Type**: `void`
- **Calls**:
  - `it`
  - `parser.parseAndGenerateServices`
  - `expect(
          parseResult.services.esTreeNodeToTSNodeMap.has(
            parseResult.ast.body[0],
          ),
        ).toBe`
### `testParse({
      ext,
      jsxContent,
      jsxSetting,
      shouldThrow = false,
    }: {
      ext: '.js' | '.json' | '.jsx' | '.ts' | '.tsx' | '.vue';
      jsxContent: boolean;
      jsxSetting: boolean;
      shouldThrow?: boolean;
    }): void`

<details><summary>Code</summary>

```ts
({
      ext,
      jsxContent,
      jsxSetting,
      shouldThrow = false,
    }: {
      ext: '.js' | '.json' | '.jsx' | '.ts' | '.tsx' | '.vue';
      jsxContent: boolean;
      jsxSetting: boolean;
      shouldThrow?: boolean;
    }): void => {
      const code =
        ext === '.json'
          ? '{ "x": 1 }'
          : jsxContent
            ? 'const x = <div />;'
            : 'const x = 1';
      it(`should parse ${ext} file - ${
        jsxContent ? 'with' : 'without'
      } JSX content - parserOptions.jsx = ${jsxSetting}`, () => {
        let result:
          | parser.ParseAndGenerateServicesResult<typeof config>
          | undefined;
        // eslint-disable-next-line vitest/valid-expect
        const exp = expect(() => {
          result = parser.parseAndGenerateServices(code, {
            ...config,
            filePath: join(FIXTURES_DIR, `file${ext}`),
            jsx: jsxSetting,
          });
        });
        if (!shouldThrow) {
          exp.not.toThrow();
        } else {
          exp.toThrow();
        }

        if (!shouldThrow) {
          assert.isDefined(result?.ast);

          expect({
            ...result,
            services: {
              ...result.services,
              // Reduce noise in snapshot by not printing the TS program
              program:
                result.services.program == null ? 'No Program' : 'With Program',
            },
          }).toMatchSnapshot();
        }
      });
    }
```
</details>

- **Parameters**:
  - `{
      ext,
      jsxContent,
      jsxSetting,
      shouldThrow = false,
    }: {
      ext: '.js' | '.json' | '.jsx' | '.ts' | '.tsx' | '.vue';
      jsxContent: boolean;
      jsxSetting: boolean;
      shouldThrow?: boolean;
    }`
- **Return Type**: `void`
- **Calls**:
  - `it`
  - `expect`
  - `parser.parseAndGenerateServices`
  - `join (from node:path)`
  - `exp.not.toThrow`
  - `exp.toThrow`
  - `assert.isDefined`
  - `expect({
            ...result,
            services: {
              ...result.services,
              // Reduce noise in snapshot by not printing the TS program
              program:
                result.services.program == null ? 'No Program' : 'With Program',
            },
          }).toMatchSnapshot`
- **Internal Comments**:
```
// eslint-disable-next-line vitest/valid-expect (x2)
// Reduce noise in snapshot by not printing the TS program (x2)
```

### `testParse({
        ext,
        shouldAllowTLA = false,
        sourceType,
      }: {
        ext: '.js' | '.mjs' | '.mts' | '.ts';
        shouldAllowTLA?: boolean;
        sourceType?: 'module' | 'script';
      }): void`

<details><summary>Code</summary>

```ts
({
        ext,
        shouldAllowTLA = false,
        sourceType,
      }: {
        ext: '.js' | '.mjs' | '.mts' | '.ts';
        shouldAllowTLA?: boolean;
        sourceType?: 'module' | 'script';
      }): void => {
        const ast = parser.parse(code, {
          ...config,
          filePath: `file${ext}`,
          sourceType,
        });
        const expressionType = (
          ast.body[0] as parser.TSESTree.ExpressionStatement
        ).expression.type;

        it(`parse(): should ${
          shouldAllowTLA ? 'allow' : 'not allow'
        } TLA for ${ext} file with sourceType = ${sourceType}`, () => {
          expect(expressionType).toBe(
            shouldAllowTLA
              ? parser.AST_NODE_TYPES.AwaitExpression
              : parser.AST_NODE_TYPES.CallExpression,
          );
        });
      }
```
</details>

- **Parameters**:
  - `{
        ext,
        shouldAllowTLA = false,
        sourceType,
      }: {
        ext: '.js' | '.mjs' | '.mts' | '.ts';
        shouldAllowTLA?: boolean;
        sourceType?: 'module' | 'script';
      }`
- **Return Type**: `void`
- **Calls**:
  - `parser.parse`
  - `it`
  - `expect(expressionType).toBe`
### `testParseAndGenerateServices({
        ext,
        shouldAllowTLA = false,
        sourceType,
      }: {
        ext: '.js' | '.mjs' | '.mts' | '.ts';
        shouldAllowTLA?: boolean;
        sourceType?: 'module' | 'script';
      }): void`

<details><summary>Code</summary>

```ts
({
        ext,
        shouldAllowTLA = false,
        sourceType,
      }: {
        ext: '.js' | '.mjs' | '.mts' | '.ts';
        shouldAllowTLA?: boolean;
        sourceType?: 'module' | 'script';
      }): void => {
        const result = parser.parseAndGenerateServices(code, {
          ...config,
          filePath: `file${ext}`,
          sourceType,
        });
        const expressionType = (
          result.ast.body[0] as parser.TSESTree.ExpressionStatement
        ).expression.type;

        it(`parseAndGenerateServices(): should ${
          shouldAllowTLA ? 'allow' : 'not allow'
        } TLA for ${ext} file with sourceType = ${sourceType}`, () => {
          expect(expressionType).toBe(
            shouldAllowTLA
              ? parser.AST_NODE_TYPES.AwaitExpression
              : parser.AST_NODE_TYPES.CallExpression,
          );
        });
      }
```
</details>

- **Parameters**:
  - `{
        ext,
        shouldAllowTLA = false,
        sourceType,
      }: {
        ext: '.js' | '.mjs' | '.mts' | '.ts';
        shouldAllowTLA?: boolean;
        sourceType?: 'module' | 'script';
      }`
- **Return Type**: `void`
- **Calls**:
  - `parser.parseAndGenerateServices`
  - `it`
  - `expect(expressionType).toBe`
### `testParse(filePath: string, extraFileExtensions: string[]): () => void`

<details><summary>Code</summary>

```ts
(filePath: string, extraFileExtensions: string[] = ['.vue']) =>
        (): void => {
          try {
            parser.parseAndGenerateServices(code, {
              ...config,
              extraFileExtensions,
              filePath: join(PROJECT_DIR, filePath),
              project: './tsconfig.json',
            });
          } catch (error) {
            alignErrorPath(error as Error);
          }
        }
```
</details>

- **Parameters**:
  - `filePath: string`
  - `extraFileExtensions: string[]`
- **Return Type**: `() => void`
### `testExtraFileExtensions(filePath: string, extraFileExtensions: string[]): () => void`

<details><summary>Code</summary>

```ts
(filePath: string, extraFileExtensions: string[]) => (): void => {
          parser.parseAndGenerateServices(code, {
            ...config,
            extraFileExtensions,
            filePath: join(PROJECT_DIR, filePath),
            projectService: true,
          });
        }
```
</details>

- **Parameters**:
  - `filePath: string`
  - `extraFileExtensions: string[]`
- **Return Type**: `() => void`
### `testParse(filePath: string): () => void`

<details><summary>Code</summary>

```ts
(filePath: string) => (): void => {
          try {
            parser.parseAndGenerateServices(code, {
              ...config,
              filePath: join(PROJECT_DIR, filePath),
            });
          } catch (error) {
            alignErrorPath(error as Error);
          }
        }
```
</details>

- **Parameters**:
  - `filePath: string`
- **Return Type**: `() => void`
### `testParse(filePath: 'ignoreme' | 'includeme', projectFolderIgnoreList: TSESTreeOptions['projectFolderIgnoreList']): () => void`

<details><summary>Code</summary>

```ts
(
          filePath: 'ignoreme' | 'includeme',
          projectFolderIgnoreList?: TSESTreeOptions['projectFolderIgnoreList'],
        ) =>
        (): void => {
          parser.parseAndGenerateServices(code, {
            ...config,
            filePath: join(PROJECT_DIR, filePath, './file.ts'),
            projectFolderIgnoreList,
          });
        }
```
</details>

- **Parameters**:
  - `filePath: 'ignoreme' | 'includeme'`
  - `projectFolderIgnoreList: TSESTreeOptions['projectFolderIgnoreList']`
- **Return Type**: `() => void`
### `doParse(lifetime: CacheDurationSeconds): void`

<details><summary>Code</summary>

```ts
function doParse(lifetime: CacheDurationSeconds): void {
          parser.parseAndGenerateServices('const x = 1', {
            cacheLifetime: {
              glob: lifetime,
            },
            disallowAutomaticSingleRunInference: true,
            filePath: join(FIXTURES_DIR, 'file.ts'),
            project,
            tsconfigRootDir: FIXTURES_DIR,
          });
        }
```
</details>

- **Parameters**:
  - `lifetime: CacheDurationSeconds`
- **Return Type**: `void`
- **Calls**:
  - `parser.parseAndGenerateServices`
  - `join (from node:path)`
### `testParse(): () => void`

<details><summary>Code</summary>

```ts
() => (): void => {
        parser.parseAndGenerateServices(code, {
          disallowAutomaticSingleRunInference: true,
          filePath: join(PROJECT_DIR, 'file.ts'),
          project: './**/tsconfig.json',
          tsconfigRootDir: PROJECT_DIR,
        });
      }
```
</details>

- **Return Type**: `() => void`

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