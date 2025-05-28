[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getESLintCoreRule.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getESLintCoreRule.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintUtils` | `@typescript-eslint/utils` |
| `builtinRules` | `eslint/use-at-your-own-risk` |


---

## Functions

### `getESLintCoreRule(ruleId: R): RuleMap[R]`

<details><summary>Code</summary>

```ts
<R extends RuleId>(ruleId: R): RuleMap[R] =>
  ESLintUtils.nullThrows(
    builtinRules.get(ruleId),
    `ESLint's core rule '${ruleId}' not found.`,
  )
```
</details>

- **Parameters**:
  - `ruleId: R`
- **Return Type**: `RuleMap[R]`
- **Calls**:
  - `ESLintUtils.nullThrows`
### `maybeGetESLintCoreRule(ruleId: R): RuleMap[R] | null`

<details><summary>Code</summary>

```ts
export function maybeGetESLintCoreRule<R extends RuleId>(
  ruleId: R,
): RuleMap[R] | null {
  try {
    return getESLintCoreRule<R>(ruleId);
  } catch {
    return null;
  }
}
```
</details>

- **Parameters**:
  - `ruleId: R`
- **Return Type**: `RuleMap[R] | null`
- **Calls**:
  - `getESLintCoreRule`

---

## Interfaces

### `RuleMap`

<details><summary>Interface Code</summary>

```ts
interface RuleMap {
  /* eslint-disable @typescript-eslint/consistent-type-imports -- more concise to use inline imports */
  'arrow-parens': typeof import('eslint/lib/rules/arrow-parens');
  'consistent-return': typeof import('eslint/lib/rules/consistent-return');
  'dot-notation': typeof import('eslint/lib/rules/dot-notation');
  'init-declarations': typeof import('eslint/lib/rules/init-declarations');
  'max-params': typeof import('eslint/lib/rules/max-params');
  'no-dupe-args': typeof import('eslint/lib/rules/no-dupe-args');
  'no-dupe-class-members': typeof import('eslint/lib/rules/no-dupe-class-members');
  'no-empty-function': typeof import('eslint/lib/rules/no-empty-function');
  'no-implicit-globals': typeof import('eslint/lib/rules/no-implicit-globals');
  'no-invalid-this': typeof import('eslint/lib/rules/no-invalid-this');
  'no-loop-func': typeof import('eslint/lib/rules/no-loop-func');
  'no-loss-of-precision': typeof import('eslint/lib/rules/no-loss-of-precision');
  'no-magic-numbers': typeof import('eslint/lib/rules/no-magic-numbers');
  'no-restricted-globals': typeof import('eslint/lib/rules/no-restricted-globals');
  'no-restricted-imports': typeof import('eslint/lib/rules/no-restricted-imports');
  'no-undef': typeof import('eslint/lib/rules/no-undef');
  'no-unused-expressions': typeof import('eslint/lib/rules/no-unused-expressions');
  'no-useless-constructor': typeof import('eslint/lib/rules/no-useless-constructor');
  'prefer-const': typeof import('eslint/lib/rules/prefer-const');
  'prefer-destructuring': typeof import('eslint/lib/rules/prefer-destructuring');
  strict: typeof import('eslint/lib/rules/strict');
  /* eslint-enable @typescript-eslint/consistent-type-imports */
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `'arrow-parens'` | `typeof import('eslint/lib/rules/arrow-parens')` | ✗ |  |
| `'consistent-return'` | `typeof import('eslint/lib/rules/consistent-return')` | ✗ |  |
| `'dot-notation'` | `typeof import('eslint/lib/rules/dot-notation')` | ✗ |  |
| `'init-declarations'` | `typeof import('eslint/lib/rules/init-declarations')` | ✗ |  |
| `'max-params'` | `typeof import('eslint/lib/rules/max-params')` | ✗ |  |
| `'no-dupe-args'` | `typeof import('eslint/lib/rules/no-dupe-args')` | ✗ |  |
| `'no-dupe-class-members'` | `typeof import('eslint/lib/rules/no-dupe-class-members')` | ✗ |  |
| `'no-empty-function'` | `typeof import('eslint/lib/rules/no-empty-function')` | ✗ |  |
| `'no-implicit-globals'` | `typeof import('eslint/lib/rules/no-implicit-globals')` | ✗ |  |
| `'no-invalid-this'` | `typeof import('eslint/lib/rules/no-invalid-this')` | ✗ |  |
| `'no-loop-func'` | `typeof import('eslint/lib/rules/no-loop-func')` | ✗ |  |
| `'no-loss-of-precision'` | `typeof import('eslint/lib/rules/no-loss-of-precision')` | ✗ |  |
| `'no-magic-numbers'` | `typeof import('eslint/lib/rules/no-magic-numbers')` | ✗ |  |
| `'no-restricted-globals'` | `typeof import('eslint/lib/rules/no-restricted-globals')` | ✗ |  |
| `'no-restricted-imports'` | `typeof import('eslint/lib/rules/no-restricted-imports')` | ✗ |  |
| `'no-undef'` | `typeof import('eslint/lib/rules/no-undef')` | ✗ |  |
| `'no-unused-expressions'` | `typeof import('eslint/lib/rules/no-unused-expressions')` | ✗ |  |
| `'no-useless-constructor'` | `typeof import('eslint/lib/rules/no-useless-constructor')` | ✗ |  |
| `'prefer-const'` | `typeof import('eslint/lib/rules/prefer-const')` | ✗ |  |
| `'prefer-destructuring'` | `typeof import('eslint/lib/rules/prefer-destructuring')` | ✗ |  |
| `strict` | `typeof import('eslint/lib/rules/strict')` | ✗ |  |


---

## Type Aliases

### `RuleId`

```ts
type RuleId = keyof RuleMap;
```


---