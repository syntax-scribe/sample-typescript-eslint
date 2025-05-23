[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `withoutProjectParserOptions.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/withoutProjectParserOptions.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `withoutProjectParserOptions(opts: Options): Omit<
  Options,
  'EXPERIMENTAL_useProjectService' | 'project' | 'projectService'
>`

<details><summary>Code</summary>

```ts
export function withoutProjectParserOptions<Options extends object>(
  opts: Options,
): Omit<
  Options,
  'EXPERIMENTAL_useProjectService' | 'project' | 'projectService'
> {
  // eslint-disable-next-line @typescript-eslint/no-unused-vars -- The variables are meant to be omitted
  const { EXPERIMENTAL_useProjectService, project, projectService, ...rest } =
    opts as Record<string, unknown>;

  return rest as unknown as Options;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Removes options that prompt the parser to parse the project with type
 * information. In other words, you can use this if you are invoking the parser
 * directly, to ensure that one file will be parsed in isolation, which is much,
 * much faster.
 *
 * @see https://github.com/typescript-eslint/typescript-eslint/issues/8428
 */
```

- **Parameters**:
  - `opts: Options`
- **Return Type**: `Omit<
  Options,
  'EXPERIMENTAL_useProjectService' | 'project' | 'projectService'
>`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-unused-vars -- The variables are meant to be omitted (x2)
```


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