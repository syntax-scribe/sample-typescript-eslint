[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `misc.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 15
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 0
- **Type Aliases**: 4

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/misc.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleContext` | `@typescript-eslint/utils/ts-eslint` |
| `requiresQuoting` | `@typescript-eslint/type-utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `getStaticValue` | `./astUtils` |
| `isParenthesized` | `./astUtils` |


---

## Functions

### `isDefinitionFile(fileName: string): boolean`

<details><summary>Code</summary>

```ts
export function isDefinitionFile(fileName: string): boolean {
  const lowerFileName = fileName.toLowerCase();
  for (const definitionExt of DEFINITION_EXTENSIONS) {
    if (lowerFileName.endsWith(definitionExt)) {
      return true;
    }
  }

  return /\.d\.(ts|cts|mts|.*\.ts)$/.test(lowerFileName);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if the context file name is *.d.ts or *.d.tsx
 */
```

- **Parameters**:
  - `fileName: string`
- **Return Type**: `boolean`
- **Calls**:
  - `fileName.toLowerCase`
  - `lowerFileName.endsWith`
  - `/\.d\.(ts|cts|mts|.*\.ts)$/.test`
### `upperCaseFirst(str: string): string`

<details><summary>Code</summary>

```ts
export function upperCaseFirst(str: string): string {
  return str[0].toUpperCase() + str.slice(1);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Upper cases the first character or the string
 */
```

- **Parameters**:
  - `str: string`
- **Return Type**: `string`
- **Calls**:
  - `str[0].toUpperCase`
  - `str.slice`
### `arrayGroupByToMap(array: T[], getKey: (item: T) => Key): Map<Key, T[]>`

<details><summary>Code</summary>

```ts
export function arrayGroupByToMap<T, Key extends number | string>(
  array: T[],
  getKey: (item: T) => Key,
): Map<Key, T[]> {
  const groups = new Map<Key, T[]>();

  for (const item of array) {
    const key = getKey(item);
    const existing = groups.get(key);

    if (existing) {
      existing.push(item);
    } else {
      groups.set(key, [item]);
    }
  }

  return groups;
}
```
</details>

- **Parameters**:
  - `array: T[]`
  - `getKey: (item: T) => Key`
- **Return Type**: `Map<Key, T[]>`
- **Calls**:
  - `getKey`
  - `groups.get`
  - `existing.push`
  - `groups.set`
### `arraysAreEqual(a: T[] | undefined, b: T[] | undefined, eq: (a: T, b: T) => boolean): boolean`

<details><summary>Code</summary>

```ts
export function arraysAreEqual<T>(
  a: T[] | undefined,
  b: T[] | undefined,
  eq: (a: T, b: T) => boolean,
): boolean {
  return (
    a === b ||
    (a != null &&
      b != null &&
      a.length === b.length &&
      a.every((x, idx) => eq(x, b[idx])))
  );
}
```
</details>

- **Parameters**:
  - `a: T[] | undefined`
  - `b: T[] | undefined`
  - `eq: (a: T, b: T) => boolean`
- **Return Type**: `boolean`
- **Calls**:
  - `a.every`
  - `eq`
### `findFirstResult(inputs: T[], getResult: (t: T) => U | undefined): U | undefined`

<details><summary>Code</summary>

```ts
export function findFirstResult<T, U>(
  inputs: T[],
  getResult: (t: T) => U | undefined,
): U | undefined {
  for (const element of inputs) {
    const result = getResult(element);
    // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
    if (result !== undefined) {
      return result;
    }
  }
  return undefined;
}
```
</details>

- **JSDoc**:
```ts
/** Returns the first non-`undefined` result. */
```

- **Parameters**:
  - `inputs: T[]`
  - `getResult: (t: T) => U | undefined`
- **Return Type**: `U | undefined`
- **Calls**:
  - `getResult`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
```

### `getNameFromIndexSignature(node: TSESTree.TSIndexSignature): string`

<details><summary>Code</summary>

```ts
export function getNameFromIndexSignature(
  node: TSESTree.TSIndexSignature,
): string {
  const propName: TSESTree.PropertyName | undefined = node.parameters.find(
    (parameter: TSESTree.Parameter): parameter is TSESTree.Identifier =>
      parameter.type === AST_NODE_TYPES.Identifier,
  );
  return propName ? propName.name : '(index signature)';
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets a string representation of the name of the index signature.
 */
```

- **Parameters**:
  - `node: TSESTree.TSIndexSignature`
- **Return Type**: `string`
- **Calls**:
  - `node.parameters.find`
### `getNameFromMember(member: | TSESTree.AccessorProperty
    | TSESTree.MethodDefinition
    | TSESTree.Property
    | TSESTree.PropertyDefinition
    | TSESTree.TSAbstractAccessorProperty
    | TSESTree.TSAbstractMethodDefinition
    | TSESTree.TSAbstractPropertyDefinition
    | TSESTree.TSMethodSignature
    | TSESTree.TSPropertySignature, sourceCode: TSESLint.SourceCode): { name: string; type: MemberNameType }`

<details><summary>Code</summary>

```ts
export function getNameFromMember(
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
): { name: string; type: MemberNameType } {
  if (member.key.type === AST_NODE_TYPES.Identifier) {
    return {
      name: member.key.name,
      type: MemberNameType.Normal,
    };
  }
  if (member.key.type === AST_NODE_TYPES.PrivateIdentifier) {
    return {
      name: `#${member.key.name}`,
      type: MemberNameType.Private,
    };
  }
  if (member.key.type === AST_NODE_TYPES.Literal) {
    const name = `${member.key.value}`;
    if (requiresQuoting(name)) {
      return {
        name: `"${name}"`,
        type: MemberNameType.Quoted,
      };
    }
    return {
      name,
      type: MemberNameType.Normal,
    };
  }

  return {
    name: sourceCode.text.slice(...member.key.range),
    type: MemberNameType.Expression,
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets a string name representation of the name of the given MethodDefinition
 * or PropertyDefinition node, with handling for computed property names.
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
- **Return Type**: `{ name: string; type: MemberNameType }`
- **Calls**:
  - `requiresQuoting (from @typescript-eslint/type-utils)`
  - `sourceCode.text.slice`
### `getEnumNames(myEnum: Record<T, unknown>): T[]`

<details><summary>Code</summary>

```ts
export function getEnumNames<T extends string>(
  myEnum: Record<T, unknown>,
): T[] {
  return Object.keys(myEnum).filter(x => isNaN(Number(x))) as T[];
}
```
</details>

- **Parameters**:
  - `myEnum: Record<T, unknown>`
- **Return Type**: `T[]`
- **Calls**:
  - `Object.keys(myEnum).filter`
  - `isNaN`
  - `Number`
### `formatWordList(words: string[]): string`

<details><summary>Code</summary>

```ts
export function formatWordList(words: string[]): string {
  if (!words.length) {
    return '';
  }

  if (words.length === 1) {
    return words[0];
  }

  return [words.slice(0, -1).join(', '), words.slice(-1)[0]].join(' and ');
}
```
</details>

- **JSDoc**:
```ts
/**
 * Given an array of words, returns an English-friendly concatenation, separated with commas, with
 * the `and` clause inserted before the last item.
 *
 * Example: ['foo', 'bar', 'baz' ] returns the string "foo, bar, and baz".
 */
```

- **Parameters**:
  - `words: string[]`
- **Return Type**: `string`
- **Calls**:
  - `[words.slice(0, -1).join(', '), words.slice(-1)[0]].join`
  - `words.slice(0, -1).join`
  - `words.slice`
### `findLastIndex(members: T[], predicate: (member: T) => boolean | null | undefined): number`

<details><summary>Code</summary>

```ts
export function findLastIndex<T>(
  members: T[],
  predicate: (member: T) => boolean | null | undefined,
): number {
  let idx = members.length - 1;

  while (idx >= 0) {
    const valid = predicate(members[idx]);
    if (valid) {
      return idx;
    }
    idx--;
  }

  return -1;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Iterates the array in reverse and returns the index of the first element it
 * finds which passes the predicate function.
 *
 * @returns Returns the index of the element if it finds it or -1 otherwise.
 */
```

- **Parameters**:
  - `members: T[]`
  - `predicate: (member: T) => boolean | null | undefined`
- **Return Type**: `number`
- **Calls**:
  - `predicate`
### `typeNodeRequiresParentheses(node: TSESTree.TypeNode, text: string): boolean`

<details><summary>Code</summary>

```ts
export function typeNodeRequiresParentheses(
  node: TSESTree.TypeNode,
  text: string,
): boolean {
  return (
    node.type === AST_NODE_TYPES.TSFunctionType ||
    node.type === AST_NODE_TYPES.TSConstructorType ||
    node.type === AST_NODE_TYPES.TSConditionalType ||
    (node.type === AST_NODE_TYPES.TSUnionType && text.startsWith('|')) ||
    (node.type === AST_NODE_TYPES.TSIntersectionType && text.startsWith('&'))
  );
}
```
</details>

- **Parameters**:
  - `node: TSESTree.TypeNode`
  - `text: string`
- **Return Type**: `boolean`
- **Calls**:
  - `text.startsWith`
### `isRestParameterDeclaration(decl: ts.Declaration): boolean`

<details><summary>Code</summary>

```ts
export function isRestParameterDeclaration(decl: ts.Declaration): boolean {
  return ts.isParameter(decl) && decl.dotDotDotToken != null;
}
```
</details>

- **Parameters**:
  - `decl: ts.Declaration`
- **Return Type**: `boolean`
- **Calls**:
  - `ts.isParameter`
### `isParenlessArrowFunction(node: TSESTree.ArrowFunctionExpression, sourceCode: TSESLint.SourceCode): boolean`

<details><summary>Code</summary>

```ts
export function isParenlessArrowFunction(
  node: TSESTree.ArrowFunctionExpression,
  sourceCode: TSESLint.SourceCode,
): boolean {
  return (
    node.params.length === 1 && !isParenthesized(node.params[0], sourceCode)
  );
}
```
</details>

- **Parameters**:
  - `node: TSESTree.ArrowFunctionExpression`
  - `sourceCode: TSESLint.SourceCode`
- **Return Type**: `boolean`
- **Calls**:
  - `isParenthesized (from ./astUtils)`
### `getStaticMemberAccessValue(node: NodeWithKey, { sourceCode }: RuleContext<string, unknown[]>): string | symbol | undefined`

<details><summary>Code</summary>

```ts
export function getStaticMemberAccessValue(
  node: NodeWithKey,
  { sourceCode }: RuleContext<string, unknown[]>,
): string | symbol | undefined {
  const key =
    node.type === AST_NODE_TYPES.MemberExpression ? node.property : node.key;
  const { type } = key;
  if (
    !node.computed &&
    (type === AST_NODE_TYPES.Identifier ||
      type === AST_NODE_TYPES.PrivateIdentifier)
  ) {
    return key.name;
  }
  const result = getStaticValue(key, sourceCode.getScope(node));
  if (!result) {
    return undefined;
  }
  const { value } = result;
  return typeof value === 'symbol' ? value : String(value);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets a member being accessed or declared if its value can be determined statically, and
 * resolves it to the string or symbol value that will be used as the actual member
 * access key at runtime. Otherwise, returns `undefined`.
 *
 * ```ts
 * x.member // returns 'member'
 * ^^^^^^^^
 *
 * x?.member // returns 'member' (optional chaining is treated the same)
 * ^^^^^^^^^
 *
 * x['value'] // returns 'value'
 * ^^^^^^^^^^
 *
 * x[Math.random()] // returns undefined (not a static value)
 * ^^^^^^^^^^^^^^^^
 *
 * arr[0] // returns '0' (NOT 0)
 * ^^^^^^
 *
 * arr[0n] // returns '0' (NOT 0n)
 * ^^^^^^^
 *
 * const s = Symbol.for('symbolName')
 * x[s] // returns `Symbol.for('symbolName')` (since it's a static/global symbol)
 * ^^^^
 *
 * const us = Symbol('symbolName')
 * x[us] // returns undefined (since it's a unique symbol, so not statically analyzable)
 * ^^^^^
 *
 * var object = {
 *     1234: '4567', // returns '1234' (NOT 1234)
 *     ^^^^^^^^^^^^
 *     method() { } // returns 'method'
 *     ^^^^^^^^^^^^
 * }
 *
 * class WithMembers {
 *     foo: string // returns 'foo'
 *     ^^^^^^^^^^^
 * }
 * ```
 */
```

- **Parameters**:
  - `node: NodeWithKey`
  - `{ sourceCode }: RuleContext<string, unknown[]>`
- **Return Type**: `string | symbol | undefined`
- **Calls**:
  - `getStaticValue (from ./astUtils)`
  - `sourceCode.getScope`
  - `String`
### `isStaticMemberAccessOfValue(memberExpression: NodeWithKey, context: RuleContext<string, unknown[]>, values: (string | symbol)[]): boolean`

<details><summary>Code</summary>

```ts
(
  memberExpression: NodeWithKey,
  context: RuleContext<string, unknown[]>,
  ...values: (string | symbol)[]
): boolean =>
  (values as (string | symbol | undefined)[]).includes(
    getStaticMemberAccessValue(memberExpression, context),
  )
```
</details>

- **Parameters**:
  - `memberExpression: NodeWithKey`
  - `context: RuleContext<string, unknown[]>`
  - `values: (string | symbol)[]`
- **Return Type**: `boolean`
- **Calls**:
  - `(values as (string | symbol | undefined)[]).includes`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `Equal<T>`

/** Return true if both parameters are equal. */

```ts
type Equal<T> = (a: T, b: T) => boolean;
```

### `ExcludeKeys<Obj extends Record<string, unknown> extends Record<string, unknown>, Keys extends keyof Obj extends keyof Obj>`

```ts
type ExcludeKeys<Obj extends Record<string, unknown> extends Record<string, unknown>, Keys extends keyof Obj extends keyof Obj> = { [k in Exclude<keyof Obj, Keys>]: Obj[k] };
```

### `RequireKeys<Obj extends Record<string, unknown> extends Record<string, unknown>, Keys extends keyof Obj extends keyof Obj>`

```ts
type RequireKeys<Obj extends Record<string, unknown> extends Record<string, unknown>, Keys extends keyof Obj extends keyof Obj> = { [k in Keys]-?: Exclude<Obj[k], undefined> } & ExcludeKeys<Obj, Keys>;
```

### `NodeWithKey`

```ts
type NodeWithKey = | TSESTree.AccessorProperty
  | TSESTree.MemberExpression
  | TSESTree.MethodDefinition
  | TSESTree.Property
  | TSESTree.PropertyDefinition
  | TSESTree.TSAbstractMethodDefinition
  | TSESTree.TSAbstractPropertyDefinition;
```


---