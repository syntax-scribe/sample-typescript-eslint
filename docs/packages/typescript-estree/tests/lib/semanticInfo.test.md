[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `semanticInfo.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 8 |
| 📊 Variables & Constants | 36 |
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
📂 **`packages/typescript-estree/tests/lib/semanticInfo.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `../../src/index.js` |
| `TSESTreeOptions` | `../../src/index.js` |
| `createProgram` | `../../src/create-program/useProvidedPrograms.js` |
| `clearCaches` | `../../src/index.js` |
| `parseAndGenerateServices` | `../../src/index.js` |
| `deeplyCopy` | `../test-utils/test-utils.js` |
| `formatSnapshotName` | `../test-utils/test-utils.js` |
| `parseCodeAndGenerateServices` | `../test-utils/test-utils.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `code` | `string` | let/var | `await fs.readFile(path.join(FIXTURES_DIR, filename), {
        encoding: 'utf-8',
      })` | ✗ |
| `testCases` | `any` | let/var | `await Promise.all(
    testFiles.map(async filename => {
      const code = await fs.readFile(path.join(FIXTURES_DIR, filename), {
        encoding: 'utf-8',
      });
      const snapshotName = formatSnapshotName(
        filename,
        FIXTURES_DIR,
        path.extname(filename),
      );

      const { ast } = parseAndGenerateServices(code, createOptions(filename));

      const result = deeplyCopy(ast);

      return [snapshotName, result] as const;
    }),
  )` | ✗ |
| `filename` | `any` | let/var | `testFiles[0]` | ✗ |
| `code` | `string` | let/var | `await fs.readFile(path.join(FIXTURES_DIR, filename), {
      encoding: 'utf-8',
    })` | ✗ |
| `optionsProjectString` | `{ project: string; cwd?: string; cacheLifetime?: { glob?: CacheDurationSeconds; }; disallowAutomaticSingleRunInference?: boolean; errorOnTypeScriptSyntacticAndSemanticIssues?: boolean; extraFileExtensions?: string[]; ... 17 more ...; suppressDeprecatedPropertyWarnings?: boolean; }` | let/var | `{
      ...options,
      project: './tsconfig.json',
    }` | ✗ |
| `filename` | `any` | let/var | `testFiles[0]` | ✗ |
| `code` | `string` | let/var | `await fs.readFile(path.join(FIXTURES_DIR, filename), {
      encoding: 'utf-8',
    })` | ✗ |
| `optionsProjectString` | `{ project: string; cwd?: string; cacheLifetime?: { glob?: CacheDurationSeconds; }; disallowAutomaticSingleRunInference?: boolean; errorOnTypeScriptSyntacticAndSemanticIssues?: boolean; extraFileExtensions?: string[]; ... 17 more ...; suppressDeprecatedPropertyWarnings?: boolean; }` | let/var | `{
      ...options,
      project: './tsconfig.json',
    }` | ✗ |
| `optionsProjectArray` | `{ project: string[]; cwd?: string; cacheLifetime?: { glob?: CacheDurationSeconds; }; disallowAutomaticSingleRunInference?: boolean; errorOnTypeScriptSyntacticAndSemanticIssues?: boolean; extraFileExtensions?: string[]; ... 17 more ...; suppressDeprecatedPropertyWarnings?: boolean; }` | let/var | `{
      ...options,
      project: ['./tsconfig.json'],
    }` | ✗ |
| `filename` | `any` | let/var | `testFiles[0]` | ✗ |
| `code` | `string` | let/var | `await fs.readFile(path.join(FIXTURES_DIR, filename), {
      encoding: 'utf-8',
    })` | ✗ |
| `optionsAbsolutePath` | `{ project: string; cwd?: string; cacheLifetime?: { glob?: CacheDurationSeconds; }; disallowAutomaticSingleRunInference?: boolean; errorOnTypeScriptSyntacticAndSemanticIssues?: boolean; extraFileExtensions?: string[]; ... 17 more ...; suppressDeprecatedPropertyWarnings?: boolean; }` | let/var | `{
      ...options,
      project: `${__dirname}/../fixtures/semanticInfo/tsconfig.json`,
    }` | ✗ |
| `optionsRelativePath` | `{ project: string; cwd?: string; cacheLifetime?: { glob?: CacheDurationSeconds; }; disallowAutomaticSingleRunInference?: boolean; errorOnTypeScriptSyntacticAndSemanticIssues?: boolean; extraFileExtensions?: string[]; ... 17 more ...; suppressDeprecatedPropertyWarnings?: boolean; }` | let/var | `{
      ...options,
      project: `./tsconfig.json`,
    }` | ✗ |
| `declaration` | `any` | let/var | `(
        parseResult.ast.body[0] as TSESTree.VariableDeclaration
      ).declarations[0]` | ✗ |
| `arrayMember` | `any` | let/var | `(declaration.init as TSESTree.ArrayExpression)
        .elements[0]` | ✗ |
| `boundName` | `TSESTree.Identifier` | let/var | `declaration.id as TSESTree.Identifier` | ✗ |
| `declaration` | `any` | let/var | `(
        parseResult.ast.body[0] as TSESTree.VariableDeclaration
      ).declarations[0]` | ✗ |
| `arrayMember` | `any` | let/var | `(declaration.init as TSESTree.ArrayExpression)
        .elements[0]` | ✗ |
| `boundName` | `TSESTree.Identifier` | let/var | `declaration.id as TSESTree.Identifier` | ✗ |
| `binaryExpression` | `any` | let/var | `(
      parseResult.ast.body[0] as TSESTree.VariableDeclaration
    ).declarations[0].init` | ✗ |
| `computedPropertyString` | `any` | let/var | `(
      (parseResult.ast.body[1] as TSESTree.ClassDeclaration).body
        .body[0] as TSESTree.PropertyDefinition
    ).key` | ✗ |
| `arrayBoundName` | `TSESTree.Identifier` | let/var | `(
      (
        (parseResult.ast.body[1] as TSESTree.ExpressionStatement)
          .expression as TSESTree.CallExpression
      ).callee as TSESTree.MemberExpression
    ).object as TSESTree.Identifier` | ✗ |
| `boundName` | `TSESTree.Identifier` | const | `(parseResult.ast.body[0] as TSESTree.VariableDeclaration)
      .declarations[0].id as TSESTree.Identifier` | ✗ |
| `code` | `string` | let/var | `await fs.readFile(fileName, { encoding: 'utf-8' })` | ✗ |
| `code` | `string` | let/var | `await fs.readFile(fileName, { encoding: 'utf-8' })` | ✗ |
| `code` | `string` | let/var | `await fs.readFile(fileName, { encoding: 'utf-8' })` | ✗ |
| `filename` | `any` | let/var | `testFiles[0]` | ✗ |
| `code` | `string` | let/var | `await fs.readFile(path.join(FIXTURES_DIR, filename), {
        encoding: 'utf-8',
      })` | ✗ |
| `optionsProjectString` | `{ programs: any[]; project: string; cwd?: string; cacheLifetime?: { glob?: CacheDurationSeconds; }; disallowAutomaticSingleRunInference?: boolean; errorOnTypeScriptSyntacticAndSemanticIssues?: boolean; extraFileExtensions?: string[]; ... 16 more ...; suppressDeprecatedPropertyWarnings?: boolean; }` | let/var | `{
        ...options,
        programs: [program1, program2],
        project: './tsconfig.json',
      }` | ✗ |
| `filename` | `"non-existent-file.ts"` | const | `'non-existent-file.ts'` | ✗ |
| `optionsWithProjectTrue` | `{ programs: any; project: boolean; cwd?: string; cacheLifetime?: { glob?: CacheDurationSeconds; }; disallowAutomaticSingleRunInference?: boolean; errorOnTypeScriptSyntacticAndSemanticIssues?: boolean; extraFileExtensions?: string[]; ... 16 more ...; suppressDeprecatedPropertyWarnings?: boolean; }` | const | `{
        ...options,
        programs: undefined,
        project: true,
      }` | ✗ |
| `filename` | `"non-existent-file.ts"` | const | `'non-existent-file.ts'` | ✗ |
| `optionsWithSingleProgram` | `{ programs: ts.Program[]; cwd?: string; cacheLifetime?: { glob?: CacheDurationSeconds; }; disallowAutomaticSingleRunInference?: boolean; errorOnTypeScriptSyntacticAndSemanticIssues?: boolean; extraFileExtensions?: string[]; filePath?: string; ... 16 more ...; suppressDeprecatedPropertyWarnings?: boolean; }` | const | `{
      ...options,
      programs: [program],
    }` | ✗ |
| `filename` | `"non-existent-file.ts"` | const | `'non-existent-file.ts'` | ✗ |
| `optionsWithSingleProgram` | `{ programs: ts.Program[]; cwd?: string; cacheLifetime?: { glob?: CacheDurationSeconds; }; disallowAutomaticSingleRunInference?: boolean; errorOnTypeScriptSyntacticAndSemanticIssues?: boolean; extraFileExtensions?: string[]; filePath?: string; ... 16 more ...; suppressDeprecatedPropertyWarnings?: boolean; }` | const | `{
      ...options,
      programs: [program1],
    }` | ✗ |
| `optionsWithMultiplePrograms` | `{ programs: any[]; cwd?: string; cacheLifetime?: { glob?: CacheDurationSeconds; }; disallowAutomaticSingleRunInference?: boolean; errorOnTypeScriptSyntacticAndSemanticIssues?: boolean; extraFileExtensions?: string[]; ... 17 more ...; suppressDeprecatedPropertyWarnings?: boolean; }` | const | `{
      ...options,
      programs: [program1, program2],
    }` | ✗ |


---

## Functions

### `createOptions(fileName: string): { cwd?: string } & TSESTreeOptions`

<details><summary>Code</summary>

```ts
function createOptions(fileName: string): { cwd?: string } & TSESTreeOptions {
  return {
    comment: true,
    disallowAutomaticSingleRunInference: true,
    errorOnUnknownASTType: true,
    filePath: fileName,
    jsx: false,
    loc: true,
    loggerFn: false,
    project: `./tsconfig.json`,
    range: true,
    tokens: true,
    tsconfigRootDir: FIXTURES_DIR,
  };
}
```
</details>

- **Parameters**:
  - `fileName: string`
- **Return Type**: `{ cwd?: string } & TSESTreeOptions`

---