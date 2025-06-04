[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-restricted-imports.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 10 |
| 📦 Imports | 14 |
| 📊 Variables & Constants | 9 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `baseSchema` | `{ anyOf: [unknown, { items: [{ properties: { paths: { items: { anyOf: [{ type: "string"; }, { properties: JSONSchema4ObjectSchema; required: string[]; type: "object"; }]; }; type: "array"; }; patterns: { anyOf: [{ items: { type: "string"; }; type: "array"; }, { ...; }]; }; }; type: "object"; }]; type: "array"; }]; }` | const | `baseRule.meta.schema as {
  anyOf: [
    unknown,
    {
      items: [
        {
          properties: {
            paths: {
              items: {
                anyOf: [
                  { type: 'string' },
                  {
                    properties: JSONSchema4ObjectSchema['properties'];
                    required: string[];
                    type: 'object';
                  },
                ];
              };
              type: 'array';
            };
            patterns: {
              anyOf: [
                { items: { type: 'string' }; type: 'array' },
                {
                  items: {
                    properties: JSONSchema4ObjectSchema['properties'];
                    required: string[];
                    type: 'object';
                  };
                  type: 'array';
                },
              ];
            };
          };
          type: 'object';
        },
      ];
      type: 'array';
    },
  ];
}` | ✗ |
| `allowTypeImportsOptionSchema` | `JSONSchema4ObjectSchema['properties']` | const | `{
  allowTypeImports: {
    type: 'boolean',
    description: 'Whether to allow type-only imports for a path.',
  },
}` | ✗ |
| `arrayOfStringsOrObjects` | `JSONSchema4ArraySchema` | const | `{
  type: 'array',
  items: {
    anyOf: [
      { type: 'string' },
      {
        type: 'object',
        additionalProperties: false,
        properties: {
          ...tryAccess(
            () =>
              baseSchema.anyOf[1].items[0].properties.paths.items.anyOf[1]
                .properties,
            undefined,
          ),
          ...allowTypeImportsOptionSchema,
        },
        required: tryAccess(
          () =>
            baseSchema.anyOf[1].items[0].properties.paths.items.anyOf[1]
              .required,
          undefined,
        ),
      },
    ],
  },
  uniqueItems: true,
}` | ✗ |
| `arrayOfStringsOrObjectPatterns` | `JSONSchema4AnyOfSchema` | const | `{
  anyOf: [
    {
      type: 'array',
      items: {
        type: 'string',
      },
      uniqueItems: true,
    },
    {
      type: 'array',
      items: {
        type: 'object',
        additionalProperties: false,
        properties: {
          ...tryAccess(
            () =>
              baseSchema.anyOf[1].items[0].properties.patterns.anyOf[1].items
                .properties,
            undefined,
          ),
          ...allowTypeImportsOptionSchema,
        },
        required: tryAccess(
          () =>
            baseSchema.anyOf[1].items[0].properties.patterns.anyOf[1].items
              .required,
          [],
        ),
      },
      uniqueItems: true,
    },
  ],
}` | ✗ |
| `schema` | `JSONSchema4AnyOfSchema` | const | `{
  anyOf: [
    arrayOfStringsOrObjects,
    {
      type: 'array',
      additionalItems: false,
      items: [
        {
          type: 'object',
          additionalProperties: false,
          properties: {
            paths: arrayOfStringsOrObjects,
            patterns: arrayOfStringsOrObjectPatterns,
          },
        },
      ],
    },
  ],
}` | ✗ |
| `allowedTypeImportPathNameSet` | `Set<string>` | const | `new Set<string>()` | ✗ |
| `allowedImportTypeMatchers` | `Ignore[]` | const | `[]` | ✗ |
| `allowedImportTypeRegexMatchers` | `RegExp[]` | const | `[]` | ✗ |
| `synthesizedImport` | `TSESTree.ImportDeclaration` | const | `{
            ...node,
            type: AST_NODE_TYPES.ImportDeclaration,
            assertions: [],
            attributes: [],
            source: node.moduleReference.expression,
            specifiers: [
              {
                ...node.id,
                type: AST_NODE_TYPES.ImportDefaultSpecifier,
                local: node.id,
                // @ts-expect-error -- parent types are incompatible but it's fine for the purposes of this extension
                parent: node.id.parent,
              },
            ],
          }` | ✗ |


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