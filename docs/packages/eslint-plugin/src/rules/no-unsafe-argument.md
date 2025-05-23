[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unsafe-argument.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 7
- **Classes**: 1
- **Imports**: 9
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unsafe-argument.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `isRestParameterDeclaration` | `../util` |
| `isTypeAnyArrayType` | `../util` |
| `isTypeAnyType` | `../util` |
| `isUnsafeAssignment` | `../util` |
| `nullThrows` | `../util` |


---

## Functions

### `FunctionSignature.create(checker: ts.TypeChecker, tsNode: ts.CallLikeExpression): FunctionSignature | null`

<details><summary>Code</summary>

```ts
public static create(
    checker: ts.TypeChecker,
    tsNode: ts.CallLikeExpression,
  ): FunctionSignature | null {
    const signature = checker.getResolvedSignature(tsNode);
    if (!signature) {
      return null;
    }

    const paramTypes: ts.Type[] = [];
    let restType: RestType | null = null;

    const parameters = signature.getParameters();
    for (let i = 0; i < parameters.length; i += 1) {
      const param = parameters[i];
      const type = checker.getTypeOfSymbolAtLocation(param, tsNode);

      const decl = param.getDeclarations()?.[0];
      if (decl && isRestParameterDeclaration(decl)) {
        // is a rest param
        if (checker.isArrayType(type)) {
          restType = {
            type: checker.getTypeArguments(type)[0],
            index: i,
            kind: RestTypeKind.Array,
          };
        } else if (checker.isTupleType(type)) {
          restType = {
            index: i,
            kind: RestTypeKind.Tuple,
            typeArguments: checker.getTypeArguments(type),
          };
        } else {
          restType = {
            type,
            index: i,
            kind: RestTypeKind.Other,
          };
        }
        break;
      }

      paramTypes.push(type);
    }

    return new this(paramTypes, restType);
  }
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `tsNode: ts.CallLikeExpression`
- **Return Type**: `FunctionSignature | null`
- **Calls**:
  - `checker.getResolvedSignature`
  - `signature.getParameters`
  - `checker.getTypeOfSymbolAtLocation`
  - `param.getDeclarations`
  - `isRestParameterDeclaration (from ../util)`
  - `checker.isArrayType`
  - `checker.getTypeArguments`
  - `checker.isTupleType`
  - `paramTypes.push`
- **Internal Comments**:
```
// is a rest param
```

### `FunctionSignature.consumeRemainingArguments(): void`

<details><summary>Code</summary>

```ts
public consumeRemainingArguments(): void {
    this.hasConsumedArguments = true;
  }
```
</details>

- **Return Type**: `void`
### `FunctionSignature.getNextParameterType(): ts.Type | null`

<details><summary>Code</summary>

```ts
public getNextParameterType(): ts.Type | null {
    const index = this.parameterTypeIndex;
    this.parameterTypeIndex += 1;

    if (index >= this.paramTypes.length || this.hasConsumedArguments) {
      if (this.restType == null) {
        return null;
      }

      switch (this.restType.kind) {
        case RestTypeKind.Tuple: {
          const typeArguments = this.restType.typeArguments;
          if (this.hasConsumedArguments) {
            // all types consumed by a rest - just assume it's the last type
            // there is one edge case where this is wrong, but we ignore it because
            // it's rare and really complicated to handle
            // eg: function foo(...a: [number, ...string[], number])
            return typeArguments[typeArguments.length - 1];
          }

          const typeIndex = index - this.restType.index;
          if (typeIndex >= typeArguments.length) {
            return typeArguments[typeArguments.length - 1];
          }

          return typeArguments[typeIndex];
        }

        case RestTypeKind.Array:
        case RestTypeKind.Other:
          return this.restType.type;
      }
    }
    return this.paramTypes[index];
  }
```
</details>

- **Return Type**: `ts.Type | null`
- **Internal Comments**:
```
// all types consumed by a rest - just assume it's the last type
// there is one edge case where this is wrong, but we ignore it because
// it's rare and really complicated to handle
// eg: function foo(...a: [number, ...string[], number])
```

### `describeType(type: ts.Type): string`

<details><summary>Code</summary>

```ts
function describeType(type: ts.Type): string {
      if (tsutils.isIntrinsicErrorType(type)) {
        return 'error typed';
      }

      return `\`${checker.typeToString(type)}\``;
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `string`
- **Calls**:
  - `tsutils.isIntrinsicErrorType`
  - `checker.typeToString`
### `describeTypeForSpread(type: ts.Type): string`

<details><summary>Code</summary>

```ts
function describeTypeForSpread(type: ts.Type): string {
      if (
        checker.isArrayType(type) &&
        tsutils.isIntrinsicErrorType(checker.getTypeArguments(type)[0])
      ) {
        return 'error';
      }

      return describeType(type);
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `string`
- **Calls**:
  - `checker.isArrayType`
  - `tsutils.isIntrinsicErrorType`
  - `checker.getTypeArguments`
  - `describeType`
### `describeTypeForTuple(type: ts.Type): string`

<details><summary>Code</summary>

```ts
function describeTypeForTuple(type: ts.Type): string {
      if (tsutils.isIntrinsicErrorType(type)) {
        return 'error typed';
      }

      return `of type \`${checker.typeToString(type)}\``;
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `string`
- **Calls**:
  - `tsutils.isIntrinsicErrorType`
  - `checker.typeToString`
### `checkUnsafeArguments(args: TSESTree.CallExpressionArgument[] | TSESTree.Expression[], callee: TSESTree.Expression, node: | TSESTree.CallExpression
        | TSESTree.NewExpression
        | TSESTree.TaggedTemplateExpression): void`

<details><summary>Code</summary>

```ts
function checkUnsafeArguments(
      args: TSESTree.CallExpressionArgument[] | TSESTree.Expression[],
      callee: TSESTree.Expression,
      node:
        | TSESTree.CallExpression
        | TSESTree.NewExpression
        | TSESTree.TaggedTemplateExpression,
    ): void {
      if (args.length === 0) {
        return;
      }

      // ignore any-typed calls as these are caught by no-unsafe-call
      if (isTypeAnyType(services.getTypeAtLocation(callee))) {
        return;
      }

      const tsNode = services.esTreeNodeToTSNodeMap.get(node);
      const signature = nullThrows(
        FunctionSignature.create(checker, tsNode),
        'Expected to a signature resolved',
      );

      if (node.type === AST_NODE_TYPES.TaggedTemplateExpression) {
        // Consumes the first parameter (TemplateStringsArray) of the function called with TaggedTemplateExpression.
        signature.getNextParameterType();
      }

      for (const argument of args) {
        switch (argument.type) {
          // spreads consume
          case AST_NODE_TYPES.SpreadElement: {
            const spreadArgType = services.getTypeAtLocation(argument.argument);

            if (isTypeAnyType(spreadArgType)) {
              // foo(...any)
              context.report({
                node: argument,
                messageId: 'unsafeSpread',
                data: { sender: describeType(spreadArgType) },
              });
            } else if (isTypeAnyArrayType(spreadArgType, checker)) {
              // foo(...any[])

              // TODO - we could break down the spread and compare the array type against each argument
              context.report({
                node: argument,
                messageId: 'unsafeArraySpread',
                data: { sender: describeTypeForSpread(spreadArgType) },
              });
            } else if (checker.isTupleType(spreadArgType)) {
              // foo(...[tuple1, tuple2])
              const spreadTypeArguments =
                checker.getTypeArguments(spreadArgType);
              for (const tupleType of spreadTypeArguments) {
                const parameterType = signature.getNextParameterType();
                if (parameterType == null) {
                  continue;
                }
                const result = isUnsafeAssignment(
                  tupleType,
                  parameterType,
                  checker,
                  // we can't pass the individual tuple members in here as this will most likely be a spread variable
                  // not a spread array
                  null,
                );
                if (result) {
                  context.report({
                    node: argument,
                    messageId: 'unsafeTupleSpread',
                    data: {
                      receiver: describeType(parameterType),
                      sender: describeTypeForTuple(tupleType),
                    },
                  });
                }
              }
              if (
                spreadArgType.target.combinedFlags & ts.ElementFlags.Variable
              ) {
                // the last element was a rest - so all remaining defined arguments can be considered "consumed"
                // all remaining arguments should be compared against the rest type (if one exists)
                signature.consumeRemainingArguments();
              }
            } else {
              // something that's iterable
              // handling this will be pretty complex - so we ignore it for now
              // TODO - handle generic iterable case
            }
            break;
          }

          default: {
            const parameterType = signature.getNextParameterType();
            if (parameterType == null) {
              continue;
            }

            const argumentType = services.getTypeAtLocation(argument);
            const result = isUnsafeAssignment(
              argumentType,
              parameterType,
              checker,
              argument,
            );
            if (result) {
              context.report({
                node: argument,
                messageId: 'unsafeArgument',
                data: {
                  receiver: describeType(parameterType),
                  sender: describeType(argumentType),
                },
              });
            }
          }
        }
      }
    }
```
</details>

- **Parameters**:
  - `args: TSESTree.CallExpressionArgument[] | TSESTree.Expression[]`
  - `callee: TSESTree.Expression`
  - `node: | TSESTree.CallExpression
        | TSESTree.NewExpression
        | TSESTree.TaggedTemplateExpression`
- **Return Type**: `void`
- **Calls**:
  - `isTypeAnyType (from ../util)`
  - `services.getTypeAtLocation`
  - `services.esTreeNodeToTSNodeMap.get`
  - `nullThrows (from ../util)`
  - `FunctionSignature.create`
  - `signature.getNextParameterType`
  - `context.report`
  - `describeType`
  - `isTypeAnyArrayType (from ../util)`
  - `describeTypeForSpread`
  - `checker.isTupleType`
  - `checker.getTypeArguments`
  - `isUnsafeAssignment (from ../util)`
  - `describeTypeForTuple`
  - `signature.consumeRemainingArguments`
- **Internal Comments**:
```
// ignore any-typed calls as these are caught by no-unsafe-call
// Consumes the first parameter (TemplateStringsArray) of the function called with TaggedTemplateExpression. (x4)
// spreads consume
// foo(...any) (x4)
// foo(...any[]) (x4)
// TODO - we could break down the spread and compare the array type against each argument (x4)
// foo(...[tuple1, tuple2]) (x2)
// we can't pass the individual tuple members in here as this will most likely be a spread variable
// not a spread array
// the last element was a rest - so all remaining defined arguments can be considered "consumed" (x4)
// all remaining arguments should be compared against the rest type (if one exists) (x4)
```


---

## Classes

### `FunctionSignature`

<details><summary>Class Code</summary>

```ts
class FunctionSignature {
  private hasConsumedArguments = false;

  private parameterTypeIndex = 0;

  private constructor(
    private paramTypes: ts.Type[],
    private restType: RestType | null,
  ) {}

  public static create(
    checker: ts.TypeChecker,
    tsNode: ts.CallLikeExpression,
  ): FunctionSignature | null {
    const signature = checker.getResolvedSignature(tsNode);
    if (!signature) {
      return null;
    }

    const paramTypes: ts.Type[] = [];
    let restType: RestType | null = null;

    const parameters = signature.getParameters();
    for (let i = 0; i < parameters.length; i += 1) {
      const param = parameters[i];
      const type = checker.getTypeOfSymbolAtLocation(param, tsNode);

      const decl = param.getDeclarations()?.[0];
      if (decl && isRestParameterDeclaration(decl)) {
        // is a rest param
        if (checker.isArrayType(type)) {
          restType = {
            type: checker.getTypeArguments(type)[0],
            index: i,
            kind: RestTypeKind.Array,
          };
        } else if (checker.isTupleType(type)) {
          restType = {
            index: i,
            kind: RestTypeKind.Tuple,
            typeArguments: checker.getTypeArguments(type),
          };
        } else {
          restType = {
            type,
            index: i,
            kind: RestTypeKind.Other,
          };
        }
        break;
      }

      paramTypes.push(type);
    }

    return new this(paramTypes, restType);
  }

  public consumeRemainingArguments(): void {
    this.hasConsumedArguments = true;
  }

  public getNextParameterType(): ts.Type | null {
    const index = this.parameterTypeIndex;
    this.parameterTypeIndex += 1;

    if (index >= this.paramTypes.length || this.hasConsumedArguments) {
      if (this.restType == null) {
        return null;
      }

      switch (this.restType.kind) {
        case RestTypeKind.Tuple: {
          const typeArguments = this.restType.typeArguments;
          if (this.hasConsumedArguments) {
            // all types consumed by a rest - just assume it's the last type
            // there is one edge case where this is wrong, but we ignore it because
            // it's rare and really complicated to handle
            // eg: function foo(...a: [number, ...string[], number])
            return typeArguments[typeArguments.length - 1];
          }

          const typeIndex = index - this.restType.index;
          if (typeIndex >= typeArguments.length) {
            return typeArguments[typeArguments.length - 1];
          }

          return typeArguments[typeIndex];
        }

        case RestTypeKind.Array:
        case RestTypeKind.Other:
          return this.restType.type;
      }
    }
    return this.paramTypes[index];
  }
}
```
</details>

#### Methods

##### `create(checker: ts.TypeChecker, tsNode: ts.CallLikeExpression): FunctionSignature | null`

<details><summary>Code</summary>

```ts
public static create(
    checker: ts.TypeChecker,
    tsNode: ts.CallLikeExpression,
  ): FunctionSignature | null {
    const signature = checker.getResolvedSignature(tsNode);
    if (!signature) {
      return null;
    }

    const paramTypes: ts.Type[] = [];
    let restType: RestType | null = null;

    const parameters = signature.getParameters();
    for (let i = 0; i < parameters.length; i += 1) {
      const param = parameters[i];
      const type = checker.getTypeOfSymbolAtLocation(param, tsNode);

      const decl = param.getDeclarations()?.[0];
      if (decl && isRestParameterDeclaration(decl)) {
        // is a rest param
        if (checker.isArrayType(type)) {
          restType = {
            type: checker.getTypeArguments(type)[0],
            index: i,
            kind: RestTypeKind.Array,
          };
        } else if (checker.isTupleType(type)) {
          restType = {
            index: i,
            kind: RestTypeKind.Tuple,
            typeArguments: checker.getTypeArguments(type),
          };
        } else {
          restType = {
            type,
            index: i,
            kind: RestTypeKind.Other,
          };
        }
        break;
      }

      paramTypes.push(type);
    }

    return new this(paramTypes, restType);
  }
```
</details>

##### `consumeRemainingArguments(): void`

<details><summary>Code</summary>

```ts
public consumeRemainingArguments(): void {
    this.hasConsumedArguments = true;
  }
```
</details>

##### `getNextParameterType(): ts.Type | null`

<details><summary>Code</summary>

```ts
public getNextParameterType(): ts.Type | null {
    const index = this.parameterTypeIndex;
    this.parameterTypeIndex += 1;

    if (index >= this.paramTypes.length || this.hasConsumedArguments) {
      if (this.restType == null) {
        return null;
      }

      switch (this.restType.kind) {
        case RestTypeKind.Tuple: {
          const typeArguments = this.restType.typeArguments;
          if (this.hasConsumedArguments) {
            // all types consumed by a rest - just assume it's the last type
            // there is one edge case where this is wrong, but we ignore it because
            // it's rare and really complicated to handle
            // eg: function foo(...a: [number, ...string[], number])
            return typeArguments[typeArguments.length - 1];
          }

          const typeIndex = index - this.restType.index;
          if (typeIndex >= typeArguments.length) {
            return typeArguments[typeArguments.length - 1];
          }

          return typeArguments[typeIndex];
        }

        case RestTypeKind.Array:
        case RestTypeKind.Other:
          return this.restType.type;
      }
    }
    return this.paramTypes[index];
  }
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = | 'unsafeArgument'
  | 'unsafeArraySpread'
  | 'unsafeSpread'
  | 'unsafeTupleSpread';
```

### `RestType`

```ts
type RestType = | {
      index: number;
      kind: RestTypeKind.Array;
      type: ts.Type;
    }
  | {
      index: number;
      kind: RestTypeKind.Other;
      type: ts.Type;
    }
  | {
      index: number;
      kind: RestTypeKind.Tuple;
      typeArguments: readonly ts.Type[];
    };
```


---