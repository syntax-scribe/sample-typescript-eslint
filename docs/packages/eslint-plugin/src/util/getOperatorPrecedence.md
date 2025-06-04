[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getOperatorPrecedence.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 📦 Imports | 4 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 1 |


## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)
- [Enums](#enums)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getOperatorPrecedence.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `SyntaxKind` | `typescript` |
| `ValueOf` | `./types` |


---

## Functions

### `getOperatorPrecedenceForNode(node: TSESTree.Node): OperatorPrecedence`

<details><summary>Code</summary>

```ts
export function getOperatorPrecedenceForNode(
  node: TSESTree.Node,
): OperatorPrecedence {
  switch (node.type) {
    case AST_NODE_TYPES.SpreadElement:
    case AST_NODE_TYPES.RestElement:
      return OperatorPrecedence.Spread;

    case AST_NODE_TYPES.YieldExpression:
    case AST_NODE_TYPES.ArrowFunctionExpression:
      return OperatorPrecedence.Yield;

    case AST_NODE_TYPES.ConditionalExpression:
      return OperatorPrecedence.Conditional;

    case AST_NODE_TYPES.SequenceExpression:
      return OperatorPrecedence.Comma;

    case AST_NODE_TYPES.AssignmentExpression:
    case AST_NODE_TYPES.BinaryExpression:
    case AST_NODE_TYPES.LogicalExpression:
      switch (node.operator) {
        case '==':
        case '+=':
        case '-=':
        case '**=':
        case '*=':
        case '/=':
        case '%=':
        case '<<=':
        case '>>=':
        case '>>>=':
        case '&=':
        case '^=':
        case '|=':
        case '||=':
        case '&&=':
        case '??=':
          return OperatorPrecedence.Assignment;

        default:
          return getBinaryOperatorPrecedence(node.operator);
      }

    case AST_NODE_TYPES.TSTypeAssertion:
    case AST_NODE_TYPES.TSNonNullExpression:
    case AST_NODE_TYPES.UnaryExpression:
    case AST_NODE_TYPES.AwaitExpression:
      return OperatorPrecedence.Unary;

    case AST_NODE_TYPES.UpdateExpression:
      // TODO: Should prefix `++` and `--` be moved to the `Update` precedence?
      if (node.prefix) {
        return OperatorPrecedence.Unary;
      }
      return OperatorPrecedence.Update;

    case AST_NODE_TYPES.ChainExpression:
      return getOperatorPrecedenceForNode(node.expression);

    case AST_NODE_TYPES.CallExpression:
      return OperatorPrecedence.LeftHandSide;

    case AST_NODE_TYPES.NewExpression:
      return node.arguments.length > 0
        ? OperatorPrecedence.Member
        : OperatorPrecedence.LeftHandSide;

    case AST_NODE_TYPES.TaggedTemplateExpression:
    case AST_NODE_TYPES.MemberExpression:
    case AST_NODE_TYPES.MetaProperty:
      return OperatorPrecedence.Member;

    case AST_NODE_TYPES.TSAsExpression:
      return OperatorPrecedence.Relational;

    case AST_NODE_TYPES.ThisExpression:
    case AST_NODE_TYPES.Super:
    case AST_NODE_TYPES.Identifier:
    case AST_NODE_TYPES.PrivateIdentifier:
    case AST_NODE_TYPES.Literal:
    case AST_NODE_TYPES.ArrayExpression:
    case AST_NODE_TYPES.ObjectExpression:
    case AST_NODE_TYPES.FunctionExpression:
    case AST_NODE_TYPES.ClassExpression:
    case AST_NODE_TYPES.TemplateLiteral:
    case AST_NODE_TYPES.JSXElement:
    case AST_NODE_TYPES.JSXFragment:
      // we don't have nodes for these cases
      // case SyntaxKind.ParenthesizedExpression:
      // case SyntaxKind.OmittedExpression:
      return OperatorPrecedence.Primary;

    default:
      return OperatorPrecedence.Invalid;
  }
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `OperatorPrecedence`
- **Calls**:
  - `getBinaryOperatorPrecedence`
  - `getOperatorPrecedenceForNode`
- **Internal Comments**:
```
// TODO: Should prefix `++` and `--` be moved to the `Update` precedence?
// we don't have nodes for these cases
// case SyntaxKind.ParenthesizedExpression:
// case SyntaxKind.OmittedExpression:
```

### `getOperatorPrecedence(nodeKind: SyntaxKind, operatorKind: SyntaxKind, hasArguments: boolean): OperatorPrecedence`

<details><summary>Code</summary>

```ts
export function getOperatorPrecedence(
  nodeKind: SyntaxKind,
  operatorKind: SyntaxKind,
  hasArguments?: boolean,
): OperatorPrecedence {
  switch (nodeKind) {
    // A list of comma-separated expressions. This node is only created by transformations.
    case SyntaxKind.CommaListExpression:
      return OperatorPrecedence.Comma;

    case SyntaxKind.SpreadElement:
      return OperatorPrecedence.Spread;

    case SyntaxKind.YieldExpression:
      return OperatorPrecedence.Yield;

    case SyntaxKind.ConditionalExpression:
      return OperatorPrecedence.Conditional;

    case SyntaxKind.BinaryExpression:
      switch (operatorKind) {
        case SyntaxKind.AmpersandAmpersandEqualsToken:
        case SyntaxKind.AmpersandEqualsToken:
        case SyntaxKind.AsteriskAsteriskEqualsToken:
        case SyntaxKind.AsteriskEqualsToken:
        case SyntaxKind.BarBarEqualsToken:
        case SyntaxKind.BarEqualsToken:
        case SyntaxKind.CaretEqualsToken:
        case SyntaxKind.EqualsToken:
        case SyntaxKind.GreaterThanGreaterThanEqualsToken:
        case SyntaxKind.GreaterThanGreaterThanGreaterThanEqualsToken:
        case SyntaxKind.LessThanLessThanEqualsToken:
        case SyntaxKind.MinusEqualsToken:
        case SyntaxKind.PercentEqualsToken:
        case SyntaxKind.PlusEqualsToken:
        case SyntaxKind.QuestionQuestionEqualsToken:
        case SyntaxKind.SlashEqualsToken:
          return OperatorPrecedence.Assignment;

        case SyntaxKind.CommaToken:
          return OperatorPrecedence.Comma;

        default:
          return getBinaryOperatorPrecedence(operatorKind);
      }

    // TODO: Should prefix `++` and `--` be moved to the `Update` precedence?
    case SyntaxKind.TypeAssertionExpression:
    case SyntaxKind.NonNullExpression:
    case SyntaxKind.PrefixUnaryExpression:
    case SyntaxKind.TypeOfExpression:
    case SyntaxKind.VoidExpression:
    case SyntaxKind.DeleteExpression:
    case SyntaxKind.AwaitExpression:
      return OperatorPrecedence.Unary;

    case SyntaxKind.PostfixUnaryExpression:
      return OperatorPrecedence.Update;

    case SyntaxKind.CallExpression:
      return OperatorPrecedence.LeftHandSide;

    case SyntaxKind.NewExpression:
      return hasArguments
        ? OperatorPrecedence.Member
        : OperatorPrecedence.LeftHandSide;

    case SyntaxKind.TaggedTemplateExpression:
    case SyntaxKind.PropertyAccessExpression:
    case SyntaxKind.ElementAccessExpression:
    case SyntaxKind.MetaProperty:
      return OperatorPrecedence.Member;

    case SyntaxKind.AsExpression:
    case SyntaxKind.SatisfiesExpression:
      return OperatorPrecedence.Relational;

    case SyntaxKind.ThisKeyword:
    case SyntaxKind.SuperKeyword:
    case SyntaxKind.Identifier:
    case SyntaxKind.PrivateIdentifier:
    case SyntaxKind.NullKeyword:
    case SyntaxKind.TrueKeyword:
    case SyntaxKind.FalseKeyword:
    case SyntaxKind.NumericLiteral:
    case SyntaxKind.BigIntLiteral:
    case SyntaxKind.StringLiteral:
    case SyntaxKind.ArrayLiteralExpression:
    case SyntaxKind.ObjectLiteralExpression:
    case SyntaxKind.FunctionExpression:
    case SyntaxKind.ArrowFunction:
    case SyntaxKind.ClassExpression:
    case SyntaxKind.RegularExpressionLiteral:
    case SyntaxKind.NoSubstitutionTemplateLiteral:
    case SyntaxKind.TemplateExpression:
    case SyntaxKind.ParenthesizedExpression:
    case SyntaxKind.OmittedExpression:
    case SyntaxKind.JsxElement:
    case SyntaxKind.JsxSelfClosingElement:
    case SyntaxKind.JsxFragment:
      return OperatorPrecedence.Primary;

    default:
      return OperatorPrecedence.Invalid;
  }
}
```
</details>

- **Parameters**:
  - `nodeKind: SyntaxKind`
  - `operatorKind: SyntaxKind`
  - `hasArguments: boolean`
- **Return Type**: `OperatorPrecedence`
- **Calls**:
  - `getBinaryOperatorPrecedence`
- **Internal Comments**:
```
// A list of comma-separated expressions. This node is only created by transformations.
// TODO: Should prefix `++` and `--` be moved to the `Update` precedence?
```

### `getBinaryOperatorPrecedence(kind: SyntaxKind | TSESTreeOperatorKind): OperatorPrecedence`

<details><summary>Code</summary>

```ts
export function getBinaryOperatorPrecedence(
  kind: SyntaxKind | TSESTreeOperatorKind,
): OperatorPrecedence {
  switch (kind) {
    case '-':
    case '+':
    case SyntaxKind.MinusToken:
    case SyntaxKind.PlusToken:
      return OperatorPrecedence.Additive;

    case '!=':
    case '!==':
    case '==':
    case '===':
    case SyntaxKind.EqualsEqualsEqualsToken:
    case SyntaxKind.EqualsEqualsToken:
    case SyntaxKind.ExclamationEqualsEqualsToken:
    case SyntaxKind.ExclamationEqualsToken:
      return OperatorPrecedence.Equality;

    case '??':
    case SyntaxKind.QuestionQuestionToken:
      return OperatorPrecedence.Coalesce;

    case '*':
    case '/':
    case '%':
    case SyntaxKind.AsteriskToken:
    case SyntaxKind.PercentToken:
    case SyntaxKind.SlashToken:
      return OperatorPrecedence.Multiplicative;

    case '**':
    case SyntaxKind.AsteriskAsteriskToken:
      return OperatorPrecedence.Exponentiation;

    case '&':
    case SyntaxKind.AmpersandToken:
      return OperatorPrecedence.BitwiseAND;

    case '&&':
    case SyntaxKind.AmpersandAmpersandToken:
      return OperatorPrecedence.LogicalAND;

    case '^':
    case SyntaxKind.CaretToken:
      return OperatorPrecedence.BitwiseXOR;

    case '<':
    case '<=':
    case '>':
    case '>=':
    case 'in':
    case 'instanceof':
    case SyntaxKind.AsKeyword:
    case SyntaxKind.GreaterThanEqualsToken:
    case SyntaxKind.GreaterThanToken:
    case SyntaxKind.InKeyword:
    case SyntaxKind.InstanceOfKeyword:
    case SyntaxKind.LessThanEqualsToken:
    case SyntaxKind.LessThanToken:
      // case 'as': -- we don't have a token for this
      return OperatorPrecedence.Relational;

    case '<<':
    case '>>':
    case '>>>':
    case SyntaxKind.GreaterThanGreaterThanGreaterThanToken:
    case SyntaxKind.GreaterThanGreaterThanToken:
    case SyntaxKind.LessThanLessThanToken:
      return OperatorPrecedence.Shift;

    case '|':
    case SyntaxKind.BarToken:
      return OperatorPrecedence.BitwiseOR;

    case '||':
    case SyntaxKind.BarBarToken:
      return OperatorPrecedence.LogicalOR;
  }

  // -1 is lower than all other precedences.  Returning it will cause binary expression
  // parsing to stop.
  return -1;
}
```
</details>

- **Parameters**:
  - `kind: SyntaxKind | TSESTreeOperatorKind`
- **Return Type**: `OperatorPrecedence`
- **Internal Comments**:
```
// case 'as': -- we don't have a token for this
// -1 is lower than all other precedences.  Returning it will cause binary expression
// parsing to stop.
```


---

## Type Aliases

### `TSESTreeOperatorKind`

```ts
type TSESTreeOperatorKind = | ValueOf<TSESTree.BinaryOperatorToText>
  | ValueOf<TSESTree.PunctuatorTokenToText>;
```


---

## Enums

### `enum OperatorPrecedence`

<details><summary>Enum Code</summary>

```ts
export enum OperatorPrecedence {
  // Expression:
  //     AssignmentExpression
  //     Expression `,` AssignmentExpression
  Comma,

  // NOTE: `Spread` is higher than `Comma` due to how it is parsed in |ElementList|
  // SpreadElement:
  //     `...` AssignmentExpression
  Spread,

  // AssignmentExpression:
  //     ConditionalExpression
  //     YieldExpression
  //     ArrowFunction
  //     AsyncArrowFunction
  //     LeftHandSideExpression `=` AssignmentExpression
  //     LeftHandSideExpression AssignmentOperator AssignmentExpression
  //
  // NOTE: AssignmentExpression is broken down into several precedences due to the requirements
  //       of the parenthesize rules.

  // AssignmentExpression: YieldExpression
  // YieldExpression:
  //     `yield`
  //     `yield` AssignmentExpression
  //     `yield` `*` AssignmentExpression
  Yield,

  // AssignmentExpression: LeftHandSideExpression `=` AssignmentExpression
  // AssignmentExpression: LeftHandSideExpression AssignmentOperator AssignmentExpression
  // AssignmentOperator: one of
  //     `*=` `/=` `%=` `+=` `-=` `<<=` `>>=` `>>>=` `&=` `^=` `|=` `**=`
  Assignment,

  // NOTE: `Conditional` is considered higher than `Assignment` here, but in reality they have
  //       the same precedence.
  // AssignmentExpression: ConditionalExpression
  // ConditionalExpression:
  //     ShortCircuitExpression
  //     ShortCircuitExpression `?` AssignmentExpression `:` AssignmentExpression
  // ShortCircuitExpression:
  //     LogicalORExpression
  //     CoalesceExpression
  Conditional,

  // CoalesceExpression:
  //     CoalesceExpressionHead `??` BitwiseORExpression
  // CoalesceExpressionHead:
  //     CoalesceExpression
  //     BitwiseORExpression
  Coalesce = Conditional, // NOTE: This is wrong

  // LogicalORExpression:
  //     LogicalANDExpression
  //     LogicalORExpression `||` LogicalANDExpression
  LogicalOR,

  // LogicalANDExpression:
  //     BitwiseORExpression
  //     LogicalANDExpression `&&` BitwiseORExpression
  LogicalAND,

  // BitwiseORExpression:
  //     BitwiseXORExpression
  //     BitwiseORExpression `^` BitwiseXORExpression
  BitwiseOR,

  // BitwiseXORExpression:
  //     BitwiseANDExpression
  //     BitwiseXORExpression `^` BitwiseANDExpression
  BitwiseXOR,

  // BitwiseANDExpression:
  //     EqualityExpression
  //     BitwiseANDExpression `^` EqualityExpression
  BitwiseAND,

  // EqualityExpression:
  //     RelationalExpression
  //     EqualityExpression `==` RelationalExpression
  //     EqualityExpression `!=` RelationalExpression
  //     EqualityExpression `===` RelationalExpression
  //     EqualityExpression `!==` RelationalExpression
  Equality,

  // RelationalExpression:
  //     ShiftExpression
  //     RelationalExpression `<` ShiftExpression
  //     RelationalExpression `>` ShiftExpression
  //     RelationalExpression `<=` ShiftExpression
  //     RelationalExpression `>=` ShiftExpression
  //     RelationalExpression `instanceof` ShiftExpression
  //     RelationalExpression `in` ShiftExpression
  //     [+TypeScript] RelationalExpression `as` Type
  Relational,

  // ShiftExpression:
  //     AdditiveExpression
  //     ShiftExpression `<<` AdditiveExpression
  //     ShiftExpression `>>` AdditiveExpression
  //     ShiftExpression `>>>` AdditiveExpression
  Shift,

  // AdditiveExpression:
  //     MultiplicativeExpression
  //     AdditiveExpression `+` MultiplicativeExpression
  //     AdditiveExpression `-` MultiplicativeExpression
  Additive,

  // MultiplicativeExpression:
  //     ExponentiationExpression
  //     MultiplicativeExpression MultiplicativeOperator ExponentiationExpression
  // MultiplicativeOperator: one of `*`, `/`, `%`
  Multiplicative,

  // ExponentiationExpression:
  //     UnaryExpression
  //     UpdateExpression `**` ExponentiationExpression
  Exponentiation,

  // UnaryExpression:
  //     UpdateExpression
  //     `delete` UnaryExpression
  //     `void` UnaryExpression
  //     `typeof` UnaryExpression
  //     `+` UnaryExpression
  //     `-` UnaryExpression
  //     `~` UnaryExpression
  //     `!` UnaryExpression
  //     AwaitExpression
  // UpdateExpression:            // TODO: Do we need to investigate the precedence here?
  //     `++` UnaryExpression
  //     `--` UnaryExpression
  Unary,

  // UpdateExpression:
  //     LeftHandSideExpression
  //     LeftHandSideExpression `++`
  //     LeftHandSideExpression `--`
  Update,

  // LeftHandSideExpression:
  //     NewExpression
  //     CallExpression
  // NewExpression:
  //     MemberExpression
  //     `new` NewExpression
  LeftHandSide,

  // CallExpression:
  //     CoverCallExpressionAndAsyncArrowHead
  //     SuperCall
  //     ImportCall
  //     CallExpression Arguments
  //     CallExpression `[` Expression `]`
  //     CallExpression `.` IdentifierName
  //     CallExpression TemplateLiteral
  // MemberExpression:
  //     PrimaryExpression
  //     MemberExpression `[` Expression `]`
  //     MemberExpression `.` IdentifierName
  //     MemberExpression TemplateLiteral
  //     SuperProperty
  //     MetaProperty
  //     `new` MemberExpression Arguments
  Member,

  // TODO: JSXElement?
  // PrimaryExpression:
  //     `this`
  //     IdentifierReference
  //     Literal
  //     ArrayLiteral
  //     ObjectLiteral
  //     FunctionExpression
  //     ClassExpression
  //     GeneratorExpression
  //     AsyncFunctionExpression
  //     AsyncGeneratorExpression
  //     RegularExpressionLiteral
  //     TemplateLiteral
  //     CoverParenthesizedExpressionAndArrowParameterList
  Primary,

  Highest = Primary,
  Lowest = Comma,
  // -1 is lower than all other precedences. Returning it will cause binary expression
  // parsing to stop.
  Invalid = -1,
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `Comma` | *auto* |  |
| `Spread` | *auto* |  |
| `Yield` | *auto* |  |
| `Assignment` | *auto* |  |
| `Conditional` | *auto* |  |
| `Coalesce` | `Conditional` |  |
| `LogicalOR` | *auto* |  |
| `LogicalAND` | *auto* |  |
| `BitwiseOR` | *auto* |  |
| `BitwiseXOR` | *auto* |  |
| `BitwiseAND` | *auto* |  |
| `Equality` | *auto* |  |
| `Relational` | *auto* |  |
| `Shift` | *auto* |  |
| `Additive` | *auto* |  |
| `Multiplicative` | *auto* |  |
| `Exponentiation` | *auto* |  |
| `Unary` | *auto* |  |
| `Update` | *auto* |  |
| `LeftHandSide` | *auto* |  |
| `Member` | *auto* |  |
| `Primary` | *auto* |  |
| `Highest` | `Primary` |  |
| `Lowest` | `Comma` |  |
| `Invalid` | `-1` |  |


---