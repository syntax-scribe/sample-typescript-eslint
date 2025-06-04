[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `unbound-method.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 7 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 12 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/unbound-method.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getModifiers` | `../util` |
| `getParserServices` | `../util` |
| `isBuiltinSymbolLike` | `../util` |
| `isSymbolFromDefaultLibrary` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `SUPPORTED_GLOBALS` | `readonly ["Number", "Object", "String", "RegExp", "Symbol", "Array", "Proxy", "Date", "Atomics", "Reflect", "console", "Math", "JSON", "Intl"]` | const | `[
  'Number',
  'Object',
  'String', // eslint-disable-line @typescript-eslint/internal/prefer-ast-types-enum
  'RegExp',
  'Symbol',
  'Array',
  'Proxy',
  'Date',
  'Atomics',
  'Reflect',
  'console',
  'Math',
  'JSON',
  'Intl',
] as const` | ✗ |
| `object` | `SymbolConstructor | Console | ObjectConstructor | RegExpConstructor | ArrayConstructor | ... 8 more ... | JSON` | const | `global[namespace]` | ✗ |
| `nativelyBoundMembers` | `Set<string>` | const | `new Set(
  SUPPORTED_GLOBALS.flatMap(namespace => {
    if (!(namespace in global)) {
      // node.js might not have namespaces like Intl depending on compilation options
      // https://nodejs.org/api/intl.html#intl_options_for_building_node_js
      return [];
    }
    const object = global[namespace];
    return Object.getOwnPropertyNames(object)
      .filter(
        name =>
          !name.startsWith('_') &&
          typeof (object as Record<string, unknown>)[name] === 'function',
      )
      .map(name => `${namespace}.${name}`);
  }),
)` | ✗ |
| `SUPPORTED_GLOBAL_TYPES` | `string[]` | const | `[
  'NumberConstructor',
  'ObjectConstructor',
  'StringConstructor',
  'SymbolConstructor',
  'ArrayConstructor',
  'Array',
  'ProxyConstructor',
  'Console',
  'DateConstructor',
  'Atomics',
  'Math',
  'JSON',
]` | ✗ |
| `BASE_MESSAGE` | `"Avoid referencing unbound methods which may cause unintentional scoping of `this`."` | const | `'Avoid referencing unbound methods which may cause unintentional scoping of `this`.'` | ✗ |
| `notImported` | `boolean` | const | `objectSymbol != null &&
          isNotImported(objectSymbol, currentSourceFile)` | ✗ |
| `initNode` | `TSESTree.Node | null` | let/var | `null` | ✗ |
| `parent` | `TSESTree.Node | undefined` | let/var | `node` | ✗ |
| `assignee` | `any` | const | `(valueDeclaration as ts.PropertyAssignment).initializer` | ✗ |
| `firstParamIsThis` | `boolean` | const | `firstParam?.name.kind === ts.SyntaxKind.Identifier &&
    // eslint-disable-next-line @typescript-eslint/no-unsafe-enum-comparison
    firstParam.name.escapedText === 'this'` | ✗ |
| `thisArgIsVoid` | `boolean` | const | `firstParamIsThis && firstParam.type?.kind === ts.SyntaxKind.VoidKeyword` | ✗ |
| `parent` | `any` | const | `node.parent` | ✗ |


---

## Functions

### `isNotImported(symbol: ts.Symbol, currentSourceFile: ts.SourceFile | undefined): boolean`

<details><summary>Code</summary>

```ts
(
  symbol: ts.Symbol,
  currentSourceFile: ts.SourceFile | undefined,
): boolean => {
  const { valueDeclaration } = symbol;
  if (!valueDeclaration) {
    // working around https://github.com/microsoft/TypeScript/issues/31294
    return false;
  }

  return (
    !!currentSourceFile &&
    currentSourceFile !== valueDeclaration.getSourceFile()
  );
}
```
</details>

- **Parameters**:
  - `symbol: ts.Symbol`
  - `currentSourceFile: ts.SourceFile | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `valueDeclaration.getSourceFile`
- **Internal Comments**:
```
// working around https://github.com/microsoft/TypeScript/issues/31294
```

### `checkIfMethodAndReport(node: TSESTree.Node, symbol: ts.Symbol | undefined): boolean`

<details><summary>Code</summary>

```ts
function checkIfMethodAndReport(
      node: TSESTree.Node,
      symbol: ts.Symbol | undefined,
    ): boolean {
      if (!symbol) {
        return false;
      }

      const { dangerous, firstParamIsThis } = checkIfMethod(
        symbol,
        ignoreStatic,
      );
      if (dangerous) {
        context.report({
          node,
          messageId:
            firstParamIsThis === false
              ? 'unboundWithoutThisAnnotation'
              : 'unbound',
        });
        return true;
      }
      return false;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `symbol: ts.Symbol | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `checkIfMethod`
  - `context.report`
### `isNativelyBound(object: TSESTree.Node, property: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isNativelyBound(
      object: TSESTree.Node,
      property: TSESTree.Node,
    ): boolean {
      // We can't rely entirely on the type-level checks made at the end of this
      // function, because sometimes type declarations don't come from the
      // default library, but come from, for example, "@types/node". And we can't
      // tell if a method is unbound just by looking at its signature declared in
      // the interface.
      //
      // See related discussion https://github.com/typescript-eslint/typescript-eslint/pull/8952#discussion_r1576543310
      if (
        object.type === AST_NODE_TYPES.Identifier &&
        property.type === AST_NODE_TYPES.Identifier
      ) {
        const objectSymbol = services.getSymbolAtLocation(object);
        const notImported =
          objectSymbol != null &&
          isNotImported(objectSymbol, currentSourceFile);

        if (
          notImported &&
          nativelyBoundMembers.has(`${object.name}.${property.name}`)
        ) {
          return true;
        }
      }

      // if `${object.name}.${property.name}` doesn't match any of
      // the nativelyBoundMembers, then we fallback to type-level checks
      return (
        isBuiltinSymbolLike(
          services.program,
          services.getTypeAtLocation(object),
          SUPPORTED_GLOBAL_TYPES,
        ) &&
        isSymbolFromDefaultLibrary(
          services.program,
          services.getTypeAtLocation(property).getSymbol(),
        )
      );
    }
```
</details>

- **Parameters**:
  - `object: TSESTree.Node`
  - `property: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `services.getSymbolAtLocation`
  - `isNotImported`
  - `nativelyBoundMembers.has`
  - `isBuiltinSymbolLike (from ../util)`
  - `services.getTypeAtLocation`
  - `isSymbolFromDefaultLibrary (from ../util)`
  - `services.getTypeAtLocation(property).getSymbol`
- **Internal Comments**:
```
// We can't rely entirely on the type-level checks made at the end of this
// function, because sometimes type declarations don't come from the
// default library, but come from, for example, "@types/node". And we can't
// tell if a method is unbound just by looking at its signature declared in
// the interface.
//
// See related discussion https://github.com/typescript-eslint/typescript-eslint/pull/8952#discussion_r1576543310
// if `${object.name}.${property.name}` doesn't match any of
// the nativelyBoundMembers, then we fallback to type-level checks
```

### `isNodeInsideTypeDeclaration(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isNodeInsideTypeDeclaration(node: TSESTree.Node): boolean {
  let parent: TSESTree.Node | undefined = node;
  while ((parent = parent.parent)) {
    if (
      (parent.type === AST_NODE_TYPES.ClassDeclaration && parent.declare) ||
      parent.type === AST_NODE_TYPES.TSAbstractMethodDefinition ||
      parent.type === AST_NODE_TYPES.TSDeclareFunction ||
      parent.type === AST_NODE_TYPES.TSFunctionType ||
      parent.type === AST_NODE_TYPES.TSInterfaceDeclaration ||
      parent.type === AST_NODE_TYPES.TSTypeAliasDeclaration ||
      (parent.type === AST_NODE_TYPES.VariableDeclaration && parent.declare)
    ) {
      return true;
    }
  }
  return false;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `checkIfMethod(symbol: ts.Symbol, ignoreStatic: boolean): CheckMethodResult`

<details><summary>Code</summary>

```ts
function checkIfMethod(
  symbol: ts.Symbol,
  ignoreStatic: boolean,
): CheckMethodResult {
  const { valueDeclaration } = symbol;
  if (!valueDeclaration) {
    // working around https://github.com/microsoft/TypeScript/issues/31294
    return { dangerous: false };
  }

  switch (valueDeclaration.kind) {
    case ts.SyntaxKind.PropertyDeclaration:
      return {
        dangerous:
          (valueDeclaration as ts.PropertyDeclaration).initializer?.kind ===
          ts.SyntaxKind.FunctionExpression,
      };
    case ts.SyntaxKind.PropertyAssignment: {
      const assignee = (valueDeclaration as ts.PropertyAssignment).initializer;
      if (assignee.kind !== ts.SyntaxKind.FunctionExpression) {
        return {
          dangerous: false,
        };
      }
      return checkMethod(assignee as ts.FunctionExpression, ignoreStatic);
    }
    case ts.SyntaxKind.MethodDeclaration:
    case ts.SyntaxKind.MethodSignature: {
      return checkMethod(
        valueDeclaration as ts.MethodDeclaration | ts.MethodSignature,
        ignoreStatic,
      );
    }
  }

  return { dangerous: false };
}
```
</details>

- **Parameters**:
  - `symbol: ts.Symbol`
  - `ignoreStatic: boolean`
- **Return Type**: `CheckMethodResult`
- **Calls**:
  - `checkMethod`
- **Internal Comments**:
```
// working around https://github.com/microsoft/TypeScript/issues/31294
```

### `checkMethod(valueDeclaration: | ts.FunctionExpression
    | ts.MethodDeclaration
    | ts.MethodSignature, ignoreStatic: boolean): CheckMethodResult`

<details><summary>Code</summary>

```ts
function checkMethod(
  valueDeclaration:
    | ts.FunctionExpression
    | ts.MethodDeclaration
    | ts.MethodSignature,
  ignoreStatic: boolean,
): CheckMethodResult {
  const firstParam = valueDeclaration.parameters.at(0);
  const firstParamIsThis =
    firstParam?.name.kind === ts.SyntaxKind.Identifier &&
    // eslint-disable-next-line @typescript-eslint/no-unsafe-enum-comparison
    firstParam.name.escapedText === 'this';
  const thisArgIsVoid =
    firstParamIsThis && firstParam.type?.kind === ts.SyntaxKind.VoidKeyword;

  return {
    dangerous:
      !thisArgIsVoid &&
      !(
        ignoreStatic &&
        tsutils.includesModifier(
          getModifiers(valueDeclaration),
          ts.SyntaxKind.StaticKeyword,
        )
      ),
    firstParamIsThis,
  };
}
```
</details>

- **Parameters**:
  - `valueDeclaration: | ts.FunctionExpression
    | ts.MethodDeclaration
    | ts.MethodSignature`
  - `ignoreStatic: boolean`
- **Return Type**: `CheckMethodResult`
- **Calls**:
  - `valueDeclaration.parameters.at`
  - `tsutils.includesModifier`
  - `getModifiers (from ../util)`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-unsafe-enum-comparison (x4)
```

### `isSafeUse(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isSafeUse(node: TSESTree.Node): boolean {
  const parent = node.parent;

  switch (parent?.type) {
    case AST_NODE_TYPES.IfStatement:
    case AST_NODE_TYPES.ForStatement:
    case AST_NODE_TYPES.MemberExpression:
    case AST_NODE_TYPES.SwitchStatement:
    case AST_NODE_TYPES.UpdateExpression:
    case AST_NODE_TYPES.WhileStatement:
      return true;

    case AST_NODE_TYPES.CallExpression:
      return parent.callee === node;

    case AST_NODE_TYPES.ConditionalExpression:
      return parent.test === node;

    case AST_NODE_TYPES.TaggedTemplateExpression:
      return parent.tag === node;

    case AST_NODE_TYPES.UnaryExpression:
      // the first case is safe for obvious
      // reasons. The second one is also fine
      // since we're returning something falsy
      return ['!', 'delete', 'typeof', 'void'].includes(parent.operator);

    case AST_NODE_TYPES.BinaryExpression:
      return ['!=', '!==', '==', '===', 'instanceof'].includes(parent.operator);

    case AST_NODE_TYPES.AssignmentExpression:
      return (
        parent.operator === '=' &&
        (node === parent.left ||
          (node.type === AST_NODE_TYPES.MemberExpression &&
            node.object.type === AST_NODE_TYPES.Super &&
            parent.left.type === AST_NODE_TYPES.MemberExpression &&
            parent.left.object.type === AST_NODE_TYPES.ThisExpression))
      );

    case AST_NODE_TYPES.ChainExpression:
    case AST_NODE_TYPES.TSNonNullExpression:
    case AST_NODE_TYPES.TSAsExpression:
    case AST_NODE_TYPES.TSTypeAssertion:
      return isSafeUse(parent);

    case AST_NODE_TYPES.LogicalExpression:
      if (parent.operator === '&&' && parent.left === node) {
        // this is safe, as && will return the left if and only if it's falsy
        return true;
      }

      // in all other cases, it's likely the logical expression will return the method ref
      // so make sure the parent is a safe usage
      return isSafeUse(parent);
  }

  return false;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `['!', 'delete', 'typeof', 'void'].includes`
  - `['!=', '!==', '==', '===', 'instanceof'].includes`
  - `isSafeUse`
- **Internal Comments**:
```
// the first case is safe for obvious
// reasons. The second one is also fine
// since we're returning something falsy
// this is safe, as && will return the left if and only if it's falsy
// in all other cases, it's likely the logical expression will return the method ref
// so make sure the parent is a safe usage
```


---

## Interfaces

### `Config`

<details><summary>Interface Code</summary>

```ts
interface Config {
  ignoreStatic: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `ignoreStatic` | `boolean` | ✗ |  |

### `CheckMethodResult`

<details><summary>Interface Code</summary>

```ts
interface CheckMethodResult {
  dangerous: boolean;
  firstParamIsThis?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `dangerous` | `boolean` | ✗ |  |
| `firstParamIsThis` | `boolean` | ✓ |  |


---

## Type Aliases

### `Options`

```ts
type Options = [Config];
```

### `MessageIds`

```ts
type MessageIds = 'unbound' | 'unboundWithoutThisAnnotation';
```


---