[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `parameter-properties.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 1
- **Type Aliases**: 4

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

## Classes

> No classes found in this file.


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