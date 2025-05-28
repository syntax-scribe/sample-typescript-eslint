[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `pack-packages.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 9 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 2 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Async/Await Patterns](#asyncawait-patterns)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/integration-tests/tools/pack-packages.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TestProject` | `vitest/node` |
| `pathToFileURL` | `node:url` |
| `promisify` | `node:util` |
| `rootPackageJson` | `../../../package.json` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `FIXTURES_DIR_BASENAME` | `"fixtures"` | const | `'fixtures'` | ✗ |
| `YARN_RC_CONTENT` | `"nodeLinker: node-modules\n\nenableGlobalCache: true\n"` | const | `'nodeLinker: node-modules\n\nenableGlobalCache: true\n'` | ✗ |
| `PACKAGES` | `Dirent<string>[]` | let/var | `await fs.readdir(PACKAGES_DIR, {
    encoding: 'utf-8',
    withFileTypes: true,
  })` | ✗ |
| `packageJson` | `PackageJSON` | let/var | `(
            await import(pathToFileURL(packagePath).href, {
              with: { type: 'json' },
            })
          ).default` | ✗ |
| `result` | `{ stdout: string; stderr: string; }` | let/var | `await execFile('npm', ['pack', packageDir], {
            cwd: TAR_FOLDER,
            encoding: 'utf-8',
            shell: true,
          })` | ✗ |
| `tarball` | `string` | let/var | `stdoutLines[stdoutLines.length - 1]` | ✗ |
| `BASE_DEPENDENCIES` | `PackageJSON['devDependencies']` | let/var | `{
    ...tseslintPackages,
    eslint: rootPackageJson.devDependencies.eslint,
    typescript: rootPackageJson.devDependencies.typescript,
    vitest: rootPackageJson.devDependencies.vitest,
  }` | ✗ |
| `temp` | `string` | let/var | `await fs.mkdtemp(path.join(INTEGRATION_TEST_DIR, 'temp'), {
    encoding: 'utf-8',
  })` | ✗ |
| `fixturePackageJson` | `PackageJSON` | let/var | `(
        await import(
          pathToFileURL(path.join(fixtureDir, 'package.json')).href,
          { with: { type: 'json' } }
        )
      ).default` | ✗ |


---

## Async/Await Patterns

| Type | Function | Await Expressions | Promise Chains |
|------|----------|-------------------|----------------|
| async-function | `setup` | project.globTestFiles(project.vitest.state.getPaths()), fs.readdir(PACKAGES_DIR, {
    encoding: 'utf-8',
    withFileTypes: true,
  }), fs.mkdir(FIXTURES_DESTINATION_DIR, { recursive: true }), fs.mkdir(TAR_FOLDER, { recursive: true }), Promise.all(
        PACKAGES.map(async ({ name: pkg }) => {
          const packageDir = path.join(PACKAGES_DIR, pkg);
          const packagePath = path.join(packageDir, 'package.json');

          try {
            if (!(await fs.lstat(packagePath)).isFile()) {
              return;
            }
          } catch {
            return;
          }

          const packageJson: PackageJSON = (
            await import(pathToFileURL(packagePath).href, {
              with: { type: 'json' },
            })
          ).default;

          if ('private' in packageJson && packageJson.private === true) {
            return;
          }

          const result = await execFile('npm', ['pack', packageDir], {
            cwd: TAR_FOLDER,
            encoding: 'utf-8',
            shell: true,
          });

          if (typeof result.stdout !== 'string') {
            return;
          }

          const stdoutLines = result.stdout.trim().split('\n');
          const tarball = stdoutLines[stdoutLines.length - 1];

          return [
            packageJson.name,
            `file:${path.join(TAR_FOLDER, tarball)}`,
          ] as const;
        }),
      ), fs.lstat(packagePath), import(pathToFileURL(packagePath).href, {
              with: { type: 'json' },
            }), execFile('npm', ['pack', packageDir], {
            cwd: TAR_FOLDER,
            encoding: 'utf-8',
            shell: true,
          }), fs.mkdtemp(path.join(INTEGRATION_TEST_DIR, 'temp'), {
    encoding: 'utf-8',
  }), fs.writeFile(path.join(temp, '.yarnrc.yml'), YARN_RC_CONTENT, {
    encoding: 'utf-8',
  }), fs.writeFile(
    path.join(temp, 'package.json'),
    JSON.stringify(
      {
        devDependencies: BASE_DEPENDENCIES,
        packageManager: rootPackageJson.packageManager,
        private: true,
        resolutions: tseslintPackages,
      },
      null,
      2,
    ),
    { encoding: 'utf-8' },
  ), execFile('yarn', ['install', '--no-immutable'], {
    cwd: temp,
    shell: true,
  }), Promise.all(
    testFileBaseNames.map(async fixture => {
      const testFolder = path.join(FIXTURES_DESTINATION_DIR, fixture);

      const fixtureDir = path.join(FIXTURES_DIR, fixture);

      const fixturePackageJson: PackageJSON = (
        await import(
          pathToFileURL(path.join(fixtureDir, 'package.json')).href,
          { with: { type: 'json' } }
        )
      ).default;

      await fs.cp(fixtureDir, testFolder, { recursive: true });

      await fs.writeFile(
        path.join(testFolder, 'package.json'),
        JSON.stringify(
          {
            private: true,
            ...fixturePackageJson,
            devDependencies: {
              ...BASE_DEPENDENCIES,
              ...fixturePackageJson.devDependencies,
            },

            packageManager: rootPackageJson.packageManager,

            // ensure everything uses the locally packed versions instead of the NPM versions
            resolutions: {
              ...tseslintPackages,
            },
          },
          null,
          2,
        ),
        { encoding: 'utf-8' },
      );

      await fs.writeFile(
        path.join(testFolder, '.yarnrc.yml'),
        YARN_RC_CONTENT,
        { encoding: 'utf-8' },
      );

      const { stderr, stdout } = await execFile(
        'yarn',
        ['install', '--no-immutable'],
        {
          cwd: testFolder,
          shell: true,
        },
      );

      if (stderr) {
        console.error(stderr);

        if (stdout) {
          console.log(stdout);
        }
      }
    }),
  ), import(
          pathToFileURL(path.join(fixtureDir, 'package.json')).href,
          { with: { type: 'json' } }
        ), fs.cp(fixtureDir, testFolder, { recursive: true }), fs.writeFile(
        path.join(testFolder, 'package.json'),
        JSON.stringify(
          {
            private: true,
            ...fixturePackageJson,
            devDependencies: {
              ...BASE_DEPENDENCIES,
              ...fixturePackageJson.devDependencies,
            },

            packageManager: rootPackageJson.packageManager,

            // ensure everything uses the locally packed versions instead of the NPM versions
            resolutions: {
              ...tseslintPackages,
            },
          },
          null,
          2,
        ),
        { encoding: 'utf-8' },
      ), fs.writeFile(
        path.join(testFolder, '.yarnrc.yml'),
        YARN_RC_CONTENT,
        { encoding: 'utf-8' },
      ), execFile(
        'yarn',
        ['install', '--no-immutable'],
        {
          cwd: testFolder,
          shell: true,
        },
      ), fs.rm(temp, { recursive: true }) | Promise.all, Promise.all |
| async-function | `teardown` | fs.rm(INTEGRATION_TEST_DIR, { recursive: true }) | *none* |


---

## Functions

### `setup(project: TestProject): Promise<void>`

<details><summary>Code</summary>

```ts
async (project: TestProject): Promise<void> => {
  const testFileBaseNames = (
    await project.globTestFiles(project.vitest.state.getPaths())
  ).testFiles.map(testFilePath => path.basename(testFilePath, '.test.ts'));

  const PACKAGES = await fs.readdir(PACKAGES_DIR, {
    encoding: 'utf-8',
    withFileTypes: true,
  });

  await fs.mkdir(FIXTURES_DESTINATION_DIR, { recursive: true });

  await fs.mkdir(TAR_FOLDER, { recursive: true });

  const tseslintPackages = Object.fromEntries(
    (
      await Promise.all(
        PACKAGES.map(async ({ name: pkg }) => {
          const packageDir = path.join(PACKAGES_DIR, pkg);
          const packagePath = path.join(packageDir, 'package.json');

          try {
            if (!(await fs.lstat(packagePath)).isFile()) {
              return;
            }
          } catch {
            return;
          }

          const packageJson: PackageJSON = (
            await import(pathToFileURL(packagePath).href, {
              with: { type: 'json' },
            })
          ).default;

          if ('private' in packageJson && packageJson.private === true) {
            return;
          }

          const result = await execFile('npm', ['pack', packageDir], {
            cwd: TAR_FOLDER,
            encoding: 'utf-8',
            shell: true,
          });

          if (typeof result.stdout !== 'string') {
            return;
          }

          const stdoutLines = result.stdout.trim().split('\n');
          const tarball = stdoutLines[stdoutLines.length - 1];

          return [
            packageJson.name,
            `file:${path.join(TAR_FOLDER, tarball)}`,
          ] as const;
        }),
      )
    ).filter(e => e != null),
  );

  const BASE_DEPENDENCIES: PackageJSON['devDependencies'] = {
    ...tseslintPackages,
    eslint: rootPackageJson.devDependencies.eslint,
    typescript: rootPackageJson.devDependencies.typescript,
    vitest: rootPackageJson.devDependencies.vitest,
  };

  const temp = await fs.mkdtemp(path.join(INTEGRATION_TEST_DIR, 'temp'), {
    encoding: 'utf-8',
  });

  await fs.writeFile(path.join(temp, '.yarnrc.yml'), YARN_RC_CONTENT, {
    encoding: 'utf-8',
  });

  await fs.writeFile(
    path.join(temp, 'package.json'),
    JSON.stringify(
      {
        devDependencies: BASE_DEPENDENCIES,
        packageManager: rootPackageJson.packageManager,
        private: true,
        resolutions: tseslintPackages,
      },
      null,
      2,
    ),
    { encoding: 'utf-8' },
  );

  // We install the tarballs here once so that yarn can cache them globally.
  // This solves 2 problems:
  // 1. Tests can be run concurrently because they won't be trying to install
  //    the same tarballs at the same time.
  // 2. Installing the tarballs for each test becomes much faster as Yarn can
  //    grab them from the global cache folder.
  await execFile('yarn', ['install', '--no-immutable'], {
    cwd: temp,
    shell: true,
  });

  await Promise.all(
    testFileBaseNames.map(async fixture => {
      const testFolder = path.join(FIXTURES_DESTINATION_DIR, fixture);

      const fixtureDir = path.join(FIXTURES_DIR, fixture);

      const fixturePackageJson: PackageJSON = (
        await import(
          pathToFileURL(path.join(fixtureDir, 'package.json')).href,
          { with: { type: 'json' } }
        )
      ).default;

      await fs.cp(fixtureDir, testFolder, { recursive: true });

      await fs.writeFile(
        path.join(testFolder, 'package.json'),
        JSON.stringify(
          {
            private: true,
            ...fixturePackageJson,
            devDependencies: {
              ...BASE_DEPENDENCIES,
              ...fixturePackageJson.devDependencies,
            },

            packageManager: rootPackageJson.packageManager,

            // ensure everything uses the locally packed versions instead of the NPM versions
            resolutions: {
              ...tseslintPackages,
            },
          },
          null,
          2,
        ),
        { encoding: 'utf-8' },
      );

      await fs.writeFile(
        path.join(testFolder, '.yarnrc.yml'),
        YARN_RC_CONTENT,
        { encoding: 'utf-8' },
      );

      const { stderr, stdout } = await execFile(
        'yarn',
        ['install', '--no-immutable'],
        {
          cwd: testFolder,
          shell: true,
        },
      );

      if (stderr) {
        console.error(stderr);

        if (stdout) {
          console.log(stdout);
        }
      }
    }),
  );

  await fs.rm(temp, { recursive: true });

  console.log('Finished packing local packages.');
}
```
</details>

- **Parameters**:
  - `project: TestProject`
- **Return Type**: `Promise<void>`
- **Calls**:
  - `(
    await project.globTestFiles(project.vitest.state.getPaths())
  ).testFiles.map`
  - `project.globTestFiles`
  - `project.vitest.state.getPaths`
  - `path.basename`
  - `fs.readdir`
  - `fs.mkdir`
  - `Object.fromEntries`
  - `(
      await Promise.all(
        PACKAGES.map(async ({ name: pkg }) => {
          const packageDir = path.join(PACKAGES_DIR, pkg);
          const packagePath = path.join(packageDir, 'package.json');

          try {
            if (!(await fs.lstat(packagePath)).isFile()) {
              return;
            }
          } catch {
            return;
          }

          const packageJson: PackageJSON = (
            await import(pathToFileURL(packagePath).href, {
              with: { type: 'json' },
            })
          ).default;

          if ('private' in packageJson && packageJson.private === true) {
            return;
          }

          const result = await execFile('npm', ['pack', packageDir], {
            cwd: TAR_FOLDER,
            encoding: 'utf-8',
            shell: true,
          });

          if (typeof result.stdout !== 'string') {
            return;
          }

          const stdoutLines = result.stdout.trim().split('\n');
          const tarball = stdoutLines[stdoutLines.length - 1];

          return [
            packageJson.name,
            `file:${path.join(TAR_FOLDER, tarball)}`,
          ] as const;
        }),
      )
    ).filter`
  - `Promise.all`
  - `PACKAGES.map`
  - `path.join`
  - `(await fs.lstat(packagePath)).isFile`
  - `fs.lstat`
  - `complex_call_2317`
  - `pathToFileURL (from node:url)`
  - `execFile`
  - `result.stdout.trim().split`
  - `fs.mkdtemp`
  - `fs.writeFile`
  - `JSON.stringify`
  - `testFileBaseNames.map`
  - `complex_call_4599`
  - `fs.cp`
  - `console.error`
  - `console.log`
  - `fs.rm`
- **Internal Comments**:
```
// We install the tarballs here once so that yarn can cache them globally. (x2)
// This solves 2 problems: (x2)
// 1. Tests can be run concurrently because they won't be trying to install (x2)
//    the same tarballs at the same time. (x2)
// 2. Installing the tarballs for each test becomes much faster as Yarn can (x2)
//    grab them from the global cache folder. (x2)
// ensure everything uses the locally packed versions instead of the NPM versions (x2)
```

### `teardown(): Promise<void>`

<details><summary>Code</summary>

```ts
async (): Promise<void> => {
  if (process.env.KEEP_INTEGRATION_TEST_DIR !== 'true') {
    await fs.rm(INTEGRATION_TEST_DIR, { recursive: true });
  }
}
```
</details>

- **Return Type**: `Promise<void>`
- **Calls**:
  - `fs.rm`

---

## Interfaces

### `PackageJSON`

<details><summary>Interface Code</summary>

```ts
interface PackageJSON {
  devDependencies: Record<string, string>;
  name: string;
  private?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `devDependencies` | `Record<string, string>` | ✗ |  |
| `name` | `string` | ✗ |  |
| `private` | `boolean` | ✓ |  |


---