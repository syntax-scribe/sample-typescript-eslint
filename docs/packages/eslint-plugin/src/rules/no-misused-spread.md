[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-misused-spread.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 33 |
| 🧱 Classes | 0 |
| 📦 Imports | 14 |
| 📊 Variables & Constants | 1 |
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
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-misused-spread.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `TypeOrValueSpecifier` | `../util` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `getWrappingFixer` | `../util` |
| `isBuiltinSymbolLike` | `../util` |
| `isPromiseLike` | `../util` |
| `isTypeFlagSet` | `../util` |
| `readonlynessOptionsSchema` | `../util` |
| `typeMatchesSomeSpecifier` | `../util` |
| `isHigherPrecedenceThanAwait` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `kind` | `any` | const | `t.getSymbol()?.valueDeclaration?.kind` | ✗ |


---

## Functions

### `checkArrayOrCallSpread(node: TSESTree.SpreadElement): void`

<details><summary>Code</summary>

```ts
function checkArrayOrCallSpread(node: TSESTree.SpreadElement): void {
      const type = getConstrainedTypeAtLocation(services, node.argument);

      if (
        !typeMatchesSomeSpecifier(type, options.allow, services.program) &&
        isString(type)
      ) {
        context.report({
          node,
          messageId: 'noStringSpread',
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.SpreadElement`
- **Return Type**: `void`
- **Calls**:
  - `getConstrainedTypeAtLocation (from ../util)`
  - `typeMatchesSomeSpecifier (from ../util)`
  - `isString`
  - `context.report`
### `getMapSpreadSuggestions(node: TSESTree.JSXSpreadAttribute | TSESTree.SpreadElement, type: ts.Type): TSESLint.ReportSuggestionArray<MessageIds> | null`

<details><summary>Code</summary>

```ts
function getMapSpreadSuggestions(
      node: TSESTree.JSXSpreadAttribute | TSESTree.SpreadElement,
      type: ts.Type,
    ): TSESLint.ReportSuggestionArray<MessageIds> | null {
      const types = tsutils.unionConstituents(type);
      if (types.some(t => !isMap(services.program, t))) {
        return null;
      }

      if (
        node.parent.type === AST_NODE_TYPES.ObjectExpression &&
        node.parent.properties.length === 1
      ) {
        return [
          {
            messageId: 'replaceMapSpreadInObject',
            fix: getWrappingFixer({
              node: node.parent,
              innerNode: node.argument,
              sourceCode: context.sourceCode,
              wrap: code => `Object.fromEntries(${code})`,
            }),
          },
        ];
      }

      return [
        {
          messageId: 'replaceMapSpreadInObject',
          fix: getWrappingFixer({
            node: node.argument,
            sourceCode: context.sourceCode,
            wrap: code => `Object.fromEntries(${code})`,
          }),
        },
      ];
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.JSXSpreadAttribute | TSESTree.SpreadElement`
  - `type: ts.Type`
- **Return Type**: `TSESLint.ReportSuggestionArray<MessageIds> | null`
- **Calls**:
  - `tsutils.unionConstituents`
  - `types.some`
  - `isMap`
  - `getWrappingFixer (from ../util)`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `getPromiseSpreadSuggestions(node: TSESTree.Expression): TSESLint.ReportSuggestionArray<MessageIds>`

<details><summary>Code</summary>

```ts
function getPromiseSpreadSuggestions(
      node: TSESTree.Expression,
    ): TSESLint.ReportSuggestionArray<MessageIds> {
      const isHighPrecendence = isHigherPrecedenceThanAwait(
        services.esTreeNodeToTSNodeMap.get(node),
      );

      return [
        {
          messageId: 'addAwait',
          fix: fixer =>
            isHighPrecendence
              ? fixer.insertTextBefore(node, 'await ')
              : [
                  fixer.insertTextBefore(node, 'await ('),
                  fixer.insertTextAfter(node, ')'),
                ],
        },
      ];
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `TSESLint.ReportSuggestionArray<MessageIds>`
- **Calls**:
  - `isHigherPrecedenceThanAwait (from ../util)`
  - `services.esTreeNodeToTSNodeMap.get`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
            isHighPrecendence
              ? fixer.insertTextBefore(node, 'await ')
              : [
                  fixer.insertTextBefore(node, 'await ('),
                  fixer.insertTextAfter(node, ')'),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
            isHighPrecendence
              ? fixer.insertTextBefore(node, 'await ')
              : [
                  fixer.insertTextBefore(node, 'await ('),
                  fixer.insertTextAfter(node, ')'),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
### `checkObjectSpread(node: TSESTree.JSXSpreadAttribute | TSESTree.SpreadElement): void`

<details><summary>Code</summary>

```ts
function checkObjectSpread(
      node: TSESTree.JSXSpreadAttribute | TSESTree.SpreadElement,
    ): void {
      const type = getConstrainedTypeAtLocation(services, node.argument);

      if (typeMatchesSomeSpecifier(type, options.allow, services.program)) {
        return;
      }

      if (isPromise(services.program, type)) {
        context.report({
          node,
          messageId: 'noPromiseSpreadInObject',
          suggest: getPromiseSpreadSuggestions(node.argument),
        });

        return;
      }

      if (isFunctionWithoutProps(type)) {
        context.report({
          node,
          messageId: 'noFunctionSpreadInObject',
        });

        return;
      }

      if (isMap(services.program, type)) {
        context.report({
          node,
          messageId: 'noMapSpreadInObject',
          suggest: getMapSpreadSuggestions(node, type),
        });

        return;
      }

      if (isArray(checker, type)) {
        context.report({
          node,
          messageId: 'noArraySpreadInObject',
        });

        return;
      }

      if (
        isIterable(type, checker) &&
        // Don't report when the type is string, since TS will flag it already
        !isString(type)
      ) {
        context.report({
          node,
          messageId: 'noIterableSpreadInObject',
        });

        return;
      }

      if (isClassInstance(checker, type)) {
        context.report({
          node,
          messageId: 'noClassInstanceSpreadInObject',
        });

        return;
      }

      if (isClassDeclaration(type)) {
        context.report({
          node,
          messageId: 'noClassDeclarationSpreadInObject',
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.JSXSpreadAttribute | TSESTree.SpreadElement`
- **Return Type**: `void`
- **Calls**:
  - `getConstrainedTypeAtLocation (from ../util)`
  - `typeMatchesSomeSpecifier (from ../util)`
  - `isPromise`
  - `context.report`
  - `getPromiseSpreadSuggestions`
  - `isFunctionWithoutProps`
  - `isMap`
  - `getMapSpreadSuggestions`
  - `isArray`
  - `isIterable`
  - `isString`
  - `isClassInstance`
  - `isClassDeclaration`
- **Internal Comments**:
```
// Don't report when the type is string, since TS will flag it already
```

### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `Object.fromEntries(${code})`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
            isHighPrecendence
              ? fixer.insertTextBefore(node, 'await ')
              : [
                  fixer.insertTextBefore(node, 'await ('),
                  fixer.insertTextAfter(node, ')'),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
            isHighPrecendence
              ? fixer.insertTextBefore(node, 'await ')
              : [
                  fixer.insertTextBefore(node, 'await ('),
                  fixer.insertTextAfter(node, ')'),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
### `isIterable(type: ts.Type, checker: ts.TypeChecker): boolean`

<details><summary>Code</summary>

```ts
function isIterable(type: ts.Type, checker: ts.TypeChecker): boolean {
  return tsutils
    .typeConstituents(type)
    .some(
      t => !!tsutils.getWellKnownSymbolPropertyOfType(t, 'iterator', checker),
    );
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `checker: ts.TypeChecker`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils
    .typeConstituents(type)
    .some`
  - `tsutils.getWellKnownSymbolPropertyOfType`
### `isArray(checker: ts.TypeChecker, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isArray(checker: ts.TypeChecker, type: ts.Type): boolean {
  return isTypeRecurser(
    type,
    t => checker.isArrayType(t) || checker.isTupleType(t),
  );
}
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeRecurser`
  - `checker.isArrayType`
  - `checker.isTupleType`
### `isString(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isString(type: ts.Type): boolean {
  return isTypeRecurser(type, t => isTypeFlagSet(t, ts.TypeFlags.StringLike));
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeRecurser`
  - `isTypeFlagSet (from ../util)`
### `isFunctionWithoutProps(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isFunctionWithoutProps(type: ts.Type): boolean {
  return isTypeRecurser(
    type,
    t => t.getCallSignatures().length > 0 && t.getProperties().length === 0,
  );
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeRecurser`
  - `t.getCallSignatures`
  - `t.getProperties`
### `isPromise(program: ts.Program, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isPromise(program: ts.Program, type: ts.Type): boolean {
  return isTypeRecurser(type, t => isPromiseLike(program, t));
}
```
</details>

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeRecurser`
  - `isPromiseLike (from ../util)`
### `isClassInstance(checker: ts.TypeChecker, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isClassInstance(checker: ts.TypeChecker, type: ts.Type): boolean {
  return isTypeRecurser(type, t => {
    // If the type itself has a construct signature, it's a class(-like)
    if (t.getConstructSignatures().length) {
      return false;
    }

    const symbol = t.getSymbol();

    // If the type's symbol has a construct signature, the type is an instance
    return !!symbol
      ?.getDeclarations()
      ?.some(
        declaration =>
          checker
            .getTypeOfSymbolAtLocation(symbol, declaration)
            .getConstructSignatures().length,
      );
  });
}
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeRecurser`
  - `t.getConstructSignatures`
  - `t.getSymbol`
  - `symbol
      ?.getDeclarations()
      ?.some`
  - `checker
            .getTypeOfSymbolAtLocation(symbol, declaration)
            .getConstructSignatures`
- **Internal Comments**:
```
// If the type itself has a construct signature, it's a class(-like)
// If the type's symbol has a construct signature, the type is an instance
```

### `isClassDeclaration(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isClassDeclaration(type: ts.Type): boolean {
  return isTypeRecurser(type, t => {
    if (
      tsutils.isObjectType(t) &&
      tsutils.isObjectFlagSet(t, ts.ObjectFlags.InstantiationExpressionType)
    ) {
      return true;
    }

    const kind = t.getSymbol()?.valueDeclaration?.kind;

    return (
      kind === ts.SyntaxKind.ClassDeclaration ||
      kind === ts.SyntaxKind.ClassExpression
    );
  });
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeRecurser`
  - `tsutils.isObjectType`
  - `tsutils.isObjectFlagSet`
  - `t.getSymbol`
### `isMap(program: ts.Program, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isMap(program: ts.Program, type: ts.Type): boolean {
  return isTypeRecurser(type, t =>
    isBuiltinSymbolLike(program, t, ['Map', 'ReadonlyMap', 'WeakMap']),
  );
}
```
</details>

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeRecurser`
  - `isBuiltinSymbolLike (from ../util)`
### `isTypeRecurser(type: ts.Type, predicate: (t: ts.Type) => boolean): boolean`

<details><summary>Code</summary>

```ts
function isTypeRecurser(
  type: ts.Type,
  predicate: (t: ts.Type) => boolean,
): boolean {
  if (type.isUnionOrIntersection()) {
    return type.types.some(t => isTypeRecurser(t, predicate));
  }

  return predicate(type);
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `predicate: (t: ts.Type) => boolean`
- **Return Type**: `boolean`
- **Calls**:
  - `type.isUnionOrIntersection`
  - `type.types.some`
  - `isTypeRecurser`
  - `predicate`

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    allow?: TypeOrValueSpecifier[];
  },
];
```

### `MessageIds`

```ts
type MessageIds = | 'addAwait'
  | 'noArraySpreadInObject'
  | 'noClassDeclarationSpreadInObject'
  | 'noClassInstanceSpreadInObject'
  | 'noFunctionSpreadInObject'
  | 'noIterableSpreadInObject'
  | 'noMapSpreadInObject'
  | 'noPromiseSpreadInObject'
  | 'noStringSpread'
  | 'replaceMapSpreadInObject';
```


---