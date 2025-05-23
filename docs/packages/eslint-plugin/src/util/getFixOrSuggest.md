[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getFixOrSuggest.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getFixOrSuggest.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |


---

## Functions

### `getFixOrSuggest({
  fixOrSuggest,
  suggestion,
}: {
  fixOrSuggest: 'fix' | 'none' | 'suggest';
  suggestion: TSESLint.SuggestionReportDescriptor<MessageId>;
}): | { fix: TSESLint.ReportFixFunction }
  | { suggest: TSESLint.SuggestionReportDescriptor<MessageId>[] }
  | undefined`

<details><summary>Code</summary>

```ts
export function getFixOrSuggest<MessageId extends string>({
  fixOrSuggest,
  suggestion,
}: {
  fixOrSuggest: 'fix' | 'none' | 'suggest';
  suggestion: TSESLint.SuggestionReportDescriptor<MessageId>;
}):
  | { fix: TSESLint.ReportFixFunction }
  | { suggest: TSESLint.SuggestionReportDescriptor<MessageId>[] }
  | undefined {
  switch (fixOrSuggest) {
    case 'fix':
      return { fix: suggestion.fix };
    case 'none':
      return undefined;
    case 'suggest':
      return { suggest: [suggestion] };
  }
}
```
</details>

- **Parameters**:
  - `{
  fixOrSuggest,
  suggestion,
}: {
  fixOrSuggest: 'fix' | 'none' | 'suggest';
  suggestion: TSESLint.SuggestionReportDescriptor<MessageId>;
}`
- **Return Type**: `| { fix: TSESLint.ReportFixFunction }
  | { suggest: TSESLint.SuggestionReportDescriptor<MessageId>[] }
  | undefined`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---