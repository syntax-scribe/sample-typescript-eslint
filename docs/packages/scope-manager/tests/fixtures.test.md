[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `fixtures.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `path` | `node:path` |
| `AnalyzeOptions` | `./test-utils` |
| `parseAndAnalyze` | `./test-utils` |


---

## Functions

### `nestDescribe(fixture: (typeof fixtures)[number], segments: any): void`

<details><summary>Code</summary>

```ts
function nestDescribe(
  fixture: (typeof fixtures)[number],
  segments = fixture.segments,
): void {
  if (segments.length > 0) {
    describe(segments[0], () => {
      nestDescribe(fixture, segments.slice(1));
    });
  } else {
    test(
      fixture.name,
      { only: [...fixture.segments, fixture.name].join(path.sep) === ONLY },
      async () => {
        const contents = await fs.readFile(fixture.absolute, {
          encoding: 'utf-8',
        });

        const lines = contents.split('\n');
        const options: Record<string, unknown> = {
          lib: [],
        };

        /*
         * What's all this!?
         *
         * To help with configuring individual tests, each test may use a four-slash comment to configure the scope manager
         * This is just a rudimentary "parser" for said comments.
         */
        for (const line of lines) {
          if (!line.startsWith('////')) {
            continue;
          }

          const match = FOUR_SLASH.exec(line);
          if (!match) {
            throw new Error(
              `Four-slash did not match expected format: ${line}`,
            );
          }
          const [, key, rawValue] = match;
          const type = ALLOWED_OPTIONS.get(key);
          if (!type) {
            throw new Error(`Unknown option ${key}`);
          }

          let value: unknown = rawValue;
          switch (type[0]) {
            case 'string': {
              const strmatch = QUOTED_STRING.exec(rawValue);
              if (strmatch) {
                value = strmatch[1];
              }
              break;
            }

            case 'number': {
              const parsed = parseFloat(rawValue);
              if (isNaN(parsed)) {
                throw new Error(
                  `Expected a number for ${key}, but got ${rawValue}`,
                );
              }
              value = parsed;
              break;
            }

            case 'boolean': {
              if (rawValue === 'true') {
                value = true;
              } else if (rawValue === 'false') {
                value = false;
              } else {
                throw new Error(
                  `Expected a boolean for ${key}, but got ${rawValue}`,
                );
              }
              break;
            }
          }

          if (type[1] && !type[1].has(value)) {
            throw new Error(
              `Expected value for ${key} to be one of (${[...type[1]].join(
                ' | ',
              )}), but got ${value as string}`,
            );
          }

          if (value === 'true') {
            options[key] = true;
          } else if (value === 'false') {
            options[key] = false;
          } else {
            options[key] = value;
          }
        }

        await fs.mkdir(fixture.snapshotPath, { recursive: true });

        try {
          const { scopeManager } = parseAndAnalyze(contents, options, {
            jsx: fixture.ext.endsWith('x'),
          });
          await expect(scopeManager).toMatchFileSnapshot(fixture.snapshotFile);
        } catch (e) {
          await expect(e).toMatchFileSnapshot(fixture.snapshotFile);
        }
      },
    );
  }
}
```
</details>

- **Parameters**:
  - `fixture: (typeof fixtures)[number]`
  - `segments: any`
- **Return Type**: `void`
- **Calls**:
  - `describe`
  - `nestDescribe`
  - `segments.slice`
  - `test`
  - `[...fixture.segments, fixture.name].join`
  - `fs.readFile`
  - `contents.split`
  - `line.startsWith`
  - `FOUR_SLASH.exec`
  - `ALLOWED_OPTIONS.get`
  - `QUOTED_STRING.exec`
  - `parseFloat`
  - `isNaN`
  - `type[1].has`
  - `[...type[1]].join`
  - `fs.mkdir`
  - `parseAndAnalyze (from ./test-utils)`
  - `fixture.ext.endsWith`
  - `expect(scopeManager).toMatchFileSnapshot`
  - `expect(e).toMatchFileSnapshot`
- **Internal Comments**:
```
/*
         * What's all this!?
         *
         * To help with configuring individual tests, each test may use a four-slash comment to configure the scope manager
         * This is just a rudimentary "parser" for said comments.
         */
```


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `ALLOWED_VALUE`

```ts
type ALLOWED_VALUE = ['boolean' | 'number' | 'string', Set<unknown>?];
```


---