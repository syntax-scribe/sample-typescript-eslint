[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `integration-test-base.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 4 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Async/Await Patterns](#asyncawait-patterns)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/integration-tests/tools/integration-test-base.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `execFile` | `./pack-packages.js` |
| `FIXTURES_DESTINATION_DIR` | `./pack-packages.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `stderr` | `string` | let/var | `''` | ✗ |


---

## Async/Await Patterns

| Type | Function | Await Expressions | Promise Chains |
|------|----------|-------------------|----------------|
| await-expression | `integrationTest` | executeTest(testFolder) | *none* |
| await-expression | `eslintIntegrationTest` | execFile(
        'yarn',
        [
          'eslint',
          '--format',
          'json',
          '--output-file',
          outFile,
          '--fix-dry-run',
          filesGlob,
        ],
        {
          cwd: testFolder,
          shell: true,
        },
      ), fs.readFile(outFile, { encoding: 'utf-8' }) | *none* |
| promise-chain | `typescriptIntegrationTest` | *none* | Promise.allSettled |
| await-expression | `typescriptIntegrationTest` | Promise.allSettled([
      execFile('yarn', ['tsc', '--noEmit', '--skipLibCheck', ...tscArgs], {
        cwd: testFolder,
        shell: true,
      }),
    ]) | *none* |


---

## Functions

### `integrationTest(testName: string, testFilename: string, executeTest: (testFolder: string) => Promise<void>): void`

<details><summary>Code</summary>

```ts
function integrationTest(
  testName: string,
  testFilename: string,
  executeTest: (testFolder: string) => Promise<void>,
): void {
  const fixture = path.parse(testFilename).name.replace('.test', '');

  const testFolder = path.join(FIXTURES_DESTINATION_DIR, fixture);

  describe(fixture, () => {
    describe(testName, () => {
      it('should work successfully', async () => {
        await executeTest(testFolder);
      });
    });
  });
}
```
</details>

- **Parameters**:
  - `testName: string`
  - `testFilename: string`
  - `executeTest: (testFolder: string) => Promise<void>`
- **Return Type**: `void`
- **Calls**:
  - `path.parse(testFilename).name.replace`
  - `path.join`
  - `describe`
  - `it`
  - `executeTest`
### `eslintIntegrationTest(testFilename: string, filesGlob: string): void`

<details><summary>Code</summary>

```ts
export function eslintIntegrationTest(
  testFilename: string,
  filesGlob: string,
): void {
  integrationTest('eslint', testFilename, async testFolder => {
    // lint, outputting to a JSON file
    const outFile = path.join(testFolder, 'eslint.json');

    let stderr = '';
    try {
      await execFile(
        'yarn',
        [
          'eslint',
          '--format',
          'json',
          '--output-file',
          outFile,
          '--fix-dry-run',
          filesGlob,
        ],
        {
          cwd: testFolder,
          shell: true,
        },
      );
    } catch (ex) {
      // we expect eslint will "fail" because we have intentional lint errors

      // useful for debugging
      if (typeof ex === 'object' && ex != null && 'stderr' in ex) {
        stderr = String(ex.stderr);
      }
    }
    // console.log('Lint complete.');
    expect(stderr).toHaveLength(0);

    // assert the linting state is consistent
    const lintOutputRAW = (await fs.readFile(outFile, { encoding: 'utf-8' }))
      // clean the output to remove any changing facets so tests are stable
      .replaceAll(
        new RegExp(`"filePath": ?"(/private)?${testFolder}`, 'g'),
        '"filePath": "<root>',
      )
      .replaceAll(
        /"filePath":"([^"]*)"/g,
        (_, testFile: string) =>
          `"filePath": "<root>/${path.relative(testFolder, testFile)}"`,
      )
      .replaceAll(/C:\\\\(usr)\\\\(linked)\\\\(tsconfig.json)/g, '/$1/$2/$3');
    try {
      const lintOutput = JSON.parse(lintOutputRAW);
      expect(lintOutput).toMatchSnapshot();
    } catch {
      throw new Error(
        `Lint output could not be parsed as JSON: \`${lintOutputRAW}\`.`,
      );
    }
  });
}
```
</details>

- **Parameters**:
  - `testFilename: string`
  - `filesGlob: string`
- **Return Type**: `void`
- **Calls**:
  - `integrationTest`
  - `path.join`
  - `execFile (from ./pack-packages.js)`
  - `String`
  - `expect(stderr).toHaveLength`
  - `(await fs.readFile(outFile, { encoding: 'utf-8' }))
      // clean the output to remove any changing facets so tests are stable
      .replaceAll(
        new RegExp(`"filePath": ?"(/private)?${testFolder}`, 'g'),
        '"filePath": "<root>',
      )
      .replaceAll(
        /"filePath":"([^"]*)"/g,
        (_, testFile: string) =>
          `"filePath": "<root>/${path.relative(testFolder, testFile)}"`,
      )
      .replaceAll`
  - `JSON.parse`
  - `expect(lintOutput).toMatchSnapshot`
- **Internal Comments**:
```
// lint, outputting to a JSON file (x2)
// we expect eslint will "fail" because we have intentional lint errors
// useful for debugging
// console.log('Lint complete.'); (x5)
// assert the linting state is consistent (x2)
```

### `typescriptIntegrationTest(testName: string, testFilename: string, tscArgs: string[], assertOutput: (out: string) => void): void`

<details><summary>Code</summary>

```ts
export function typescriptIntegrationTest(
  testName: string,
  testFilename: string,
  tscArgs: string[],
  assertOutput: (out: string) => void,
): void {
  integrationTest(testName, testFilename, async testFolder => {
    const [result] = await Promise.allSettled([
      execFile('yarn', ['tsc', '--noEmit', '--skipLibCheck', ...tscArgs], {
        cwd: testFolder,
        shell: true,
      }),
    ]);

    if (result.status === 'rejected') {
      // this looks weird - but it means that we can show the stdout (the errors)
      // in the test output when typescript fails which helps with debugging
      assertOutput(
        (result.reason as { stdout: string }).stdout.replace(
          // on macos the tmp path might be shown by TS with `/private/`, but
          // the tmp util does not include that prefix folder
          new RegExp(`(/private)?${testFolder}`),
          '/<tmp_folder>',
        ),
      );
    } else {
      // TS logs nothing when it succeeds
      expect(result.value.stdout).toBe('');
      expect(result.value.stderr).toBe('');
    }
  });
}
```
</details>

- **Parameters**:
  - `testName: string`
  - `testFilename: string`
  - `tscArgs: string[]`
  - `assertOutput: (out: string) => void`
- **Return Type**: `void`
- **Calls**:
  - `integrationTest`
  - `Promise.allSettled`
  - `execFile (from ./pack-packages.js)`
  - `assertOutput`
  - `(result.reason as { stdout: string }).stdout.replace`
  - `expect(result.value.stdout).toBe`
  - `expect(result.value.stderr).toBe`
- **Internal Comments**:
```
// this looks weird - but it means that we can show the stdout (the errors) (x3)
// in the test output when typescript fails which helps with debugging (x3)
// on macos the tmp path might be shown by TS with `/private/`, but
// the tmp util does not include that prefix folder
// TS logs nothing when it succeeds (x5)
```


---