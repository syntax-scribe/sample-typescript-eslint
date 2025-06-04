[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `checkNullishAndReport.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 8 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-optional-chain-utils/checkNullishAndReport.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserServicesWithTypeInformation` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `ReportDescriptor` | `@typescript-eslint/utils/ts-eslint` |
| `RuleContext` | `@typescript-eslint/utils/ts-eslint` |
| `isTypeFlagSet` | `@typescript-eslint/type-utils` |
| `unionConstituents` | `ts-api-utils` |
| `PreferOptionalChainMessageIds` | `./PreferOptionalChainOptions` |
| `PreferOptionalChainOptions` | `./PreferOptionalChainOptions` |


---

## Functions

### `checkNullishAndReport(context: RuleContext<
    PreferOptionalChainMessageIds,
    [PreferOptionalChainOptions]
  >, parserServices: ParserServicesWithTypeInformation, { requireNullish }: PreferOptionalChainOptions, maybeNullishNodes: TSESTree.Expression[], descriptor: ReportDescriptor<PreferOptionalChainMessageIds>): void`

<details><summary>Code</summary>

```ts
export function checkNullishAndReport(
  context: RuleContext<
    PreferOptionalChainMessageIds,
    [PreferOptionalChainOptions]
  >,
  parserServices: ParserServicesWithTypeInformation,
  { requireNullish }: PreferOptionalChainOptions,
  maybeNullishNodes: TSESTree.Expression[],
  descriptor: ReportDescriptor<PreferOptionalChainMessageIds>,
): void {
  if (
    !requireNullish ||
    maybeNullishNodes.some(node =>
      unionConstituents(parserServices.getTypeAtLocation(node)).some(t =>
        isTypeFlagSet(t, ts.TypeFlags.Null | ts.TypeFlags.Undefined),
      ),
    )
  ) {
    context.report(descriptor);
  }
}
```
</details>

- **Parameters**:
  - `context: RuleContext<
    PreferOptionalChainMessageIds,
    [PreferOptionalChainOptions]
  >`
  - `parserServices: ParserServicesWithTypeInformation`
  - `{ requireNullish }: PreferOptionalChainOptions`
  - `maybeNullishNodes: TSESTree.Expression[]`
  - `descriptor: ReportDescriptor<PreferOptionalChainMessageIds>`
- **Return Type**: `void`
- **Calls**:
  - `maybeNullishNodes.some`
  - `unionConstituents(parserServices.getTypeAtLocation(node)).some`
  - `isTypeFlagSet (from @typescript-eslint/type-utils)`
  - `context.report`

---