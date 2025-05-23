[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-enum-initializers.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 25
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-enum-initializers.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Functions

### `TSEnumDeclaration(node: TSESTree.TSEnumDeclaration): void`

<details><summary>Code</summary>

```ts
function TSEnumDeclaration(node: TSESTree.TSEnumDeclaration): void {
      const { members } = node.body;

      members.forEach((member, index) => {
        if (member.initializer == null) {
          const name = context.sourceCode.getText(member);
          context.report({
            node: member,
            messageId: 'defineInitializer',
            data: {
              name,
            },
            suggest: [
              {
                messageId: 'defineInitializerSuggestion',
                data: { name, suggested: index },
                fix: (fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index}`);
                },
              },
              {
                messageId: 'defineInitializerSuggestion',
                data: { name, suggested: index + 1 },
                fix: (fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index + 1}`);
                },
              },
              {
                messageId: 'defineInitializerSuggestion',
                data: { name, suggested: `'${name}'` },
                fix: (fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = '${name}'`);
                },
              },
            ],
          });
        }
      });
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `members.forEach`
  - `context.sourceCode.getText`
  - `context.report`
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index + 1}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index + 1}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = '${name}'`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = '${name}'`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index + 1}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index + 1}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = '${name}'`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = '${name}'`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index + 1}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index + 1}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = '${name}'`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = '${name}'`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index + 1}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = ${index + 1}`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = '${name}'`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer): TSESLint.RuleFix => {
                  return fixer.replaceText(member, `${name} = '${name}'`);
                }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.replaceText`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = 'defineInitializer' | 'defineInitializerSuggestion';
```


---