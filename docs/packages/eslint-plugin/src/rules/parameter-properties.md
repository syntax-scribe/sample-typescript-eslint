[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `parameter-properties.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 5 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 4 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/parameter-properties.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `nullThrows` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `modifiers` | `Modifier[]` | const | `[]` | ✗ |
| `name` | `any` | const | `node.parameter.type === AST_NODE_TYPES.Identifier
                ? node.parameter.name
                : // has to be an Identifier or TSC will throw an error
                  (node.parameter.left as TSESTree.Identifier).name` | ✗ |
| `propertyNodesByNameStack` | `Map<string, PropertyNodes>[]` | const | `[]` | ✗ |
| `propertyNodesByName` | `Map<string, PropertyNodes>` | const | `propertyNodesByNameStack[propertyNodesByNameStack.length - 1]` | ✗ |
| `created` | `PropertyNodes` | const | `{}` | ✗ |


---

## Functions

### `getModifiers(node: TSESTree.PropertyDefinition | TSESTree.TSParameterProperty): Modifier`

<details><summary>Code</summary>

```ts
function getModifiers(
      node: TSESTree.PropertyDefinition | TSESTree.TSParameterProperty,
    ): Modifier {
      const modifiers: Modifier[] = [];

      if (node.accessibility) {
        modifiers.push(node.accessibility);
      }
      if (node.readonly) {
        modifiers.push('readonly');
      }

      return modifiers.filter(Boolean).join(' ') as Modifier;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Gets the modifiers of `node`.
     * @param node the node to be inspected.
     */
```

- **Parameters**:
  - `node: TSESTree.PropertyDefinition | TSESTree.TSParameterProperty`
- **Return Type**: `Modifier`
- **Calls**:
  - `modifiers.push`
  - `modifiers.filter(Boolean).join`
### `getNodesByName(name: string): PropertyNodes`

<details><summary>Code</summary>

```ts
function getNodesByName(name: string): PropertyNodes {
      const propertyNodesByName =
        propertyNodesByNameStack[propertyNodesByNameStack.length - 1];
      const existing = propertyNodesByName.get(name);
      if (existing) {
        return existing;
      }

      const created: PropertyNodes = {};
      propertyNodesByName.set(name, created);
      return created;
    }
```
</details>

- **Parameters**:
  - `name: string`
- **Return Type**: `PropertyNodes`
- **Calls**:
  - `propertyNodesByName.get`
  - `propertyNodesByName.set`
### `typeAnnotationsMatch(classProperty: TSESTree.PropertyDefinition, constructorParameter: TSESTree.Identifier): boolean`

<details><summary>Code</summary>

```ts
function typeAnnotationsMatch(
      classProperty: TSESTree.PropertyDefinition,
      constructorParameter: TSESTree.Identifier,
    ): boolean {
      if (
        !classProperty.typeAnnotation ||
        !constructorParameter.typeAnnotation
      ) {
        return (
          classProperty.typeAnnotation === constructorParameter.typeAnnotation
        );
      }

      return (
        context.sourceCode.getText(classProperty.typeAnnotation) ===
        context.sourceCode.getText(constructorParameter.typeAnnotation)
      );
    }
```
</details>

- **Parameters**:
  - `classProperty: TSESTree.PropertyDefinition`
  - `constructorParameter: TSESTree.Identifier`
- **Return Type**: `boolean`
- **Calls**:
  - `context.sourceCode.getText`

---

## Interfaces

### `PropertyNodes`

<details><summary>Interface Code</summary>

```ts
interface PropertyNodes {
      classProperty?: TSESTree.PropertyDefinition;
      constructorAssignment?: TSESTree.AssignmentExpression;
      constructorParameter?: TSESTree.Identifier;
    }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `classProperty` | `TSESTree.PropertyDefinition` | ✓ |  |
| `constructorAssignment` | `TSESTree.AssignmentExpression` | ✓ |  |
| `constructorParameter` | `TSESTree.Identifier` | ✓ |  |


---

## Type Aliases

### `Modifier`

```ts
type Modifier = | 'private'
  | 'private readonly'
  | 'protected'
  | 'protected readonly'
  | 'public'
  | 'public readonly'
  | 'readonly';
```

### `Prefer`

```ts
type Prefer = 'class-property' | 'parameter-property';
```

### `Options`

```ts
type Options = [
  {
    allow?: Modifier[];
    prefer?: Prefer;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'preferClassProperty' | 'preferParameterProperty';
```


---