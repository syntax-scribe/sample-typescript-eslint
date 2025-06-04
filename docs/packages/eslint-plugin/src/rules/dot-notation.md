[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `dot-notation.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 8 |
| 📊 Variables & Constants | 6 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/dot-notation.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `InferMessageIdsTypeFromRule` | `../util` |
| `InferOptionsTypeFromRule` | `../util` |
| `createRule` | `../util` |
| `getModifiers` | `../util` |
| `getParserServices` | `../util` |
| `getESLintCoreRule` | `../util/getESLintCoreRule` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `defaultOptions` | `Options` | const | `[
  {
    allowIndexSignaturePropertyAccess: false,
    allowKeywords: true,
    allowPattern: '',
    allowPrivateClassPropertyAccess: false,
    allowProtectedClassPropertyAccess: false,
  },
]` | ✗ |
| `allowPrivateClassPropertyAccess` | `any` | const | `options.allowPrivateClassPropertyAccess` | ✗ |
| `allowProtectedClassPropertyAccess` | `any` | const | `options.allowProtectedClassPropertyAccess` | ✗ |
| `allowIndexSignaturePropertyAccess` | `any` | const | `(options.allowIndexSignaturePropertyAccess ?? false) ||
      tsutils.isCompilerOptionEnabled(
        services.program.getCompilerOptions(),
        'noPropertyAccessFromIndexSignature',
      )` | ✗ |
| `propertySymbol` | `any` | const | `services.getSymbolAtLocation(node.property) ??
            services
              .getTypeAtLocation(node.object)
              .getNonNullableType()
              .getProperties()
              .find(
                propertySymbol =>
                  node.property.type === AST_NODE_TYPES.Literal &&
                  propertySymbol.escapedName === node.property.value,
              )` | ✗ |
| `modifierKind` | `any` | const | `getModifiers(
            propertySymbol?.getDeclarations()?.[0],
          )?.[0].kind` | ✗ |


---


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