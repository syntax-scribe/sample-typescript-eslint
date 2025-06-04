[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getFixOrSuggest.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

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