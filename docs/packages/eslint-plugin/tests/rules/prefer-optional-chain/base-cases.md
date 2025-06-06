[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `base-cases.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 4 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/prefer-optional-chain/base-cases.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `@typescript-eslint/rule-tester` |
| `PreferOptionalChainMessageIds` | `../../../src/rules/prefer-optional-chain-utils/PreferOptionalChainOptions` |
| `PreferOptionalChainOptions` | `../../../src/rules/prefer-optional-chain-utils/PreferOptionalChainOptions` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `skipIdsSet` | `Set<number>` | const | `new Set(skipIds)` | ✗ |
| `skipSpecifiedIds` | `(
    arg: ReturnType<typeof RawBaseCases>[number],
  ) => boolean` | const | `skipIds.length === 0
      ? (): boolean => true
      : ({ id }): boolean => !skipIdsSet.has(id)` | ✗ |
| `code` | `string` | const | ``// ${id}\n${declaration}\n${mutateCode(chain)}`` | ✗ |
| `output` | `string` | const | ``// ${id}\n${declaration}\n${mutateOutput(outputChain)}`` | ✗ |


---

## Functions

### `RawBaseCases(operator: '&&' | '||'): readonly [{ readonly chain: "foo && foo.bar;" | "foo || foo.bar;"; readonly declaration: "declare const foo: {bar: number} | null | undefined;"; readonly id: 1; readonly outputChain: "foo?.bar;"; }, ... 24 more ..., { ...; }]`

<details><summary>Code</summary>

```ts
(operator: '&&' | '||') =>
  [
    // chained members
    {
      chain: `foo ${operator} foo.bar;`,
      declaration: 'declare const foo: {bar: number} | null | undefined;',
      id: 1,
      outputChain: 'foo?.bar;',
    },
    {
      chain: `foo.bar ${operator} foo.bar.baz;`,
      declaration:
        'declare const foo: {bar: {baz: number} | null | undefined};',
      id: 2,
      outputChain: 'foo.bar?.baz;',
    },
    {
      chain: `foo ${operator} foo();`,
      declaration: 'declare const foo: (() => number) | null | undefined;',
      id: 3,
      outputChain: 'foo?.();',
    },
    {
      chain: `foo.bar ${operator} foo.bar();`,
      declaration:
        'declare const foo: {bar: (() => number) | null | undefined};',
      id: 4,
      outputChain: 'foo.bar?.();',
    },
    {
      chain: `foo ${operator} foo.bar ${operator} foo.bar.baz ${operator} foo.bar.baz.buzz;`,
      declaration:
        'declare const foo: {bar: {baz: {buzz: number} | null | undefined} | null | undefined} | null | undefined;',
      id: 5,
      outputChain: 'foo?.bar?.baz?.buzz;',
    },
    {
      chain: `foo.bar ${operator} foo.bar.baz ${operator} foo.bar.baz.buzz;`,
      declaration:
        'declare const foo: {bar: {baz: {buzz: number} | null | undefined} | null | undefined};',
      id: 6,
      outputChain: 'foo.bar?.baz?.buzz;',
    },
    // case with a jump (i.e. a non-nullish prop)
    {
      chain: `foo ${operator} foo.bar ${operator} foo.bar.baz.buzz;`,
      declaration:
        'declare const foo: {bar: {baz: {buzz: number}} | null | undefined} | null | undefined;',
      id: 7,
      outputChain: 'foo?.bar?.baz.buzz;',
    },
    {
      chain: `foo.bar ${operator} foo.bar.baz.buzz;`,
      declaration:
        'declare const foo: {bar: {baz: {buzz: number}} | null | undefined};',
      id: 8,
      outputChain: 'foo.bar?.baz.buzz;',
    },
    // case where for some reason there is a doubled up expression
    {
      chain: `foo ${operator} foo.bar ${operator} foo.bar.baz ${operator} foo.bar.baz ${operator} foo.bar.baz.buzz;`,
      declaration:
        'declare const foo: {bar: {baz: {buzz: number} | null | undefined} | null | undefined} | null | undefined;',
      id: 9,
      outputChain: 'foo?.bar?.baz?.buzz;',
    },
    {
      chain: `foo.bar ${operator} foo.bar.baz ${operator} foo.bar.baz ${operator} foo.bar.baz.buzz;`,
      declaration:
        'declare const foo: {bar: {baz: {buzz: number} | null | undefined} | null | undefined} | null | undefined;',
      id: 10,
      outputChain: 'foo.bar?.baz?.buzz;',
    },
    // chained members with element access
    {
      chain: `foo ${operator} foo[bar] ${operator} foo[bar].baz ${operator} foo[bar].baz.buzz;`,
      declaration: [
        'declare const bar: string;',
        'declare const foo: {[k: string]: {baz: {buzz: number} | null | undefined} | null | undefined} | null | undefined;',
      ].join('\n'),
      id: 11,
      outputChain: 'foo?.[bar]?.baz?.buzz;',
    },
    {
      id: 12,
      // case with a jump (i.e. a non-nullish prop)
      chain: `foo ${operator} foo[bar].baz ${operator} foo[bar].baz.buzz;`,
      declaration: [
        'declare const bar: string;',
        'declare const foo: {[k: string]: {baz: {buzz: number} | null | undefined} | null | undefined} | null | undefined;',
      ].join('\n'),
      outputChain: 'foo?.[bar].baz?.buzz;',
    },
    // case with a property access in computed property
    {
      chain: `foo ${operator} foo[bar.baz] ${operator} foo[bar.baz].buzz;`,
      declaration: [
        'declare const bar: {baz: string};',
        'declare const foo: {[k: string]: {buzz: number} | null | undefined} | null | undefined;',
      ].join('\n'),
      id: 13,
      outputChain: 'foo?.[bar.baz]?.buzz;',
    },
    // chained calls
    {
      chain: `foo ${operator} foo.bar ${operator} foo.bar.baz ${operator} foo.bar.baz.buzz();`,
      declaration:
        'declare const foo: {bar: {baz: {buzz: () => number} | null | undefined} | null | undefined} | null | undefined;',
      id: 14,
      outputChain: 'foo?.bar?.baz?.buzz();',
    },
    {
      chain: `foo ${operator} foo.bar ${operator} foo.bar.baz ${operator} foo.bar.baz.buzz ${operator} foo.bar.baz.buzz();`,
      declaration:
        'declare const foo: {bar: {baz: {buzz: (() => number) | null | undefined} | null | undefined} | null | undefined} | null | undefined;',
      id: 15,
      outputChain: 'foo?.bar?.baz?.buzz?.();',
    },
    {
      chain: `foo.bar ${operator} foo.bar.baz ${operator} foo.bar.baz.buzz ${operator} foo.bar.baz.buzz();`,
      declaration:
        'declare const foo: {bar: {baz: {buzz: (() => number) | null | undefined} | null | undefined} | null | undefined};',
      id: 16,
      outputChain: 'foo.bar?.baz?.buzz?.();',
    },
    // case with a jump (i.e. a non-nullish prop)
    {
      chain: `foo ${operator} foo.bar ${operator} foo.bar.baz.buzz();`,
      declaration:
        'declare const foo: {bar: {baz: {buzz: () => number}} | null | undefined} | null | undefined;',
      id: 17,
      outputChain: 'foo?.bar?.baz.buzz();',
    },
    {
      chain: `foo.bar ${operator} foo.bar.baz.buzz();`,
      declaration:
        'declare const foo: {bar: {baz: {buzz: () => number}} | null | undefined};',
      id: 18,
      outputChain: 'foo.bar?.baz.buzz();',
    },
    {
      id: 19,
      // case with a jump (i.e. a non-nullish prop)
      chain: `foo ${operator} foo.bar ${operator} foo.bar.baz.buzz ${operator} foo.bar.baz.buzz();`,
      declaration:
        'declare const foo: {bar: {baz: {buzz: (() => number) | null | undefined}} | null | undefined} | null | undefined;',
      outputChain: 'foo?.bar?.baz.buzz?.();',
    },
    {
      id: 20,
      // case with a call expr inside the chain for some inefficient reason
      chain: `foo.bar ${operator} foo.bar() ${operator} foo.bar().baz ${operator} foo.bar().baz.buzz ${operator} foo.bar().baz.buzz();`,
      declaration:
        'declare const foo: {bar: () => ({baz: {buzz: (() => number) | null | undefined} | null | undefined}) | null | undefined};',
      outputChain: 'foo.bar?.()?.baz?.buzz?.();',
    },
    // chained calls with element access
    {
      chain: `foo ${operator} foo.bar ${operator} foo.bar.baz ${operator} foo.bar.baz[buzz]();`,
      declaration: [
        'declare const buzz: string;',
        'declare const foo: {bar: {baz: {[k: string]: () => number} | null | undefined} | null | undefined} | null | undefined;',
      ].join('\n'),
      id: 21,
      outputChain: 'foo?.bar?.baz?.[buzz]();',
    },
    {
      chain: `foo ${operator} foo.bar ${operator} foo.bar.baz ${operator} foo.bar.baz[buzz] ${operator} foo.bar.baz[buzz]();`,
      declaration: [
        'declare const buzz: string;',
        'declare const foo: {bar: {baz: {[k: string]: (() => number) | null | undefined} | null | undefined} | null | undefined} | null | undefined;',
      ].join('\n'),
      id: 22,
      outputChain: 'foo?.bar?.baz?.[buzz]?.();',
    },
    // (partially) pre-optional chained
    {
      chain: `foo ${operator} foo?.bar ${operator} foo?.bar.baz ${operator} foo?.bar.baz[buzz] ${operator} foo?.bar.baz[buzz]();`,
      declaration: [
        'declare const buzz: string;',
        'declare const foo: {bar: {baz: {[k: string]: (() => number) | null | undefined} | null | undefined} | null | undefined} | null | undefined;',
      ].join('\n'),
      id: 23,
      outputChain: 'foo?.bar?.baz?.[buzz]?.();',
    },
    {
      chain: `foo ${operator} foo?.bar.baz ${operator} foo?.bar.baz[buzz];`,
      declaration: [
        'declare const buzz: string;',
        'declare const foo: {bar: {baz: {[k: string]: number} | null | undefined}} | null | undefined;',
      ].join('\n'),
      id: 24,
      outputChain: 'foo?.bar.baz?.[buzz];',
    },
    {
      chain: `foo ${operator} foo?.() ${operator} foo?.().bar;`,
      declaration:
        'declare const foo: (() => ({bar: number} | null | undefined)) | null | undefined;',
      id: 25,
      outputChain: 'foo?.()?.bar;',
    },
    {
      chain: `foo.bar ${operator} foo.bar?.() ${operator} foo.bar?.().baz;`,
      declaration:
        'declare const foo: {bar: () => ({baz: number} | null | undefined)};',
      id: 26,
      outputChain: 'foo.bar?.()?.baz;',
    },
  ] as const
```
</details>

- **Parameters**:
  - `operator: '&&' | '||'`
- **Return Type**: `readonly [{ readonly chain: "foo && foo.bar;" | "foo || foo.bar;"; readonly declaration: "declare const foo: {bar: number} | null | undefined;"; readonly id: 1; readonly outputChain: "foo?.bar;"; }, ... 24 more ..., { ...; }]`
### `identity(c: string): string`

<details><summary>Code</summary>

```ts
c => c
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
### `BaseCases({
  mutateCode = identity,
  mutateDeclaration = identity,
  mutateOutput = mutateCode,
  operator,
  skipIds = [],
  useSuggestionFixer = false,
}: any): InvalidTestCase<PreferOptionalChainMessageIds, [PreferOptionalChainOptions]>[]`

<details><summary>Code</summary>

```ts
({
  mutateCode = identity,
  mutateDeclaration = identity,
  mutateOutput = mutateCode,
  operator,
  skipIds = [],
  useSuggestionFixer = false,
}) => {
  const skipIdsSet = new Set(skipIds);
  const skipSpecifiedIds: (
    arg: ReturnType<typeof RawBaseCases>[number],
  ) => boolean =
    skipIds.length === 0
      ? (): boolean => true
      : ({ id }): boolean => !skipIdsSet.has(id);

  return RawBaseCases(operator)
    .filter(skipSpecifiedIds)
    .map(
      ({
        chain,
        declaration: originalDeclaration,
        id,
        outputChain,
      }): InvalidTestCase<
        PreferOptionalChainMessageIds,
        [PreferOptionalChainOptions]
      > => {
        const declaration = mutateDeclaration(originalDeclaration);
        const code = `// ${id}\n${declaration}\n${mutateCode(chain)}`;
        const output = `// ${id}\n${declaration}\n${mutateOutput(outputChain)}`;

        return {
          code,
          errors: [
            {
              messageId: 'preferOptionalChain',
              suggestions: !useSuggestionFixer
                ? null
                : [
                    {
                      messageId: 'optionalChainSuggest',
                      output,
                    },
                  ],
            },
          ],
          output: useSuggestionFixer ? null : output,
        };
      },
    );
}
```
</details>

- **Parameters**:
  - `{
  mutateCode = identity,
  mutateDeclaration = identity,
  mutateOutput = mutateCode,
  operator,
  skipIds = [],
  useSuggestionFixer = false,
}: any`
- **Return Type**: `InvalidTestCase<PreferOptionalChainMessageIds, [PreferOptionalChainOptions]>[]`
- **Calls**:
  - `skipIdsSet.has`
  - `RawBaseCases(operator)
    .filter(skipSpecifiedIds)
    .map`
  - `mutateDeclaration`
  - `mutateCode`
  - `mutateOutput`

---

## Type Aliases

### `MutateFn`

```ts
type MutateFn = (c: string) => string;
```

### `BaseCaseCreator`

```ts
type BaseCaseCreator = (args: {
  mutateCode?: MutateFn;
  mutateDeclaration?: MutateFn;
  mutateOutput?: MutateFn;
  operator: '&&' | '||';
  skipIds?: number[];
  useSuggestionFixer?: true;
}) => InvalidTestCase<
  PreferOptionalChainMessageIds,
  [PreferOptionalChainOptions]
>[];
```


---