[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-restricted-imports.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 10
- **Classes**: 0
- **Imports**: 14
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-restricted-imports.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `JSONSchema4AnyOfSchema` | `@typescript-eslint/utils/json-schema` |
| `JSONSchema4ArraySchema` | `@typescript-eslint/utils/json-schema` |
| `JSONSchema4ObjectSchema` | `@typescript-eslint/utils/json-schema` |
| `ArrayOfStringOrObject` | `eslint/lib/rules/no-restricted-imports` |
| `ArrayOfStringOrObjectPatterns` | `eslint/lib/rules/no-restricted-imports` |
| `RuleListener` | `eslint/lib/rules/no-restricted-imports` |
| `Ignore` | `ignore` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ignore` | `ignore` |
| `InferMessageIdsTypeFromRule` | `../util` |
| `InferOptionsTypeFromRule` | `../util` |
| `createRule` | `../util` |
| `getESLintCoreRule` | `../util/getESLintCoreRule` |


---

## Functions

### `tryAccess(getter: () => T, fallback: T): T`

<details><summary>Code</summary>

```ts
<T>(getter: () => T, fallback: T): T => {
  try {
    return getter();
  } catch {
    return fallback;
  }
}
```
</details>

- **Parameters**:
  - `getter: () => T`
  - `fallback: T`
- **Return Type**: `T`
- **Calls**:
  - `getter`
### `isObjectOfPaths(obj: unknown): obj is { paths: ArrayOfStringOrObject }`

<details><summary>Code</summary>

```ts
function isObjectOfPaths(
  obj: unknown,
): obj is { paths: ArrayOfStringOrObject } {
  return !!obj && Object.hasOwn(obj, 'paths');
}
```
</details>

- **Parameters**:
  - `obj: unknown`
- **Return Type**: `obj is { paths: ArrayOfStringOrObject }`
- **Calls**:
  - `Object.hasOwn`
### `isObjectOfPatterns(obj: unknown): obj is { patterns: ArrayOfStringOrObjectPatterns }`

<details><summary>Code</summary>

```ts
function isObjectOfPatterns(
  obj: unknown,
): obj is { patterns: ArrayOfStringOrObjectPatterns } {
  return !!obj && Object.hasOwn(obj, 'patterns');
}
```
</details>

- **Parameters**:
  - `obj: unknown`
- **Return Type**: `obj is { patterns: ArrayOfStringOrObjectPatterns }`
- **Calls**:
  - `Object.hasOwn`
### `isOptionsArrayOfStringOrObject(options: Options): options is ArrayOfStringOrObject`

<details><summary>Code</summary>

```ts
function isOptionsArrayOfStringOrObject(
  options: Options,
): options is ArrayOfStringOrObject {
  if (isObjectOfPaths(options[0])) {
    return false;
  }
  if (isObjectOfPatterns(options[0])) {
    return false;
  }
  return true;
}
```
</details>

- **Parameters**:
  - `options: Options`
- **Return Type**: `options is ArrayOfStringOrObject`
- **Calls**:
  - `isObjectOfPaths`
  - `isObjectOfPatterns`
### `getRestrictedPaths(options: Options): ArrayOfStringOrObject`

<details><summary>Code</summary>

```ts
function getRestrictedPaths(options: Options): ArrayOfStringOrObject {
  if (isOptionsArrayOfStringOrObject(options)) {
    return options;
  }
  if (isObjectOfPaths(options[0])) {
    return options[0].paths;
  }
  return [];
}
```
</details>

- **Parameters**:
  - `options: Options`
- **Return Type**: `ArrayOfStringOrObject`
- **Calls**:
  - `isOptionsArrayOfStringOrObject`
  - `isObjectOfPaths`
### `getRestrictedPatterns(options: Options): ArrayOfStringOrObjectPatterns`

<details><summary>Code</summary>

```ts
function getRestrictedPatterns(
  options: Options,
): ArrayOfStringOrObjectPatterns {
  if (isObjectOfPatterns(options[0])) {
    return options[0].patterns;
  }
  return [];
}
```
</details>

- **Parameters**:
  - `options: Options`
- **Return Type**: `ArrayOfStringOrObjectPatterns`
- **Calls**:
  - `isObjectOfPatterns`
### `shouldCreateRule(baseRules: RuleListener, options: Options): baseRules is Exclude<RuleListener, Record<string, never>>`

<details><summary>Code</summary>

```ts
function shouldCreateRule(
  baseRules: RuleListener,
  options: Options,
): baseRules is Exclude<RuleListener, Record<string, never>> {
  if (Object.keys(baseRules).length === 0 || options.length === 0) {
    return false;
  }

  if (!isOptionsArrayOfStringOrObject(options)) {
    return !!(options[0].paths?.length || options[0].patterns?.length);
  }

  return true;
}
```
</details>

- **Parameters**:
  - `baseRules: RuleListener`
  - `options: Options`
- **Return Type**: `baseRules is Exclude<RuleListener, Record<string, never>>`
- **Calls**:
  - `Object.keys`
  - `isOptionsArrayOfStringOrObject`
### `isAllowedTypeImportPath(importSource: string): boolean`

<details><summary>Code</summary>

```ts
function isAllowedTypeImportPath(importSource: string): boolean {
      return allowedTypeImportPathNameSet.has(importSource);
    }
```
</details>

- **Parameters**:
  - `importSource: string`
- **Return Type**: `boolean`
- **Calls**:
  - `allowedTypeImportPathNameSet.has`
### `isAllowedTypeImportPattern(importSource: string): boolean`

<details><summary>Code</summary>

```ts
function isAllowedTypeImportPattern(importSource: string): boolean {
      return (
        // As long as there's one matching pattern that allows type import
        allowedImportTypeMatchers.some(matcher =>
          matcher.ignores(importSource),
        ) ||
        allowedImportTypeRegexMatchers.some(regex => regex.test(importSource))
      );
    }
```
</details>

- **Parameters**:
  - `importSource: string`
- **Return Type**: `boolean`
- **Calls**:
  - `allowedImportTypeMatchers.some`
  - `matcher.ignores`
  - `allowedImportTypeRegexMatchers.some`
  - `regex.test`
- **Internal Comments**:
```
// As long as there's one matching pattern that allows type import (x4)
```

### `checkImportNode(node: TSESTree.ImportDeclaration): void`

<details><summary>Code</summary>

```ts
function checkImportNode(node: TSESTree.ImportDeclaration): void {
      if (
        node.importKind === 'type' ||
        (node.specifiers.length > 0 &&
          node.specifiers.every(
            specifier =>
              specifier.type === AST_NODE_TYPES.ImportSpecifier &&
              specifier.importKind === 'type',
          ))
      ) {
        const importSource = node.source.value.trim();
        if (
          !isAllowedTypeImportPath(importSource) &&
          !isAllowedTypeImportPattern(importSource)
        ) {
          return rules.ImportDeclaration(node);
        }
      } else {
        return rules.ImportDeclaration(node);
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.ImportDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `node.specifiers.every`
  - `node.source.value.trim`
  - `isAllowedTypeImportPath`
  - `isAllowedTypeImportPattern`
  - `rules.ImportDeclaration`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `Options`

```ts
type Options = InferOptionsTypeFromRule<typeof baseRule>;
```

### `MessageIds`

```ts
type MessageIds = InferMessageIdsTypeFromRule<typeof baseRule>;
```


---