[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `gatherLogicalOperands.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 🧱 Classes | 0 |
| 📦 Imports | 12 |
| 📊 Variables & Constants | 10 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)
- [Enums](#enums)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-optional-chain-utils/gatherLogicalOperands.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserServicesWithTypeInformation` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `SourceCode` | `@typescript-eslint/utils/ts-eslint` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `isBigIntLiteralType` | `ts-api-utils` |
| `isBooleanLiteralType` | `ts-api-utils` |
| `isNumberLiteralType` | `ts-api-utils` |
| `isStringLiteralType` | `ts-api-utils` |
| `unionConstituents` | `ts-api-utils` |
| `PreferOptionalChainOptions` | `./PreferOptionalChainOptions` |
| `isReferenceToGlobalFunction` | `../../util` |
| `isTypeFlagSet` | `../../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `NULLISH_FLAGS` | `number` | const | `ts.TypeFlags.Null | ts.TypeFlags.Undefined` | ✗ |
| `allowedFlags` | `number` | let/var | `NULLISH_FLAGS | ts.TypeFlags.Object` | ✗ |
| `result` | `Operand[]` | const | `[]` | ✗ |
| `areMoreOperands` | `boolean` | const | `operand !== operands.at(-1)` | ✗ |
| `argument` | `any` | const | `comparedExpression.argument` | ✗ |
| `comparedName` | `any` | const | `comparedExpression` | ✗ |
| `operands` | `TSESTree.Expression[]` | const | `[]` | ✗ |
| `newlySeenLogicals` | `Set<TSESTree.LogicalExpression>` | const | `new Set<TSESTree.LogicalExpression>([node])` | ✗ |
| `stack` | `TSESTree.Expression[]` | const | `[node.right, node.left]` | ✗ |
| `current` | `TSESTree.Expression | undefined` | let/var | `*not shown*` | ✗ |


---

## Functions

### `isValidFalseBooleanCheckType(node: TSESTree.Node, disallowFalseyLiteral: boolean, parserServices: ParserServicesWithTypeInformation, options: PreferOptionalChainOptions): boolean`

<details><summary>Code</summary>

```ts
function isValidFalseBooleanCheckType(
  node: TSESTree.Node,
  disallowFalseyLiteral: boolean,
  parserServices: ParserServicesWithTypeInformation,
  options: PreferOptionalChainOptions,
): boolean {
  const type = parserServices.getTypeAtLocation(node);
  const types = unionConstituents(type);

  if (
    disallowFalseyLiteral &&
    /*
    ```
    declare const x: false | {a: string};
    x && x.a;
    !x || x.a;
    ```

    We don't want to consider these two cases because the boolean expression
    narrows out the non-nullish falsy cases - so converting the chain to `x?.a`
    would introduce a build error
    */ (types.some(
      t => isBooleanLiteralType(t) && t.intrinsicName === 'false',
    ) ||
      types.some(t => isStringLiteralType(t) && t.value === '') ||
      types.some(t => isNumberLiteralType(t) && t.value === 0) ||
      types.some(t => isBigIntLiteralType(t) && t.value.base10Value === '0'))
  ) {
    return false;
  }

  let allowedFlags = NULLISH_FLAGS | ts.TypeFlags.Object;
  if (options.checkAny === true) {
    allowedFlags |= ts.TypeFlags.Any;
  }
  if (options.checkUnknown === true) {
    allowedFlags |= ts.TypeFlags.Unknown;
  }
  if (options.checkString === true) {
    allowedFlags |= ts.TypeFlags.StringLike;
  }
  if (options.checkNumber === true) {
    allowedFlags |= ts.TypeFlags.NumberLike;
  }
  if (options.checkBoolean === true) {
    allowedFlags |= ts.TypeFlags.BooleanLike;
  }
  if (options.checkBigInt === true) {
    allowedFlags |= ts.TypeFlags.BigIntLike;
  }
  return types.every(t => isTypeFlagSet(t, allowedFlags));
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `disallowFalseyLiteral: boolean`
  - `parserServices: ParserServicesWithTypeInformation`
  - `options: PreferOptionalChainOptions`
- **Return Type**: `boolean`
- **Calls**:
  - `parserServices.getTypeAtLocation`
  - `unionConstituents (from ts-api-utils)`
  - `types.some`
  - `isBooleanLiteralType (from ts-api-utils)`
  - `isStringLiteralType (from ts-api-utils)`
  - `isNumberLiteralType (from ts-api-utils)`
  - `isBigIntLiteralType (from ts-api-utils)`
  - `types.every`
  - `isTypeFlagSet (from ../../util)`
- **Internal Comments**:
```
/*
    ```
    declare const x: false | {a: string};
    x && x.a;
    !x || x.a;
    ```

    We don't want to consider these two cases because the boolean expression
    narrows out the non-nullish falsy cases - so converting the chain to `x?.a`
    would introduce a build error
    */
```

### `gatherLogicalOperands(node: TSESTree.LogicalExpression, parserServices: ParserServicesWithTypeInformation, sourceCode: Readonly<SourceCode>, options: PreferOptionalChainOptions): {
  newlySeenLogicals: Set<TSESTree.LogicalExpression>;
  operands: Operand[];
}`

<details><summary>Code</summary>

```ts
export function gatherLogicalOperands(
  node: TSESTree.LogicalExpression,
  parserServices: ParserServicesWithTypeInformation,
  sourceCode: Readonly<SourceCode>,
  options: PreferOptionalChainOptions,
): {
  newlySeenLogicals: Set<TSESTree.LogicalExpression>;
  operands: Operand[];
} {
  const result: Operand[] = [];
  const { newlySeenLogicals, operands } = flattenLogicalOperands(node);

  for (const operand of operands) {
    const areMoreOperands = operand !== operands.at(-1);
    switch (operand.type) {
      case AST_NODE_TYPES.BinaryExpression: {
        // check for "yoda" style logical: null != x

        const { comparedExpression, comparedValue, isYoda } = (() => {
          // non-yoda checks are by far the most common, so check for them first
          const comparedValueRight = getComparisonValueType(operand.right);
          if (comparedValueRight) {
            return {
              comparedExpression: operand.left,
              comparedValue: comparedValueRight,
              isYoda: false,
            };
          }
          return {
            comparedExpression: operand.right,
            comparedValue: getComparisonValueType(operand.left),
            isYoda: true,
          };
        })();

        if (comparedValue === ComparisonValueType.UndefinedStringLiteral) {
          if (
            comparedExpression.type === AST_NODE_TYPES.UnaryExpression &&
            comparedExpression.operator === 'typeof'
          ) {
            const argument = comparedExpression.argument;
            if (
              argument.type === AST_NODE_TYPES.Identifier &&
              // typeof window === 'undefined'
              isReferenceToGlobalFunction(argument.name, argument, sourceCode)
            ) {
              result.push({ type: OperandValidity.Invalid });
              continue;
            }

            // typeof x.y === 'undefined'
            result.push({
              comparedName: comparedExpression.argument,
              comparisonType: operand.operator.startsWith('!')
                ? NullishComparisonType.NotStrictEqualUndefined
                : NullishComparisonType.StrictEqualUndefined,
              isYoda,
              node: operand,
              type: OperandValidity.Valid,
            });
            continue;
          }

          // y === 'undefined'
          result.push({ type: OperandValidity.Invalid });
          continue;
        }

        switch (operand.operator) {
          case '!=':
          case '==':
            if (
              comparedValue === ComparisonValueType.Null ||
              comparedValue === ComparisonValueType.Undefined
            ) {
              // x == null, x == undefined
              result.push({
                comparedName: comparedExpression,
                comparisonType: operand.operator.startsWith('!')
                  ? NullishComparisonType.NotEqualNullOrUndefined
                  : NullishComparisonType.EqualNullOrUndefined,
                isYoda,
                node: operand,
                type: OperandValidity.Valid,
              });
              continue;
            }
            // x == something :(
            result.push({ type: OperandValidity.Invalid });
            continue;

          case '!==':
          case '===': {
            const comparedName = comparedExpression;
            switch (comparedValue) {
              case ComparisonValueType.Null:
                result.push({
                  comparedName,
                  comparisonType: operand.operator.startsWith('!')
                    ? NullishComparisonType.NotStrictEqualNull
                    : NullishComparisonType.StrictEqualNull,
                  isYoda,
                  node: operand,
                  type: OperandValidity.Valid,
                });
                continue;

              case ComparisonValueType.Undefined:
                result.push({
                  comparedName,
                  comparisonType: operand.operator.startsWith('!')
                    ? NullishComparisonType.NotStrictEqualUndefined
                    : NullishComparisonType.StrictEqualUndefined,
                  isYoda,
                  node: operand,
                  type: OperandValidity.Valid,
                });
                continue;

              default:
                // x === something :(
                result.push({ type: OperandValidity.Invalid });
                continue;
            }
          }
        }

        result.push({ type: OperandValidity.Invalid });
        continue;
      }

      case AST_NODE_TYPES.UnaryExpression:
        if (
          operand.operator === '!' &&
          isValidFalseBooleanCheckType(
            operand.argument,
            areMoreOperands && node.operator === '||',
            parserServices,
            options,
          )
        ) {
          result.push({
            comparedName: operand.argument,
            comparisonType: NullishComparisonType.NotBoolean,
            isYoda: false,
            node: operand,
            type: OperandValidity.Valid,
          });
          continue;
        }
        result.push({ type: OperandValidity.Invalid });
        continue;

      case AST_NODE_TYPES.LogicalExpression:
        // explicitly ignore the mixed logical expression cases
        result.push({ type: OperandValidity.Invalid });
        continue;

      default:
        if (
          isValidFalseBooleanCheckType(
            operand,
            areMoreOperands && node.operator === '&&',
            parserServices,
            options,
          )
        ) {
          result.push({
            comparedName: operand,
            comparisonType: NullishComparisonType.Boolean,
            isYoda: false,
            node: operand,
            type: OperandValidity.Valid,
          });
        } else {
          result.push({ type: OperandValidity.Invalid });
        }
        continue;
    }
  }

  return {
    newlySeenLogicals,
    operands: result,
  };

  /*
  The AST is always constructed such the first element is always the deepest element.
  I.e. for this code: `foo && foo.bar && foo.bar.baz && foo.bar.baz.buzz`
  The AST will look like this:
  {
    left: {
      left: {
        left: foo
        right: foo.bar
      }
      right: foo.bar.baz
    }
    right: foo.bar.baz.buzz
  }

  So given any logical expression, we can perform a depth-first traversal to get
  the operands in order.

  Note that this function purposely does not inspect mixed logical expressions
  like `foo || foo.bar && foo.bar.baz` - separate selector
  */
  function flattenLogicalOperands(node: TSESTree.LogicalExpression): {
    newlySeenLogicals: Set<TSESTree.LogicalExpression>;
    operands: TSESTree.Expression[];
  } {
    const operands: TSESTree.Expression[] = [];
    const newlySeenLogicals = new Set<TSESTree.LogicalExpression>([node]);

    const stack: TSESTree.Expression[] = [node.right, node.left];
    let current: TSESTree.Expression | undefined;
    while ((current = stack.pop())) {
      if (
        current.type === AST_NODE_TYPES.LogicalExpression &&
        current.operator === node.operator
      ) {
        newlySeenLogicals.add(current);
        stack.push(current.right);
        stack.push(current.left);
      } else {
        operands.push(current);
      }
    }

    return {
      newlySeenLogicals,
      operands,
    };
  }

  function getComparisonValueType(
    node: TSESTree.Node,
  ): ComparisonValueType | null {
    switch (node.type) {
      case AST_NODE_TYPES.Literal:
        // eslint-disable-next-line eqeqeq, @typescript-eslint/internal/eqeq-nullish -- intentional exact comparison against null
        if (node.value === null && node.raw === 'null') {
          return ComparisonValueType.Null;
        }
        if (node.value === 'undefined') {
          return ComparisonValueType.UndefinedStringLiteral;
        }
        return null;

      case AST_NODE_TYPES.Identifier:
        if (node.name === 'undefined') {
          return ComparisonValueType.Undefined;
        }
        return null;
    }

    return null;
  }
}
```
</details>

- **Parameters**:
  - `node: TSESTree.LogicalExpression`
  - `parserServices: ParserServicesWithTypeInformation`
  - `sourceCode: Readonly<SourceCode>`
  - `options: PreferOptionalChainOptions`
- **Return Type**: `{
  newlySeenLogicals: Set<TSESTree.LogicalExpression>;
  operands: Operand[];
}`
- **Calls**:
  - `flattenLogicalOperands`
  - `operands.at`
  - `complex_call_4204`
  - `getComparisonValueType`
  - `isReferenceToGlobalFunction (from ../../util)`
  - `result.push`
  - `operand.operator.startsWith`
  - `isValidFalseBooleanCheckType`
  - `stack.pop`
  - `newlySeenLogicals.add`
  - `stack.push`
  - `operands.push`
- **Internal Comments**:
```
// check for "yoda" style logical: null != x (x2)
// non-yoda checks are by far the most common, so check for them first (x2)
// typeof window === 'undefined' (x2)
// typeof x.y === 'undefined' (x4)
// y === 'undefined' (x4)
// x == null, x == undefined (x4)
// x == something :( (x4)
// x === something :( (x4)
// explicitly ignore the mixed logical expression cases (x4)
/*
  The AST is always constructed such the first element is always the deepest element.
  I.e. for this code: `foo && foo.bar && foo.bar.baz && foo.bar.baz.buzz`
  The AST will look like this:
  {
    left: {
      left: {
        left: foo
        right: foo.bar
      }
      right: foo.bar.baz
    }
    right: foo.bar.baz.buzz
  }

  So given any logical expression, we can perform a depth-first traversal to get
  the operands in order.

  Note that this function purposely does not inspect mixed logical expressions
  like `foo || foo.bar && foo.bar.baz` - separate selector
  */
// eslint-disable-next-line eqeqeq, @typescript-eslint/internal/eqeq-nullish -- intentional exact comparison against null
```

### `flattenLogicalOperands(node: TSESTree.LogicalExpression): {
    newlySeenLogicals: Set<TSESTree.LogicalExpression>;
    operands: TSESTree.Expression[];
  }`

<details><summary>Code</summary>

```ts
function flattenLogicalOperands(node: TSESTree.LogicalExpression): {
    newlySeenLogicals: Set<TSESTree.LogicalExpression>;
    operands: TSESTree.Expression[];
  } {
    const operands: TSESTree.Expression[] = [];
    const newlySeenLogicals = new Set<TSESTree.LogicalExpression>([node]);

    const stack: TSESTree.Expression[] = [node.right, node.left];
    let current: TSESTree.Expression | undefined;
    while ((current = stack.pop())) {
      if (
        current.type === AST_NODE_TYPES.LogicalExpression &&
        current.operator === node.operator
      ) {
        newlySeenLogicals.add(current);
        stack.push(current.right);
        stack.push(current.left);
      } else {
        operands.push(current);
      }
    }

    return {
      newlySeenLogicals,
      operands,
    };
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.LogicalExpression`
- **Return Type**: `{
    newlySeenLogicals: Set<TSESTree.LogicalExpression>;
    operands: TSESTree.Expression[];
  }`
- **Calls**:
  - `stack.pop`
  - `newlySeenLogicals.add`
  - `stack.push`
  - `operands.push`
### `getComparisonValueType(node: TSESTree.Node): ComparisonValueType | null`

<details><summary>Code</summary>

```ts
function getComparisonValueType(
    node: TSESTree.Node,
  ): ComparisonValueType | null {
    switch (node.type) {
      case AST_NODE_TYPES.Literal:
        // eslint-disable-next-line eqeqeq, @typescript-eslint/internal/eqeq-nullish -- intentional exact comparison against null
        if (node.value === null && node.raw === 'null') {
          return ComparisonValueType.Null;
        }
        if (node.value === 'undefined') {
          return ComparisonValueType.UndefinedStringLiteral;
        }
        return null;

      case AST_NODE_TYPES.Identifier:
        if (node.name === 'undefined') {
          return ComparisonValueType.Undefined;
        }
        return null;
    }

    return null;
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `ComparisonValueType | null`
- **Internal Comments**:
```
// eslint-disable-next-line eqeqeq, @typescript-eslint/internal/eqeq-nullish -- intentional exact comparison against null
```


---

## Interfaces

### `ValidOperand`

<details><summary>Interface Code</summary>

```ts
export interface ValidOperand {
  comparedName: TSESTree.Node;
  comparisonType: NullishComparisonType;
  isYoda: boolean;
  node: TSESTree.Expression;
  type: OperandValidity.Valid;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `comparedName` | `TSESTree.Node` | ✗ |  |
| `comparisonType` | `NullishComparisonType` | ✗ |  |
| `isYoda` | `boolean` | ✗ |  |
| `node` | `TSESTree.Expression` | ✗ |  |
| `type` | `OperandValidity.Valid` | ✗ |  |

### `InvalidOperand`

<details><summary>Interface Code</summary>

```ts
export interface InvalidOperand {
  type: OperandValidity.Invalid;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `OperandValidity.Invalid` | ✗ |  |


---

## Type Aliases

### `Operand`

```ts
type Operand = InvalidOperand | ValidOperand;
```


---

## Enums

### `const enum ComparisonValueType`

<details><summary>Enum Code</summary>

```ts
const enum ComparisonValueType {
  Null = 'Null', // eslint-disable-line @typescript-eslint/internal/prefer-ast-types-enum
  Undefined = 'Undefined',
  UndefinedStringLiteral = 'UndefinedStringLiteral',
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `Null` | `Null` |  |
| `Undefined` | `Undefined` |  |
| `UndefinedStringLiteral` | `UndefinedStringLiteral` |  |

### `const enum OperandValidity`

<details><summary>Enum Code</summary>

```ts
export const enum OperandValidity {
  Valid = 'Valid',
  Invalid = 'Invalid',
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `Valid` | `Valid` |  |
| `Invalid` | `Invalid` |  |

### `const enum NullishComparisonType`

<details><summary>Enum Code</summary>

```ts
export const enum NullishComparisonType {
  /** `x != null`, `x != undefined` */
  NotEqualNullOrUndefined = 'NotEqualNullOrUndefined',
  /** `x == null`, `x == undefined` */
  EqualNullOrUndefined = 'EqualNullOrUndefined',

  /** `x !== null` */
  NotStrictEqualNull = 'NotStrictEqualNull',
  /** `x === null` */
  StrictEqualNull = 'StrictEqualNull',

  /** `x !== undefined`, `typeof x !== 'undefined'` */
  NotStrictEqualUndefined = 'NotStrictEqualUndefined',
  /** `x === undefined`, `typeof x === 'undefined'` */
  StrictEqualUndefined = 'StrictEqualUndefined',

  /** `!x` */
  NotBoolean = 'NotBoolean',
  /** `x` */
  Boolean = 'Boolean', // eslint-disable-line @typescript-eslint/internal/prefer-ast-types-enum
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `NotEqualNullOrUndefined` | `NotEqualNullOrUndefined` | / `x != null`, `x != undefined` */ |
| `EqualNullOrUndefined` | `EqualNullOrUndefined` | / `x == null`, `x == undefined` */ |
| `NotStrictEqualNull` | `NotStrictEqualNull` | / `x !== null` */ |
| `StrictEqualNull` | `StrictEqualNull` | / `x === null` */ |
| `NotStrictEqualUndefined` | `NotStrictEqualUndefined` | / `x !== undefined`, `typeof x !== 'undefined'` */ |
| `StrictEqualUndefined` | `StrictEqualUndefined` | / `x === undefined`, `typeof x === 'undefined'` */ |
| `NotBoolean` | `NotBoolean` | / `!x` */ |
| `Boolean` | `Boolean` | / `x` */ |


---