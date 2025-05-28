[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `member-ordering.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 19 |
| 🧱 Classes | 0 |
| 📦 Imports | 9 |
| 📊 Variables & Constants | 29 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 15 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/member-ordering.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema` | `@typescript-eslint/utils` |
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `naturalCompare` | `natural-compare` |
| `createRule` | `../util` |
| `getNameFromIndexSignature` | `../util` |
| `getNameFromMember` | `../util` |
| `MemberNameType` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `neverConfig` | `JSONSchema.JSONSchema4` | const | `{
  type: 'string',
  enum: ['never'],
}` | ✗ |
| `defaultOrder` | `MemberType[]` | const | `[
  // Index signature
  'signature',
  'call-signature',

  // Fields
  'public-static-field',
  'protected-static-field',
  'private-static-field',
  '#private-static-field',

  'public-decorated-field',
  'protected-decorated-field',
  'private-decorated-field',

  'public-instance-field',
  'protected-instance-field',
  'private-instance-field',
  '#private-instance-field',

  'public-abstract-field',
  'protected-abstract-field',

  'public-field',
  'protected-field',
  'private-field',
  '#private-field',

  'static-field',
  'instance-field',
  'abstract-field',

  'decorated-field',

  'field',

  // Static initialization
  'static-initialization',

  // Constructors
  'public-constructor',
  'protected-constructor',
  'private-constructor',

  'constructor',

  // Accessors
  'public-static-accessor',
  'protected-static-accessor',
  'private-static-accessor',
  '#private-static-accessor',

  'public-decorated-accessor',
  'protected-decorated-accessor',
  'private-decorated-accessor',

  'public-instance-accessor',
  'protected-instance-accessor',
  'private-instance-accessor',
  '#private-instance-accessor',

  'public-abstract-accessor',
  'protected-abstract-accessor',

  'public-accessor',
  'protected-accessor',
  'private-accessor',
  '#private-accessor',

  'static-accessor',
  'instance-accessor',
  'abstract-accessor',

  'decorated-accessor',

  'accessor',

  // Getters
  'public-static-get',
  'protected-static-get',
  'private-static-get',
  '#private-static-get',

  'public-decorated-get',
  'protected-decorated-get',
  'private-decorated-get',

  'public-instance-get',
  'protected-instance-get',
  'private-instance-get',
  '#private-instance-get',

  'public-abstract-get',
  'protected-abstract-get',

  'public-get',
  'protected-get',
  'private-get',
  '#private-get',

  'static-get',
  'instance-get',
  'abstract-get',

  'decorated-get',

  'get',

  // Setters
  'public-static-set',
  'protected-static-set',
  'private-static-set',
  '#private-static-set',

  'public-decorated-set',
  'protected-decorated-set',
  'private-decorated-set',

  'public-instance-set',
  'protected-instance-set',
  'private-instance-set',
  '#private-instance-set',

  'public-abstract-set',
  'protected-abstract-set',

  'public-set',
  'protected-set',
  'private-set',
  '#private-set',

  'static-set',
  'instance-set',
  'abstract-set',

  'decorated-set',

  'set',

  // Methods
  'public-static-method',
  'protected-static-method',
  'private-static-method',
  '#private-static-method',

  'public-decorated-method',
  'protected-decorated-method',
  'private-decorated-method',

  'public-instance-method',
  'protected-instance-method',
  'private-instance-method',
  '#private-instance-method',

  'public-abstract-method',
  'protected-abstract-method',

  'public-method',
  'protected-method',
  'private-method',
  '#private-method',

  'static-method',
  'instance-method',
  'abstract-method',

  'decorated-method',

  'method',
]` | ✓ |
| `allMemberTypes` | `BaseMemberType[]` | const | `[
  ...new Set(
    (
      [
        'readonly-signature',
        'signature',
        'readonly-field',
        'field',
        'method',
        'call-signature',
        'constructor',
        'accessor',
        'get',
        'set',
        'static-initialization',
      ] as const
    ).flatMap(type => [
      type,

      ...(['public', 'protected', 'private', '#private'] as const)
        .flatMap<MemberType>(accessibility => [
          type !== 'readonly-signature' &&
          type !== 'signature' &&
          type !== 'static-initialization' &&
          type !== 'call-signature' &&
          !(type === 'constructor' && accessibility === '#private')
            ? `${accessibility}-${type}` // e.g. `public-field`
            : [],

          // Only class instance fields, methods, accessors, get and set can have decorators attached to them
          accessibility !== '#private' &&
          (type === 'readonly-field' ||
            type === 'field' ||
            type === 'method' ||
            type === 'accessor' ||
            type === 'get' ||
            type === 'set')
            ? [`${accessibility}-decorated-${type}`, `decorated-${type}`]
            : [],

          type !== 'constructor' &&
          type !== 'readonly-signature' &&
          type !== 'signature' &&
          type !== 'call-signature'
            ? (
                [
                  'static',
                  'instance',
                  // There is no `static-constructor` or `instance-constructor` or `abstract-constructor`
                  ...(accessibility === '#private' ||
                  accessibility === 'private'
                    ? []
                    : (['abstract'] as const)),
                ] as const
              ).flatMap(
                scope =>
                  [
                    `${scope}-${type}`,
                    `${accessibility}-${scope}-${type}`,
                  ] as const,
              )
            : [],
        ])
        .flat(),
    ]),
  ),
]` | ✗ |
| `functionExpressions` | `any[]` | const | `[
  AST_NODE_TYPES.FunctionExpression,
  AST_NODE_TYPES.ArrowFunctionExpression,
]` | ✗ |
| `rank` | `number` | let/var | `-1` | ✗ |
| `stack` | `BaseMemberType[]` | const | `[...memberGroups]` | ✗ |
| `memberGroup` | `BaseMemberType` | const | `stack.shift()!` | ✗ |
| `abstract` | `boolean` | const | `node.type === AST_NODE_TYPES.TSAbstractAccessorProperty ||
    node.type === AST_NODE_TYPES.TSAbstractPropertyDefinition ||
    node.type === AST_NODE_TYPES.TSAbstractMethodDefinition` | ✗ |
| `scope` | `"abstract" | "instance" | "static"` | const | `'static' in node && node.static
      ? 'static'
      : abstract
        ? 'abstract'
        : 'instance'` | ✗ |
| `memberGroups` | `BaseMemberType[]` | const | `[]` | ✗ |
| `decorated` | `boolean` | const | `'decorators' in node && node.decorators.length > 0` | ✗ |
| `groupedMembers` | `Member[][]` | const | `[]` | ✗ |
| `previousRank` | `number | undefined` | let/var | `undefined` | ✗ |
| `rankOfCurrentMember` | `number` | const | `memberRanks[index]` | ✗ |
| `rankOfNextMember` | `number` | const | `memberRanks[index + 1]` | ✗ |
| `lowest` | `number` | let/var | `ranks[ranks.length - 1]` | ✗ |
| `lowestRank` | `MemberType` | const | `order[lowest]` | ✗ |
| `lowestRanks` | `BaseMemberType[]` | const | `Array.isArray(lowestRank) ? lowestRank : [lowestRank]` | ✗ |
| `previousRanks` | `number[]` | const | `[]` | ✗ |
| `memberGroups` | `Member[][]` | const | `[]` | ✗ |
| `isCorrectlySorted` | `boolean` | let/var | `true` | ✗ |
| `rankLastMember` | `number` | const | `previousRanks[previousRanks.length - 1]` | ✗ |
| `previousName` | `string` | let/var | `''` | ✗ |
| `isCorrectlySorted` | `boolean` | let/var | `true` | ✗ |
| `order` | `Order | undefined` | let/var | `*not shown*` | ✗ |
| `memberTypes` | `string | MemberType[] | undefined` | let/var | `*not shown*` | ✗ |
| `optionalityOrder` | `OptionalityOrder | undefined` | let/var | `*not shown*` | ✗ |
| `hasAlphaSort` | `boolean` | const | `!!(order && order !== 'as-written')` | ✗ |
| `hasAlphaSort` | `boolean` | const | `!!(order && order !== 'as-written')` | ✗ |


---

## Functions

### `arrayConfig(memberTypes: string): JSONSchema.JSONSchema4`

<details><summary>Code</summary>

```ts
(memberTypes: string): JSONSchema.JSONSchema4 => ({
  type: 'array',
  items: {
    oneOf: [
      {
        $ref: memberTypes,
      },
      {
        type: 'array',
        items: {
          $ref: memberTypes,
        },
      },
    ],
  },
})
```
</details>

- **Parameters**:
  - `memberTypes: string`
- **Return Type**: `JSONSchema.JSONSchema4`
### `objectConfig(memberTypes: string): JSONSchema.JSONSchema4`

<details><summary>Code</summary>

```ts
(memberTypes: string): JSONSchema.JSONSchema4 => ({
  type: 'object',
  additionalProperties: false,
  properties: {
    memberTypes: {
      oneOf: [arrayConfig(memberTypes), neverConfig],
    },
    optionalityOrder: {
      $ref: '#/items/0/$defs/optionalityOrderOptions',
    },
    order: {
      $ref: '#/items/0/$defs/orderOptions',
    },
  },
})
```
</details>

- **Parameters**:
  - `memberTypes: string`
- **Return Type**: `JSONSchema.JSONSchema4`
### `getNodeType(node: Member): MemberKind | null`

<details><summary>Code</summary>

```ts
function getNodeType(node: Member): MemberKind | null {
  switch (node.type) {
    case AST_NODE_TYPES.TSAbstractMethodDefinition:
    case AST_NODE_TYPES.MethodDefinition:
    case AST_NODE_TYPES.TSMethodSignature:
      return node.kind;
    case AST_NODE_TYPES.TSCallSignatureDeclaration:
      return 'call-signature';
    case AST_NODE_TYPES.TSConstructSignatureDeclaration:
      return 'constructor';
    case AST_NODE_TYPES.TSAbstractPropertyDefinition:
    case AST_NODE_TYPES.TSPropertySignature:
      return node.readonly ? 'readonly-field' : 'field';
    case AST_NODE_TYPES.TSAbstractAccessorProperty:
    case AST_NODE_TYPES.AccessorProperty:
      return 'accessor';
    case AST_NODE_TYPES.PropertyDefinition:
      return node.value && functionExpressions.includes(node.value.type)
        ? 'method'
        : node.readonly
          ? 'readonly-field'
          : 'field';
    case AST_NODE_TYPES.TSIndexSignature:
      return node.readonly ? 'readonly-signature' : 'signature';
    case AST_NODE_TYPES.StaticBlock:
      return 'static-initialization';
    default:
      return null;
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets the node type.
 *
 * @param node the node to be evaluated.
 */
```

- **Parameters**:
  - `node: Member`
- **Return Type**: `MemberKind | null`
- **Calls**:
  - `functionExpressions.includes`
### `getMemberRawName(member: | TSESTree.AccessorProperty
    | TSESTree.MethodDefinition
    | TSESTree.Property
    | TSESTree.PropertyDefinition
    | TSESTree.TSAbstractAccessorProperty
    | TSESTree.TSAbstractMethodDefinition
    | TSESTree.TSAbstractPropertyDefinition
    | TSESTree.TSMethodSignature
    | TSESTree.TSPropertySignature, sourceCode: TSESLint.SourceCode): string`

<details><summary>Code</summary>

```ts
function getMemberRawName(
  member:
    | TSESTree.AccessorProperty
    | TSESTree.MethodDefinition
    | TSESTree.Property
    | TSESTree.PropertyDefinition
    | TSESTree.TSAbstractAccessorProperty
    | TSESTree.TSAbstractMethodDefinition
    | TSESTree.TSAbstractPropertyDefinition
    | TSESTree.TSMethodSignature
    | TSESTree.TSPropertySignature,
  sourceCode: TSESLint.SourceCode,
): string {
  const { name, type } = getNameFromMember(member, sourceCode);

  if (type === MemberNameType.Quoted) {
    return name.slice(1, -1);
  }
  if (type === MemberNameType.Private) {
    return name.slice(1);
  }
  return name;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets the raw string value of a member's name
 */
```

- **Parameters**:
  - `member: | TSESTree.AccessorProperty
    | TSESTree.MethodDefinition
    | TSESTree.Property
    | TSESTree.PropertyDefinition
    | TSESTree.TSAbstractAccessorProperty
    | TSESTree.TSAbstractMethodDefinition
    | TSESTree.TSAbstractPropertyDefinition
    | TSESTree.TSMethodSignature
    | TSESTree.TSPropertySignature`
  - `sourceCode: TSESLint.SourceCode`
- **Return Type**: `string`
- **Calls**:
  - `getNameFromMember (from ../util)`
  - `name.slice`
### `getMemberName(node: Member, sourceCode: TSESLint.SourceCode): string | null`

<details><summary>Code</summary>

```ts
function getMemberName(
  node: Member,
  sourceCode: TSESLint.SourceCode,
): string | null {
  switch (node.type) {
    case AST_NODE_TYPES.TSPropertySignature:
    case AST_NODE_TYPES.TSMethodSignature:
    case AST_NODE_TYPES.TSAbstractAccessorProperty:
    case AST_NODE_TYPES.TSAbstractPropertyDefinition:
    case AST_NODE_TYPES.AccessorProperty:
    case AST_NODE_TYPES.PropertyDefinition:
      return getMemberRawName(node, sourceCode);
    case AST_NODE_TYPES.TSAbstractMethodDefinition:
    case AST_NODE_TYPES.MethodDefinition:
      return node.kind === 'constructor'
        ? 'constructor'
        : getMemberRawName(node, sourceCode);
    case AST_NODE_TYPES.TSConstructSignatureDeclaration:
      return 'new';
    case AST_NODE_TYPES.TSCallSignatureDeclaration:
      return 'call';
    case AST_NODE_TYPES.TSIndexSignature:
      return getNameFromIndexSignature(node);
    case AST_NODE_TYPES.StaticBlock:
      return 'static block';
    default:
      return null;
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets the member name based on the member type.
 *
 * @param node the node to be evaluated.
 */
```

- **Parameters**:
  - `node: Member`
  - `sourceCode: TSESLint.SourceCode`
- **Return Type**: `string | null`
- **Calls**:
  - `getMemberRawName`
  - `getNameFromIndexSignature (from ../util)`
### `isMemberOptional(node: Member): boolean`

<details><summary>Code</summary>

```ts
function isMemberOptional(node: Member): boolean {
  switch (node.type) {
    case AST_NODE_TYPES.TSPropertySignature:
    case AST_NODE_TYPES.TSMethodSignature:
    case AST_NODE_TYPES.TSAbstractAccessorProperty:
    case AST_NODE_TYPES.TSAbstractPropertyDefinition:
    case AST_NODE_TYPES.AccessorProperty:
    case AST_NODE_TYPES.PropertyDefinition:
    case AST_NODE_TYPES.TSAbstractMethodDefinition:
    case AST_NODE_TYPES.MethodDefinition:
      return node.optional;
  }
  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns true if the member is optional based on the member type.
 *
 * @param node the node to be evaluated.
 *
 * @returns Whether the member is optional, or false if it cannot be optional at all.
 */
```

- **Parameters**:
  - `node: Member`
- **Return Type**: `boolean`
### `getRankOrder(memberGroups: BaseMemberType[], orderConfig: MemberType[]): number`

<details><summary>Code</summary>

```ts
function getRankOrder(
  memberGroups: BaseMemberType[],
  orderConfig: MemberType[],
): number {
  let rank = -1;
  const stack = [...memberGroups]; // Get a copy of the member groups

  while (stack.length > 0 && rank === -1) {
    // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
    const memberGroup = stack.shift()!;
    rank = orderConfig.findIndex(memberType =>
      Array.isArray(memberType)
        ? memberType.includes(memberGroup)
        : memberType === memberGroup,
    );
  }

  return rank;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets the calculated rank using the provided method definition.
 * The algorithm is as follows:
 * - Get the rank based on the accessibility-scope-type name, e.g. public-instance-field
 * - If there is no order for accessibility-scope-type, then strip out the accessibility.
 * - If there is no order for scope-type, then strip out the scope.
 * - If there is no order for type, then return -1
 * @param memberGroups the valid names to be validated.
 * @param orderConfig the current order to be validated.
 *
 * @return Index of the matching member type in the order configuration.
 */
```

- **Parameters**:
  - `memberGroups: BaseMemberType[]`
  - `orderConfig: MemberType[]`
- **Return Type**: `number`
- **Calls**:
  - `stack.shift`
  - `orderConfig.findIndex`
  - `Array.isArray`
  - `memberType.includes`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x2)
```

### `getAccessibility(node: Member): Accessibility`

<details><summary>Code</summary>

```ts
function getAccessibility(node: Member): Accessibility {
  if ('accessibility' in node && node.accessibility) {
    return node.accessibility;
  }
  if ('key' in node && node.key.type === AST_NODE_TYPES.PrivateIdentifier) {
    return '#private';
  }
  return 'public';
}
```
</details>

- **Parameters**:
  - `node: Member`
- **Return Type**: `Accessibility`
### `getRank(node: Member, orderConfig: MemberType[], supportsModifiers: boolean): number`

<details><summary>Code</summary>

```ts
function getRank(
  node: Member,
  orderConfig: MemberType[],
  supportsModifiers: boolean,
): number {
  const type = getNodeType(node);

  if (
    node.type === AST_NODE_TYPES.MethodDefinition &&
    node.value.type === AST_NODE_TYPES.TSEmptyBodyFunctionExpression
  ) {
    return -1;
  }

  if (type == null) {
    // shouldn't happen but just in case, put it on the end
    return orderConfig.length - 1;
  }

  const abstract =
    node.type === AST_NODE_TYPES.TSAbstractAccessorProperty ||
    node.type === AST_NODE_TYPES.TSAbstractPropertyDefinition ||
    node.type === AST_NODE_TYPES.TSAbstractMethodDefinition;

  const scope =
    'static' in node && node.static
      ? 'static'
      : abstract
        ? 'abstract'
        : 'instance';
  const accessibility = getAccessibility(node);

  // Collect all existing member groups that apply to this node...
  // (e.g. 'public-instance-field', 'instance-field', 'public-field', 'constructor' etc.)
  const memberGroups: BaseMemberType[] = [];

  if (supportsModifiers) {
    const decorated = 'decorators' in node && node.decorators.length > 0;
    if (
      decorated &&
      (type === 'readonly-field' ||
        type === 'field' ||
        type === 'method' ||
        type === 'accessor' ||
        type === 'get' ||
        type === 'set')
    ) {
      memberGroups.push(`${accessibility}-decorated-${type}`);
      memberGroups.push(`decorated-${type}`);

      if (type === 'readonly-field') {
        memberGroups.push(`${accessibility}-decorated-field`);
        memberGroups.push(`decorated-field`);
      }
    }

    if (
      type !== 'readonly-signature' &&
      type !== 'signature' &&
      type !== 'static-initialization'
    ) {
      if (type !== 'constructor') {
        // Constructors have no scope
        memberGroups.push(`${accessibility}-${scope}-${type}`);
        memberGroups.push(`${scope}-${type}`);

        if (type === 'readonly-field') {
          memberGroups.push(`${accessibility}-${scope}-field`);
          memberGroups.push(`${scope}-field`);
        }
      }

      memberGroups.push(`${accessibility}-${type}`);
      if (type === 'readonly-field') {
        memberGroups.push(`${accessibility}-field`);
      }
    }
  }

  memberGroups.push(type);
  if (type === 'readonly-signature') {
    memberGroups.push('signature');
  } else if (type === 'readonly-field') {
    memberGroups.push('field');
  }

  // ...then get the rank order for those member groups based on the node
  return getRankOrder(memberGroups, orderConfig);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets the rank of the node given the order.
 * @param node the node to be evaluated.
 * @param orderConfig the current order to be validated.
 * @param supportsModifiers a flag indicating whether the type supports modifiers (scope or accessibility) or not.
 */
```

- **Parameters**:
  - `node: Member`
  - `orderConfig: MemberType[]`
  - `supportsModifiers: boolean`
- **Return Type**: `number`
- **Calls**:
  - `getNodeType`
  - `getAccessibility`
  - `memberGroups.push`
  - `getRankOrder`
- **Internal Comments**:
```
// shouldn't happen but just in case, put it on the end
// Collect all existing member groups that apply to this node... (x2)
// (e.g. 'public-instance-field', 'instance-field', 'public-field', 'constructor' etc.) (x2)
// Constructors have no scope (x4)
// ...then get the rank order for those member groups based on the node
```

### `groupMembersByType(members: Member[], memberTypes: MemberType[], supportsModifiers: boolean): Member[][]`

<details><summary>Code</summary>

```ts
function groupMembersByType(
  members: Member[],
  memberTypes: MemberType[],
  supportsModifiers: boolean,
): Member[][] {
  const groupedMembers: Member[][] = [];
  const memberRanks = members.map(member =>
    getRank(member, memberTypes, supportsModifiers),
  );
  let previousRank: number | undefined = undefined;
  members.forEach((member, index) => {
    if (index === members.length - 1) {
      return;
    }
    const rankOfCurrentMember = memberRanks[index];
    const rankOfNextMember = memberRanks[index + 1];
    if (rankOfCurrentMember === previousRank) {
      groupedMembers.at(-1)?.push(member);
    } else if (rankOfCurrentMember === rankOfNextMember) {
      groupedMembers.push([member]);
      previousRank = rankOfCurrentMember;
    }
  });
  return groupedMembers;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Groups members into arrays of consecutive members with the same rank.
 * If, for example, the memberSet parameter looks like the following...
 * @example
 * ```
 * interface Foo {
 *   [a: string]: number;
 *
 *   a: x;
 *   B: x;
 *   c: x;
 *
 *   c(): void;
 *   B(): void;
 *   a(): void;
 *
 *   (): Baz;
 *
 *   new (): Bar;
 * }
 * ```
 * ...the resulting array will look like: [[a, B, c], [c, B, a]].
 * @param memberSet The members to be grouped.
 * @param memberType The configured order of member types.
 * @param supportsModifiers It'll get passed to getRank().
 * @returns The array of groups of members.
 */
```

- **Parameters**:
  - `members: Member[]`
  - `memberTypes: MemberType[]`
  - `supportsModifiers: boolean`
- **Return Type**: `Member[][]`
- **Calls**:
  - `members.map`
  - `getRank`
  - `members.forEach`
  - `groupedMembers.at(-1)?.push`
  - `groupedMembers.push`
### `getLowestRank(ranks: number[], target: number, order: MemberType[]): string`

<details><summary>Code</summary>

```ts
function getLowestRank(
  ranks: number[],
  target: number,
  order: MemberType[],
): string {
  let lowest = ranks[ranks.length - 1];

  ranks.forEach(rank => {
    if (rank > target) {
      lowest = Math.min(lowest, rank);
    }
  });

  const lowestRank = order[lowest];
  const lowestRanks = Array.isArray(lowestRank) ? lowestRank : [lowestRank];
  return lowestRanks.map(rank => rank.replaceAll('-', ' ')).join(', ');
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets the lowest possible rank(s) higher than target.
 * e.g. given the following order:
 *   ...
 *   public-static-method
 *   protected-static-method
 *   private-static-method
 *   public-instance-method
 *   protected-instance-method
 *   private-instance-method
 *   ...
 * and considering that a public-instance-method has already been declared, so ranks contains
 * public-instance-method, then the lowest possible rank for public-static-method is
 * public-instance-method.
 * If a lowest possible rank is a member group, a comma separated list of ranks is returned.
 * @param ranks the existing ranks in the object.
 * @param target the minimum target rank to filter on.
 * @param order the current order to be validated.
 * @returns the name(s) of the lowest possible rank without dashes (-).
 */
```

- **Parameters**:
  - `ranks: number[]`
  - `target: number`
  - `order: MemberType[]`
- **Return Type**: `string`
- **Calls**:
  - `ranks.forEach`
  - `Math.min`
  - `Array.isArray`
  - `lowestRanks.map(rank => rank.replaceAll('-', ' ')).join`
### `checkGroupSort(members: Member[], groupOrder: MemberType[], supportsModifiers: boolean): Member[][] | null`

<details><summary>Code</summary>

```ts
function checkGroupSort(
      members: Member[],
      groupOrder: MemberType[],
      supportsModifiers: boolean,
    ): Member[][] | null {
      const previousRanks: number[] = [];
      const memberGroups: Member[][] = [];
      let isCorrectlySorted = true;

      // Find first member which isn't correctly sorted
      for (const member of members) {
        const rank = getRank(member, groupOrder, supportsModifiers);
        const name = getMemberName(member, context.sourceCode);
        const rankLastMember = previousRanks[previousRanks.length - 1];

        if (rank === -1) {
          continue;
        }

        // Works for 1st item because x < undefined === false for any x (typeof string)
        if (rank < rankLastMember) {
          context.report({
            node: member,
            messageId: 'incorrectGroupOrder',
            data: {
              name,
              rank: getLowestRank(previousRanks, rank, groupOrder),
            },
          });

          isCorrectlySorted = false;
        } else if (rank === rankLastMember) {
          // Same member group --> Push to existing member group array
          memberGroups[memberGroups.length - 1].push(member);
        } else {
          // New member group --> Create new member group array
          previousRanks.push(rank);
          memberGroups.push([member]);
        }
      }

      return isCorrectlySorted ? memberGroups : null;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the member groups are correctly sorted.
     *
     * @param members Members to be validated.
     * @param groupOrder Group order to be validated.
     * @param supportsModifiers A flag indicating whether the type supports modifiers (scope or accessibility) or not.
     *
     * @return Array of member groups or null if one of the groups is not correctly sorted.
     */
```

- **Parameters**:
  - `members: Member[]`
  - `groupOrder: MemberType[]`
  - `supportsModifiers: boolean`
- **Return Type**: `Member[][] | null`
- **Calls**:
  - `getRank`
  - `getMemberName`
  - `context.report`
  - `getLowestRank`
  - `memberGroups[memberGroups.length - 1].push`
  - `previousRanks.push`
  - `memberGroups.push`
- **Internal Comments**:
```
// Find first member which isn't correctly sorted
// Works for 1st item because x < undefined === false for any x (typeof string)
// Same member group --> Push to existing member group array (x5)
// New member group --> Create new member group array (x4)
```

### `checkAlphaSort(members: Member[], order: AlphabeticalOrder): boolean`

<details><summary>Code</summary>

```ts
function checkAlphaSort(
      members: Member[],
      order: AlphabeticalOrder,
    ): boolean {
      let previousName = '';
      let isCorrectlySorted = true;

      // Find first member which isn't correctly sorted
      members.forEach(member => {
        const name = getMemberName(member, context.sourceCode);

        // Note: Not all members have names
        if (name) {
          if (naturalOutOfOrder(name, previousName, order)) {
            context.report({
              node: member,
              messageId: 'incorrectOrder',
              data: {
                beforeMember: previousName,
                member: name,
              },
            });

            isCorrectlySorted = false;
          }

          previousName = name;
        }
      });

      return isCorrectlySorted;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the members are alphabetically sorted.
     *
     * @param members Members to be validated.
     * @param order What order the members should be sorted in.
     *
     * @return True if all members are correctly sorted.
     */
```

- **Parameters**:
  - `members: Member[]`
  - `order: AlphabeticalOrder`
- **Return Type**: `boolean`
- **Calls**:
  - `members.forEach`
  - `getMemberName`
  - `naturalOutOfOrder`
  - `context.report`
- **Internal Comments**:
```
// Find first member which isn't correctly sorted (x4)
// Note: Not all members have names
```

### `naturalOutOfOrder(name: string, previousName: string, order: AlphabeticalOrder): boolean`

<details><summary>Code</summary>

```ts
function naturalOutOfOrder(
      name: string,
      previousName: string,
      order: AlphabeticalOrder,
    ): boolean {
      if (name === previousName) {
        return false;
      }

      switch (order) {
        case 'alphabetically':
          return name < previousName;
        case 'alphabetically-case-insensitive':
          return name.toLowerCase() < previousName.toLowerCase();
        case 'natural':
          return naturalCompare(name, previousName) !== 1;
        case 'natural-case-insensitive':
          return (
            naturalCompare(name.toLowerCase(), previousName.toLowerCase()) !== 1
          );
      }
    }
```
</details>

- **Parameters**:
  - `name: string`
  - `previousName: string`
  - `order: AlphabeticalOrder`
- **Return Type**: `boolean`
- **Calls**:
  - `name.toLowerCase`
  - `previousName.toLowerCase`
  - `naturalCompare (from natural-compare)`
### `checkRequiredOrder(members: Member[], optionalityOrder: OptionalityOrder | undefined): boolean`

<details><summary>Code</summary>

```ts
function checkRequiredOrder(
      members: Member[],
      optionalityOrder: OptionalityOrder | undefined,
    ): boolean {
      const switchIndex = members.findIndex(
        (member, i) =>
          i && isMemberOptional(member) !== isMemberOptional(members[i - 1]),
      );

      const report = (member: Member): void =>
        context.report({
          loc: member.loc,
          messageId: 'incorrectRequiredMembersOrder',
          data: {
            member: getMemberName(member, context.sourceCode),
            optionalOrRequired:
              optionalityOrder === 'required-first' ? 'required' : 'optional',
          },
        });

      // if the optionality of the first item is correct (based on optionalityOrder)
      // then the first 0 inclusive to switchIndex exclusive members all
      // have the correct optionality
      if (
        isMemberOptional(members[0]) !==
        (optionalityOrder === 'optional-first')
      ) {
        report(members[0]);
        return false;
      }

      for (let i = switchIndex + 1; i < members.length; i++) {
        if (
          isMemberOptional(members[i]) !==
          isMemberOptional(members[switchIndex])
        ) {
          report(members[switchIndex]);
          return false;
        }
      }

      return true;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the order of optional and required members is correct based
     * on the given 'required' parameter.
     *
     * @param members Members to be validated.
     * @param optionalityOrder Where to place optional members, if not intermixed.
     *
     * @return True if all required and optional members are correctly sorted.
     */
```

- **Parameters**:
  - `members: Member[]`
  - `optionalityOrder: OptionalityOrder | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `members.findIndex`
  - `isMemberOptional`
  - `context.report`
  - `getMemberName`
  - `report`
- **Internal Comments**:
```
// if the optionality of the first item is correct (based on optionalityOrder)
// then the first 0 inclusive to switchIndex exclusive members all
// have the correct optionality
```

### `report(member: Member): void`

<details><summary>Code</summary>

```ts
(member: Member): void =>
        context.report({
          loc: member.loc,
          messageId: 'incorrectRequiredMembersOrder',
          data: {
            member: getMemberName(member, context.sourceCode),
            optionalOrRequired:
              optionalityOrder === 'required-first' ? 'required' : 'optional',
          },
        })
```
</details>

- **Parameters**:
  - `member: Member`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
### `validateMembersOrder(members: Member[], orderConfig: OrderConfig, supportsModifiers: boolean): void`

<details><summary>Code</summary>

```ts
function validateMembersOrder(
      members: Member[],
      orderConfig: OrderConfig,
      supportsModifiers: boolean,
    ): void {
      if (orderConfig === 'never') {
        return;
      }

      // Standardize config
      let order: Order | undefined;
      let memberTypes: string | MemberType[] | undefined;
      let optionalityOrder: OptionalityOrder | undefined;

      /**
       * It runs an alphabetic sort on the groups of the members of the class in the source code.
       * @param memberSet The members in the class of the source code on which the grouping operation will be performed.
       */
      const checkAlphaSortForAllMembers = (memberSet: Member[]): undefined => {
        const hasAlphaSort = !!(order && order !== 'as-written');
        if (hasAlphaSort && Array.isArray(memberTypes)) {
          groupMembersByType(memberSet, memberTypes, supportsModifiers).forEach(
            members => {
              checkAlphaSort(members, order as AlphabeticalOrder);
            },
          );
        }
      };

      // returns true if everything is good and false if an error was reported
      const checkOrder = (memberSet: Member[]): boolean => {
        const hasAlphaSort = !!(order && order !== 'as-written');

        // Check order
        if (Array.isArray(memberTypes)) {
          const grouped = checkGroupSort(
            memberSet,
            memberTypes,
            supportsModifiers,
          );

          if (grouped == null) {
            checkAlphaSortForAllMembers(members);
            return false;
          }

          if (hasAlphaSort) {
            grouped.map(groupMember =>
              checkAlphaSort(groupMember, order as AlphabeticalOrder),
            );
          }
        } else if (hasAlphaSort) {
          return checkAlphaSort(memberSet, order as AlphabeticalOrder);
        }

        return false;
      };

      if (Array.isArray(orderConfig)) {
        memberTypes = orderConfig;
      } else {
        order = orderConfig.order;
        memberTypes = orderConfig.memberTypes;
        optionalityOrder = orderConfig.optionalityOrder;
      }

      if (!optionalityOrder) {
        checkOrder(members);
        return;
      }

      const switchIndex = members.findIndex(
        (member, i) =>
          i && isMemberOptional(member) !== isMemberOptional(members[i - 1]),
      );

      if (switchIndex !== -1) {
        if (!checkRequiredOrder(members, optionalityOrder)) {
          return;
        }
        checkOrder(members.slice(0, switchIndex));
        checkOrder(members.slice(switchIndex));
      } else {
        checkOrder(members);
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Validates if all members are correctly sorted.
     *
     * @param members Members to be validated.
     * @param orderConfig Order config to be validated.
     * @param supportsModifiers A flag indicating whether the type supports modifiers (scope or accessibility) or not.
     */
```

- **Parameters**:
  - `members: Member[]`
  - `orderConfig: OrderConfig`
  - `supportsModifiers: boolean`
- **Return Type**: `void`
- **Calls**:
  - `Array.isArray`
  - `groupMembersByType(memberSet, memberTypes, supportsModifiers).forEach`
  - `checkAlphaSort`
  - `checkGroupSort`
  - `checkAlphaSortForAllMembers`
  - `grouped.map`
  - `checkOrder`
  - `members.findIndex`
  - `isMemberOptional`
  - `checkRequiredOrder`
  - `members.slice`
- **Internal Comments**:
```
// Standardize config (x2)
/**
       * It runs an alphabetic sort on the groups of the members of the class in the source code.
       * @param memberSet The members in the class of the source code on which the grouping operation will be performed.
       */ (x2)
// returns true if everything is good and false if an error was reported (x2)
// Check order
```

### `checkAlphaSortForAllMembers(memberSet: Member[]): undefined`

<details><summary>Code</summary>

```ts
(memberSet: Member[]): undefined => {
        const hasAlphaSort = !!(order && order !== 'as-written');
        if (hasAlphaSort && Array.isArray(memberTypes)) {
          groupMembersByType(memberSet, memberTypes, supportsModifiers).forEach(
            members => {
              checkAlphaSort(members, order as AlphabeticalOrder);
            },
          );
        }
      }
```
</details>

- **Parameters**:
  - `memberSet: Member[]`
- **Return Type**: `undefined`
- **Calls**:
  - `Array.isArray`
  - `groupMembersByType(memberSet, memberTypes, supportsModifiers).forEach`
  - `checkAlphaSort`
### `checkOrder(memberSet: Member[]): boolean`

<details><summary>Code</summary>

```ts
(memberSet: Member[]): boolean => {
        const hasAlphaSort = !!(order && order !== 'as-written');

        // Check order
        if (Array.isArray(memberTypes)) {
          const grouped = checkGroupSort(
            memberSet,
            memberTypes,
            supportsModifiers,
          );

          if (grouped == null) {
            checkAlphaSortForAllMembers(members);
            return false;
          }

          if (hasAlphaSort) {
            grouped.map(groupMember =>
              checkAlphaSort(groupMember, order as AlphabeticalOrder),
            );
          }
        } else if (hasAlphaSort) {
          return checkAlphaSort(memberSet, order as AlphabeticalOrder);
        }

        return false;
      }
```
</details>

- **Parameters**:
  - `memberSet: Member[]`
- **Return Type**: `boolean`
- **Calls**:
  - `Array.isArray`
  - `checkGroupSort`
  - `checkAlphaSortForAllMembers`
  - `grouped.map`
  - `checkAlphaSort`
- **Internal Comments**:
```
// Check order
```


---

## Interfaces

### `SortedOrderConfig`

<details><summary>Interface Code</summary>

```ts
interface SortedOrderConfig {
  memberTypes?: 'never' | MemberType[];
  optionalityOrder?: OptionalityOrder;
  order?: Order;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `memberTypes` | `'never' | MemberType[]` | ✓ |  |
| `optionalityOrder` | `OptionalityOrder` | ✓ |  |
| `order` | `Order` | ✓ |  |


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = | 'incorrectGroupOrder'
  | 'incorrectOrder'
  | 'incorrectRequiredMembersOrder';
```

### `ReadonlyType`

```ts
type ReadonlyType = 'readonly-field' | 'readonly-signature';
```

### `MemberKind`

```ts
type MemberKind = | 'accessor'
  | 'call-signature'
  | 'constructor'
  | 'field'
  | 'get'
  | 'method'
  | 'set'
  | 'signature'
  | 'static-initialization'
  | ReadonlyType;
```

### `DecoratedMemberKind`

```ts
type DecoratedMemberKind = | 'accessor'
  | 'field'
  | 'get'
  | 'method'
  | 'set'
  | Exclude<ReadonlyType, 'readonly-signature'>;
```

### `NonCallableMemberKind`

```ts
type NonCallableMemberKind = Exclude<
  MemberKind,
  'constructor' | 'readonly-signature' | 'signature'
>;
```

### `MemberScope`

```ts
type MemberScope = 'abstract' | 'instance' | 'static';
```

### `Accessibility`

```ts
type Accessibility = '#private' | TSESTree.Accessibility;
```

### `BaseMemberType`

```ts
type BaseMemberType = | `${Accessibility}-${Exclude<
      MemberKind,
      'readonly-signature' | 'signature' | 'static-initialization'
    >}`
  | `${Accessibility}-${MemberScope}-${NonCallableMemberKind}`
  | `${Accessibility}-decorated-${DecoratedMemberKind}`
  | `${MemberScope}-${NonCallableMemberKind}`
  | `decorated-${DecoratedMemberKind}`
  | MemberKind;
```

### `MemberType`

```ts
type MemberType = BaseMemberType | BaseMemberType[];
```

### `AlphabeticalOrder`

```ts
type AlphabeticalOrder = | 'alphabetically'
  | 'alphabetically-case-insensitive'
  | 'natural'
  | 'natural-case-insensitive';
```

### `Order`

```ts
type Order = 'as-written' | AlphabeticalOrder;
```

### `OrderConfig`

```ts
type OrderConfig = 'never' | MemberType[] | SortedOrderConfig;
```

### `Member`

```ts
type Member = TSESTree.ClassElement | TSESTree.TypeElement;
```

### `OptionalityOrder`

```ts
type OptionalityOrder = 'optional-first' | 'required-first';
```

### `Options`

```ts
type Options = [
  {
    classes?: OrderConfig;
    classExpressions?: OrderConfig;
    default?: OrderConfig;
    interfaces?: OrderConfig;
    typeLiterals?: OrderConfig;
  },
];
```


---