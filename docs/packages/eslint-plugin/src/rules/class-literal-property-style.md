[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `class-literal-property-style.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 5 |
| 📦 Imports | 9 |
| 📊 Variables & Constants | 5 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/class-literal-property-style.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getStaticMemberAccessValue` | `../util` |
| `isAssignee` | `../util` |
| `isFunction` | `../util` |
| `isStaticMemberAccessOfValue` | `../util` |
| `nullThrows` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `propertiesInfoStack` | `PropertiesInfo[]` | const | `[]` | ✗ |
| `text` | `string` | let/var | `''` | ✗ |
| `hasDuplicateKeySetter` | `any` | const | `name &&
            node.parent.body.some(element => {
              return (
                element.type === AST_NODE_TYPES.MethodDefinition &&
                element.kind === 'set' &&
                isStaticMemberAccessOfValue(element, context, name)
              );
            })` | ✗ |
| `text` | `string` | let/var | `''` | ✗ |
| `parent` | `TSESTree.Node | undefined` | let/var | `node.parent` | ✗ |


---

## Functions

### `printNodeModifiers(node: NodeWithModifiers, final: 'get' | 'readonly'): string`

<details><summary>Code</summary>

```ts
(
  node: NodeWithModifiers,
  final: 'get' | 'readonly',
): string =>
  `${node.accessibility ?? ''}${
    node.static ? ' static' : ''
  } ${final} `.trimStart()
```
</details>

- **Parameters**:
  - `node: NodeWithModifiers`
  - `final: 'get' | 'readonly'`
- **Return Type**: `string`
- **Calls**:
  - ``${node.accessibility ?? ''}${
    node.static ? ' static' : ''
  } ${final} `.trimStart`
### `isSupportedLiteral(node: TSESTree.Node): node is TSESTree.LiteralExpression`

<details><summary>Code</summary>

```ts
(
  node: TSESTree.Node,
): node is TSESTree.LiteralExpression => {
  switch (node.type) {
    case AST_NODE_TYPES.Literal:
      return true;

    case AST_NODE_TYPES.TaggedTemplateExpression:
      return node.quasi.quasis.length === 1;

    case AST_NODE_TYPES.TemplateLiteral:
      return node.quasis.length === 1;

    default:
      return false;
  }
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.LiteralExpression`
### `enterClassBody(): void`

<details><summary>Code</summary>

```ts
function enterClassBody(): void {
      propertiesInfoStack.push({
        excludeSet: new Set(),
        properties: [],
      });
    }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `propertiesInfoStack.push`
### `exitClassBody(): void`

<details><summary>Code</summary>

```ts
function exitClassBody(): void {
      const { excludeSet, properties } = nullThrows(
        propertiesInfoStack.pop(),
        'Stack should exist on class exit',
      );

      properties.forEach(node => {
        const { value } = node;
        if (!value || !isSupportedLiteral(value)) {
          return;
        }

        const name = getStaticMemberAccessValue(node, context);
        if (name && excludeSet.has(name)) {
          return;
        }

        context.report({
          node: node.key,
          messageId: 'preferGetterStyle',
          suggest: [
            {
              messageId: 'preferGetterStyleSuggestion',
              fix(fixer): TSESLint.RuleFix {
                const name = context.sourceCode.getText(node.key);

                let text = '';
                text += printNodeModifiers(node, 'get');
                text += node.computed ? `[${name}]` : name;
                text += `() { return ${context.sourceCode.getText(value)}; }`;

                return fixer.replaceText(node, text);
              },
            },
          ],
        });
      });
    }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `nullThrows (from ../util)`
  - `propertiesInfoStack.pop`
  - `properties.forEach`
  - `isSupportedLiteral`
  - `getStaticMemberAccessValue (from ../util)`
  - `excludeSet.has`
  - `context.report`
  - `context.sourceCode.getText`
  - `printNodeModifiers`
  - `fixer.replaceText`
### `excludeAssignedProperty(node: TSESTree.MemberExpression): void`

<details><summary>Code</summary>

```ts
function excludeAssignedProperty(node: TSESTree.MemberExpression): void {
      if (isAssignee(node)) {
        const { excludeSet } =
          propertiesInfoStack[propertiesInfoStack.length - 1];

        const name = getStaticMemberAccessValue(node, context);

        if (name) {
          excludeSet.add(name);
        }
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.MemberExpression`
- **Return Type**: `void`
- **Calls**:
  - `isAssignee (from ../util)`
  - `getStaticMemberAccessValue (from ../util)`
  - `excludeSet.add`

---

## Interfaces

### `NodeWithModifiers`

<details><summary>Interface Code</summary>

```ts
interface NodeWithModifiers {
  accessibility?: TSESTree.Accessibility;
  static: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `accessibility` | `TSESTree.Accessibility` | ✓ |  |
| `static` | `boolean` | ✗ |  |

### `PropertiesInfo`

<details><summary>Interface Code</summary>

```ts
interface PropertiesInfo {
  excludeSet: Set<string | symbol>;
  properties: TSESTree.PropertyDefinition[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `excludeSet` | `Set<string | symbol>` | ✗ |  |
| `properties` | `TSESTree.PropertyDefinition[]` | ✗ |  |


---

## Type Aliases

### `Options`

```ts
type Options = ['fields' | 'getters'];
```

### `MessageIds`

```ts
type MessageIds = | 'preferFieldStyle'
  | 'preferFieldStyleSuggestion'
  | 'preferGetterStyle'
  | 'preferGetterStyleSuggestion';
```


---