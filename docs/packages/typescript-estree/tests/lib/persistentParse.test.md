[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `persistentParse.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 8 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 32 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 7 |
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
📂 **`packages/typescript-estree/tests/lib/persistentParse.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `fs` | `node:fs/promises` |
| `path` | `node:path` |
| `clearCaches` | `../../src/clear-caches` |
| `clearWatchCaches` | `../../src/create-program/getWatchProgramsForProjects` |
| `clearDefaultProjectMatchedFiles` | `../../src/parser` |
| `parseAndGenerateServices` | `../../src/parser` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `CONTENTS` | `{ bar: string; 'bat/baz/bar': string; 'baz/bar': string; foo: string; number: string; object: string; string: string; }` | const | `{
  bar: 'console.log("bar")',
  'bat/baz/bar': 'console.log("bat/baz/bar")',
  'baz/bar': 'console.log("baz bar")',
  foo: 'console.log("foo")',
  number: 'const foo = 1;',
  object: '(() => { })();',
  string: 'let a: "a" | "b";',
}` | ✗ |
| `homeOrTmpDir` | `string` | const | `os.tmpdir() || os.homedir()` | ✗ |
| `tmpDirs` | `Set<string>` | const | `new Set<string>()` | ✗ |
| `tmpDir` | `string` | let/var | `await fs.mkdtemp(`${tmpDirsParentDirectory}/`, {
    encoding: 'utf-8',
  })` | ✗ |
| `tmpDir` | `string` | let/var | `await createTmpDir()` | ✗ |
| `PROJECT_DIR` | `string` | let/var | `await setup(tsConfigIncludeAll)` | ✗ |
| `PROJECT_DIR` | `string` | let/var | `await setup(tsConfigExcludeBar)` | ✗ |
| `PROJECT_DIR` | `string` | let/var | `await setup(tsConfigIncludeAll, false)` | ✗ |
| `PROJECT_DIR` | `string` | let/var | `await setup(tsConfigIncludeAll, false)` | ✗ |
| `bazSlashBar` | `"baz/bar"` | let/var | `'baz/bar'` | ✗ |
| `PROJECT_DIR` | `string` | let/var | `await setup(tsConfigIncludeAll)` | ✗ |
| `bazSlashBar` | `"bat/baz/bar"` | let/var | `'bat/baz/bar'` | ✗ |
| `PROJECT_DIR` | `string` | let/var | `await setup(tsConfigIncludeAll, true)` | ✗ |
| `bazSlashBar` | `"baz/bar"` | let/var | `'baz/bar'` | ✗ |
| `PROJECT_DIR` | `string` | let/var | `await setup(tsConfigExcludeBar)` | ✗ |
| `PROJECT_DIR` | `string` | let/var | `await setup(tsConfigIncludeAll, false)` | ✗ |
| `PROJECT_DIR` | `string` | let/var | `await setup(tsConfigIncludeAll, false)` | ✗ |
| `tsConfigExcludeBar` | `{ exclude: string[]; include: string[]; }` | const | `{
        exclude: ['./src/bar.ts'],
        include: ['src'],
      }` | ✗ |
| `tsConfigIncludeAll` | `{ exclude: any[]; include: string[]; }` | const | `{
        exclude: [],
        include: ['src'],
      }` | ✗ |
| `tsConfigExcludeBar` | `{ exclude: string[]; include: string[]; }` | const | `{
        exclude: ['./src/bar.ts'],
        include: ['src/'],
      }` | ✗ |
| `tsConfigIncludeAll` | `{ exclude: any[]; include: string[]; }` | const | `{
        exclude: [],
        include: ['src/'],
      }` | ✗ |
| `tsConfigExcludeBar` | `{ exclude: string[]; }` | const | `{
        exclude: ['./src/bar.ts'],
      }` | ✗ |
| `tsConfigIncludeAll` | `{}` | const | `{}` | ✗ |
| `PROJECT_DIR` | `string` | let/var | `await setup({}, false)` | ✗ |
| `PROJECT_DIR` | `string` | let/var | `await setup({}, false)` | ✗ |
| `bazSlashBar` | `"baz/bar"` | let/var | `'baz/bar'` | ✗ |
| `tsConfigExcludeBar` | `{ exclude: string[]; include: string[]; }` | const | `{
        exclude: ['./src/bar.ts'],
        include: ['./*', './**/*', './src/**/*'],
      }` | ✗ |
| `tsConfigIncludeAll` | `{ include: string[]; }` | const | `{
        include: ['./*', './**/*', './src/**/*'],
      }` | ✗ |
| `moduleTypes` | `readonly ["None", "CommonJS", "AMD", "System", "UMD", "ES6", "ES2015", "ESNext"]` | const | `[
      'None',
      'CommonJS',
      'AMD',
      'System',
      'UMD',
      'ES6',
      'ES2015',
      'ESNext',
    ] as const` | ✗ |
| `testNames` | `readonly ["object", "number", "string", "foo"]` | const | `['object', 'number', 'string', 'foo'] as const` | ✗ |
| `tsConfigIncludeAll` | `{ compilerOptions: { module: any; }; include: string[]; }` | const | `{
        compilerOptions: { module },
        include: ['./**/*'],
      }` | ✗ |
| `PROJECT_DIR` | `string` | let/var | `await setup(tsConfigIncludeAll)` | ✗ |


---

## Async/Await Patterns

| Type | Function | Await Expressions | Promise Chains |
|------|----------|-------------------|----------------|
| async-function | `writeTSConfig` | fs.writeFile(
    path.join(dirName, 'tsconfig.json'),
    JSON.stringify(config, null, 2),
    { encoding: 'utf-8' },
  ) | *none* |
| async-function | `writeFile` | fs.writeFile(
    path.join(dirName, 'src', `${file}.ts`),
    CONTENTS[file],
    'utf-8',
  ) | *none* |
| async-function | `renameFile` | fs.rename(
    path.join(dirName, 'src', `${src}.ts`),
    path.join(dirName, 'src', `${dest}.ts`),
  ) | *none* |
| async-function | `createTmpDir` | fs.mkdtemp(`${tmpDirsParentDirectory}/`, {
    encoding: 'utf-8',
  }) | *none* |
| async-function | `setup` | createTmpDir(), writeTSConfig(tmpDir, tsconfig), fs.mkdir(path.join(tmpDir, 'src'), { recursive: true }), fs.mkdir(path.join(tmpDir, 'src', 'baz'), { recursive: true }), writeFile(tmpDir, 'foo'), writeFile(tmpDir, 'bar') | *none* |
| async-function | `exists` | fs.lstat(path.join(tmpDir, 'src', `${filename}.ts`)) | *none* |
| await-expression | `baseTests` | setup(tsConfigIncludeAll), setup(tsConfigExcludeBar), setup(tsConfigIncludeAll, false), writeFile(PROJECT_DIR, 'bar'), setup(tsConfigIncludeAll, false), writeFile(PROJECT_DIR, bazSlashBar), setup(tsConfigIncludeAll), fs.mkdir(path.join(PROJECT_DIR, 'src', 'bat'), { recursive: true }), fs.mkdir(path.join(PROJECT_DIR, 'src', 'bat', 'baz'), {
      recursive: true,
    }), writeFile(PROJECT_DIR, bazSlashBar), setup(tsConfigIncludeAll, true), renameFile(PROJECT_DIR, 'bar', bazSlashBar), setup(tsConfigExcludeBar), writeTSConfig(PROJECT_DIR, tsConfigIncludeAll), setup(tsConfigIncludeAll, false), writeFile(PROJECT_DIR, 'bar'), expect(exists('bar', PROJECT_DIR)).resolves.toBe(true), setup(tsConfigIncludeAll, false), writeFile(PROJECT_DIR, 'bar'), expect(exists('bar')).resolves.toBe(true), expect(exists('bar', PROJECT_DIR)).resolves.toBe(true) | *none* |


---

## Functions

### `writeTSConfig(dirName: string, config: Record<string, unknown>): Promise<void>`

<details><summary>Code</summary>

```ts
async function writeTSConfig(
  dirName: string,
  config: Record<string, unknown>,
): Promise<void> {
  await fs.writeFile(
    path.join(dirName, 'tsconfig.json'),
    JSON.stringify(config, null, 2),
    { encoding: 'utf-8' },
  );
}
```
</details>

- **Parameters**:
  - `dirName: string`
  - `config: Record<string, unknown>`
- **Return Type**: `Promise<void>`
- **Calls**:
  - `fs.writeFile`
  - `path.join`
  - `JSON.stringify`
### `writeFile(dirName: string, file: keyof typeof CONTENTS): Promise<void>`

<details><summary>Code</summary>

```ts
async function writeFile(
  dirName: string,
  file: keyof typeof CONTENTS,
): Promise<void> {
  await fs.writeFile(
    path.join(dirName, 'src', `${file}.ts`),
    CONTENTS[file],
    'utf-8',
  );
}
```
</details>

- **Parameters**:
  - `dirName: string`
  - `file: keyof typeof CONTENTS`
- **Return Type**: `Promise<void>`
- **Calls**:
  - `fs.writeFile`
  - `path.join`
### `renameFile(dirName: string, src: 'bar', dest: 'baz/bar'): Promise<void>`

<details><summary>Code</summary>

```ts
async function renameFile(
  dirName: string,
  src: 'bar',
  dest: 'baz/bar',
): Promise<void> {
  await fs.rename(
    path.join(dirName, 'src', `${src}.ts`),
    path.join(dirName, 'src', `${dest}.ts`),
  );
}
```
</details>

- **Parameters**:
  - `dirName: string`
  - `src: 'bar'`
  - `dest: 'baz/bar'`
- **Return Type**: `Promise<void>`
- **Calls**:
  - `fs.rename`
  - `path.join`
### `createTmpDir(): Promise<string>`

<details><summary>Code</summary>

```ts
async function createTmpDir(): Promise<string> {
  const tmpDir = await fs.mkdtemp(`${tmpDirsParentDirectory}/`, {
    encoding: 'utf-8',
  });
  tmpDirs.add(tmpDir);
  return tmpDir;
}
```
</details>

- **Return Type**: `Promise<string>`
- **Calls**:
  - `fs.mkdtemp`
  - `tmpDirs.add`
### `setup(tsconfig: Record<string, unknown>, writeBar: boolean): Promise<string>`

<details><summary>Code</summary>

```ts
async function setup(
  tsconfig: Record<string, unknown>,
  writeBar = true,
): Promise<string> {
  const tmpDir = await createTmpDir();

  await writeTSConfig(tmpDir, tsconfig);

  await fs.mkdir(path.join(tmpDir, 'src'), { recursive: true });
  await fs.mkdir(path.join(tmpDir, 'src', 'baz'), { recursive: true });
  await writeFile(tmpDir, 'foo');
  if (writeBar) {
    await writeFile(tmpDir, 'bar');
  }

  return tmpDir;
}
```
</details>

- **Parameters**:
  - `tsconfig: Record<string, unknown>`
  - `writeBar: boolean`
- **Return Type**: `Promise<string>`
- **Calls**:
  - `createTmpDir`
  - `writeTSConfig`
  - `fs.mkdir`
  - `path.join`
  - `writeFile`
### `parseFile(filename: keyof typeof CONTENTS, tmpDir: string, relative: boolean, ignoreTsconfigRootDir: boolean): void`

<details><summary>Code</summary>

```ts
function parseFile(
  filename: keyof typeof CONTENTS,
  tmpDir: string,
  relative?: boolean,
  ignoreTsconfigRootDir?: boolean,
): void {
  parseAndGenerateServices(CONTENTS[filename], {
    disallowAutomaticSingleRunInference: true,
    filePath: relative
      ? path.join('src', `${filename}.ts`)
      : path.join(tmpDir, 'src', `${filename}.ts`),
    project: './tsconfig.json',
    tsconfigRootDir: ignoreTsconfigRootDir ? undefined : tmpDir,
  });
}
```
</details>

- **Parameters**:
  - `filename: keyof typeof CONTENTS`
  - `tmpDir: string`
  - `relative: boolean`
  - `ignoreTsconfigRootDir: boolean`
- **Return Type**: `void`
- **Calls**:
  - `parseAndGenerateServices (from ../../src/parser)`
  - `path.join`
### `exists(filename: keyof typeof CONTENTS, tmpDir: string): Promise<boolean>`

<details><summary>Code</summary>

```ts
async function exists(
  filename: keyof typeof CONTENTS,
  tmpDir = '',
): Promise<boolean> {
  return (await fs.lstat(path.join(tmpDir, 'src', `${filename}.ts`))).isFile();
}
```
</details>

- **Parameters**:
  - `filename: keyof typeof CONTENTS`
  - `tmpDir: string`
- **Return Type**: `Promise<boolean>`
- **Calls**:
  - `(await fs.lstat(path.join(tmpDir, 'src', `${filename}.ts`))).isFile`
  - `fs.lstat`
  - `path.join`
### `baseTests(tsConfigExcludeBar: Record<string, unknown>, tsConfigIncludeAll: Record<string, unknown>): void`

<details><summary>Code</summary>

```ts
function baseTests(
  tsConfigExcludeBar: Record<string, unknown>,
  tsConfigIncludeAll: Record<string, unknown>,
): void {
  it('parses both files successfully when included', async () => {
    const PROJECT_DIR = await setup(tsConfigIncludeAll);

    expect(() => parseFile('foo', PROJECT_DIR)).not.toThrow();
    expect(() => parseFile('bar', PROJECT_DIR)).not.toThrow();
  });

  it('parses included files, and throws on excluded files', async () => {
    const PROJECT_DIR = await setup(tsConfigExcludeBar);

    expect(() => parseFile('foo', PROJECT_DIR)).not.toThrow();
    expect(() => parseFile('bar', PROJECT_DIR)).toThrow();
  });

  it('allows parsing of new files', async () => {
    const PROJECT_DIR = await setup(tsConfigIncludeAll, false);

    // parse once to: assert the config as correct, and to make sure the program is setup
    expect(() => parseFile('foo', PROJECT_DIR)).not.toThrow();
    // bar should throw because it doesn't exist yet
    expect(() => parseFile('bar', PROJECT_DIR)).toThrow();

    // write a new file and attempt to parse it
    await writeFile(PROJECT_DIR, 'bar');

    // both files should parse fine now
    expect(() => parseFile('foo', PROJECT_DIR)).not.toThrow();
    expect(() => parseFile('bar', PROJECT_DIR)).not.toThrow();
  });

  it('allows parsing of deeply nested new files', async () => {
    const PROJECT_DIR = await setup(tsConfigIncludeAll, false);
    const bazSlashBar = 'baz/bar';

    // parse once to: assert the config as correct, and to make sure the program is setup
    expect(() => parseFile('foo', PROJECT_DIR)).not.toThrow();
    // bar should throw because it doesn't exist yet
    expect(() => parseFile(bazSlashBar, PROJECT_DIR)).toThrow();

    // write a new file and attempt to parse it
    await writeFile(PROJECT_DIR, bazSlashBar);

    // both files should parse fine now
    expect(() => parseFile('foo', PROJECT_DIR)).not.toThrow();
    expect(() => parseFile(bazSlashBar, PROJECT_DIR)).not.toThrow();
  });

  it('allows parsing of deeply nested new files in new folder', async () => {
    const PROJECT_DIR = await setup(tsConfigIncludeAll);

    expect(() => parseFile('foo', PROJECT_DIR)).not.toThrow();

    // Create deep folder structure after first parse (this is important step)
    // context: https://github.com/typescript-eslint/typescript-eslint/issues/1394
    await fs.mkdir(path.join(PROJECT_DIR, 'src', 'bat'), { recursive: true });
    await fs.mkdir(path.join(PROJECT_DIR, 'src', 'bat', 'baz'), {
      recursive: true,
    });

    const bazSlashBar = 'bat/baz/bar';

    // write a new file and attempt to parse it
    await writeFile(PROJECT_DIR, bazSlashBar);

    expect(() => parseFile(bazSlashBar, PROJECT_DIR)).not.toThrow();
  });

  it('allows renaming of files', async () => {
    const PROJECT_DIR = await setup(tsConfigIncludeAll, true);
    const bazSlashBar = 'baz/bar';

    // parse once to: assert the config as correct, and to make sure the program is setup
    expect(() => parseFile('foo', PROJECT_DIR)).not.toThrow();
    // bar should throw because it doesn't exist yet
    expect(() => parseFile(bazSlashBar, PROJECT_DIR)).toThrow();

    // write a new file and attempt to parse it
    await renameFile(PROJECT_DIR, 'bar', bazSlashBar);

    // both files should parse fine now
    expect(() => parseFile('foo', PROJECT_DIR)).not.toThrow();
    expect(() => parseFile(bazSlashBar, PROJECT_DIR)).not.toThrow();
  });

  it('reacts to changes in the tsconfig', async () => {
    const PROJECT_DIR = await setup(tsConfigExcludeBar);

    // parse once to: assert the config as correct, and to make sure the program is setup
    expect(() => parseFile('foo', PROJECT_DIR)).not.toThrow();
    expect(() => parseFile('bar', PROJECT_DIR)).toThrow();

    // change the config file so it now includes all files
    await writeTSConfig(PROJECT_DIR, tsConfigIncludeAll);
    clearCaches();

    expect(() => parseFile('foo', PROJECT_DIR)).not.toThrow();
    expect(() => parseFile('bar', PROJECT_DIR)).not.toThrow();
  });

  it('should work with relative paths', async () => {
    const PROJECT_DIR = await setup(tsConfigIncludeAll, false);

    // parse once to: assert the config as correct, and to make sure the program is setup
    expect(() => parseFile('foo', PROJECT_DIR, true)).not.toThrow();
    // bar should throw because it doesn't exist yet
    expect(() => parseFile('bar', PROJECT_DIR, true)).toThrow();

    // write a new file and attempt to parse it
    await writeFile(PROJECT_DIR, 'bar');

    // make sure that file is correctly created
    await expect(exists('bar', PROJECT_DIR)).resolves.toBe(true);

    // both files should parse fine now
    expect(() => parseFile('foo', PROJECT_DIR, true)).not.toThrow();
    expect(() => parseFile('bar', PROJECT_DIR, true)).not.toThrow();
  });

  it('should work with relative paths without tsconfig root', async () => {
    const PROJECT_DIR = await setup(tsConfigIncludeAll, false);
    process.chdir(PROJECT_DIR);

    // parse once to: assert the config as correct, and to make sure the program is setup
    expect(() => parseFile('foo', PROJECT_DIR, true, true)).not.toThrow();
    // bar should throw because it doesn't exist yet
    expect(() => parseFile('bar', PROJECT_DIR, true, true)).toThrow();

    // write a new file and attempt to parse it
    await writeFile(PROJECT_DIR, 'bar');

    // make sure that file is correctly created
    await expect(exists('bar')).resolves.toBe(true);
    await expect(exists('bar', PROJECT_DIR)).resolves.toBe(true);

    // both files should parse fine now
    expect(() => parseFile('foo', PROJECT_DIR, true, true)).not.toThrow();
    expect(() => parseFile('bar', PROJECT_DIR, true, true)).not.toThrow();
  });
}
```
</details>

- **Parameters**:
  - `tsConfigExcludeBar: Record<string, unknown>`
  - `tsConfigIncludeAll: Record<string, unknown>`
- **Return Type**: `void`
- **Calls**:
  - `it`
  - `setup`
  - `expect(() => parseFile('foo', PROJECT_DIR)).not.toThrow`
  - `expect(() => parseFile('bar', PROJECT_DIR)).not.toThrow`
  - `expect(() => parseFile('bar', PROJECT_DIR)).toThrow`
  - `writeFile`
  - `expect(() => parseFile(bazSlashBar, PROJECT_DIR)).toThrow`
  - `expect(() => parseFile(bazSlashBar, PROJECT_DIR)).not.toThrow`
  - `fs.mkdir`
  - `path.join`
  - `renameFile`
  - `writeTSConfig`
  - `clearCaches (from ../../src/clear-caches)`
  - `expect(() => parseFile('foo', PROJECT_DIR, true)).not.toThrow`
  - `expect(() => parseFile('bar', PROJECT_DIR, true)).toThrow`
  - `expect(exists('bar', PROJECT_DIR)).resolves.toBe`
  - `expect(() => parseFile('bar', PROJECT_DIR, true)).not.toThrow`
  - `process.chdir`
  - `expect(() => parseFile('foo', PROJECT_DIR, true, true)).not.toThrow`
  - `expect(() => parseFile('bar', PROJECT_DIR, true, true)).toThrow`
  - `expect(exists('bar')).resolves.toBe`
  - `expect(() => parseFile('bar', PROJECT_DIR, true, true)).not.toThrow`
- **Internal Comments**:
```
// parse once to: assert the config as correct, and to make sure the program is setup (x36)
// bar should throw because it doesn't exist yet (x25)
// write a new file and attempt to parse it (x12)
// both files should parse fine now (x30)
// Create deep folder structure after first parse (this is important step) (x2)
// context: https://github.com/typescript-eslint/typescript-eslint/issues/1394 (x2)
// change the config file so it now includes all files (x2)
// make sure that file is correctly created (x4)
```


---