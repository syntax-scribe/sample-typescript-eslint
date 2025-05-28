[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `explicit-member-accessibility.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 30 |
| 🧱 Classes | 0 |
| 📦 Imports | 11 |
| 📊 Variables & Constants | 17 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 3 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/explicit-member-accessibility.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getNameFromMember` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |
| `getMemberHeadLoc` | `../util/getMemberHeadLoc` |
| `getParameterPropertyHeadLoc` | `../util/getMemberHeadLoc` |
| `rangeToLoc` | `../util/rangeToLoc` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `baseCheck` | `AccessibilityLevel` | const | `option.accessibility ?? 'explicit'` | ✗ |
| `overrides` | `any` | const | `option.overrides ?? {}` | ✗ |
| `ctorCheck` | `any` | const | `overrides.constructors ?? baseCheck` | ✗ |
| `accessorCheck` | `any` | const | `overrides.accessors ?? baseCheck` | ✗ |
| `methodCheck` | `any` | const | `overrides.methods ?? baseCheck` | ✗ |
| `propCheck` | `any` | const | `overrides.properties ?? baseCheck` | ✗ |
| `paramPropCheck` | `any` | const | `overrides.parameterProperties ?? baseCheck` | ✗ |
| `ignoredMethodNames` | `Set<unknown>` | const | `new Set(option.ignoredMethodNames ?? [])` | ✗ |
| `nodeType` | `string` | let/var | `'method definition'` | ✗ |
| `check` | `AccessibilityLevel` | let/var | `baseCheck` | ✗ |
| `rangeToRemove` | `TSESLint.AST.Range` | let/var | `*not shown*` | ✗ |
| `keywordRange` | `TSESLint.AST.Range` | let/var | `*not shown*` | ✗ |
| `token` | `any` | const | `tokens[i]` | ✗ |
| `lastDecorator` | `any` | const | `node.decorators[node.decorators.length - 1]` | ✗ |
| `nodeType` | `"class property"` | const | `'class property'` | ✗ |
| `nodeType` | `"parameter property"` | const | `'parameter property'` | ✗ |
| `nodeName` | `any` | const | `node.parameter.type === AST_NODE_TYPES.Identifier
          ? node.parameter.name
          : // has to be an Identifier or TSC will throw an error
            (node.parameter.left as TSESTree.Identifier).name` | ✗ |


---

## Functions

### `checkMethodAccessibilityModifier(methodDefinition: | TSESTree.MethodDefinition
        | TSESTree.TSAbstractMethodDefinition): void`

<details><summary>Code</summary>

```ts
function checkMethodAccessibilityModifier(
      methodDefinition:
        | TSESTree.MethodDefinition
        | TSESTree.TSAbstractMethodDefinition,
    ): void {
      if (methodDefinition.key.type === AST_NODE_TYPES.PrivateIdentifier) {
        return;
      }

      let nodeType = 'method definition';
      let check = baseCheck;
      switch (methodDefinition.kind) {
        case 'method':
          check = methodCheck;
          break;
        case 'constructor':
          check = ctorCheck;
          break;
        case 'get':
        case 'set':
          check = accessorCheck;
          nodeType = `${methodDefinition.kind} property accessor`;
          break;
      }

      const { name: methodName } = getNameFromMember(
        methodDefinition,
        context.sourceCode,
      );

      if (check === 'off' || ignoredMethodNames.has(methodName)) {
        return;
      }

      if (
        check === 'no-public' &&
        methodDefinition.accessibility === 'public'
      ) {
        const publicKeyword = findPublicKeyword(methodDefinition);
        context.report({
          loc: rangeToLoc(context.sourceCode, publicKeyword.range),
          messageId: 'unwantedPublicAccessibility',
          data: {
            name: methodName,
            type: nodeType,
          },
          fix: fixer => fixer.removeRange(publicKeyword.rangeToRemove),
        });
      } else if (check === 'explicit' && !methodDefinition.accessibility) {
        context.report({
          loc: getMemberHeadLoc(context.sourceCode, methodDefinition),
          messageId: 'missingAccessibility',
          data: {
            name: methodName,
            type: nodeType,
          },
          suggest: getMissingAccessibilitySuggestions(methodDefinition),
        });
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if a method declaration has an accessibility modifier.
     * @param methodDefinition The node representing a MethodDefinition.
     */
```

- **Parameters**:
  - `methodDefinition: | TSESTree.MethodDefinition
        | TSESTree.TSAbstractMethodDefinition`
- **Return Type**: `void`
- **Calls**:
  - `getNameFromMember (from ../util)`
  - `ignoredMethodNames.has`
  - `findPublicKeyword`
  - `context.report`
  - `rangeToLoc (from ../util/rangeToLoc)`
  - `fixer.removeRange`
  - `getMemberHeadLoc (from ../util/getMemberHeadLoc)`
  - `getMissingAccessibilitySuggestions`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.removeRange(publicKeyword.rangeToRemove)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.removeRange(publicKeyword.rangeToRemove)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `findPublicKeyword(node: | TSESTree.AccessorProperty
        | TSESTree.MethodDefinition
        | TSESTree.PropertyDefinition
        | TSESTree.TSAbstractAccessorProperty
        | TSESTree.TSAbstractMethodDefinition
        | TSESTree.TSAbstractPropertyDefinition
        | TSESTree.TSParameterProperty): { range: TSESLint.AST.Range; rangeToRemove: TSESLint.AST.Range }`

<details><summary>Code</summary>

```ts
function findPublicKeyword(
      node:
        | TSESTree.AccessorProperty
        | TSESTree.MethodDefinition
        | TSESTree.PropertyDefinition
        | TSESTree.TSAbstractAccessorProperty
        | TSESTree.TSAbstractMethodDefinition
        | TSESTree.TSAbstractPropertyDefinition
        | TSESTree.TSParameterProperty,
    ): { range: TSESLint.AST.Range; rangeToRemove: TSESLint.AST.Range } {
      const tokens = context.sourceCode.getTokens(node);
      let rangeToRemove!: TSESLint.AST.Range;
      let keywordRange!: TSESLint.AST.Range;
      for (let i = 0; i < tokens.length; i++) {
        const token = tokens[i];
        if (
          token.type === AST_TOKEN_TYPES.Keyword &&
          token.value === 'public'
        ) {
          keywordRange = structuredClone(token.range);
          const commensAfterPublicKeyword =
            context.sourceCode.getCommentsAfter(token);
          if (commensAfterPublicKeyword.length) {
            // public /* Hi there! */ static foo()
            // ^^^^^^^
            rangeToRemove = [
              token.range[0],
              commensAfterPublicKeyword[0].range[0],
            ];
            break;
          } else {
            // public static foo()
            // ^^^^^^^
            rangeToRemove = [token.range[0], tokens[i + 1].range[0]];
            break;
          }
        }
      }
      return { range: keywordRange, rangeToRemove };
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Returns an object containing a range that corresponds to the "public"
     * keyword for a node, and the range that would need to be removed to
     * remove the "public" keyword (including associated whitespace).
     */
```

- **Parameters**:
  - `node: | TSESTree.AccessorProperty
        | TSESTree.MethodDefinition
        | TSESTree.PropertyDefinition
        | TSESTree.TSAbstractAccessorProperty
        | TSESTree.TSAbstractMethodDefinition
        | TSESTree.TSAbstractPropertyDefinition
        | TSESTree.TSParameterProperty`
- **Return Type**: `{ range: TSESLint.AST.Range; rangeToRemove: TSESLint.AST.Range }`
- **Calls**:
  - `context.sourceCode.getTokens`
  - `structuredClone`
  - `context.sourceCode.getCommentsAfter`
- **Internal Comments**:
```
// public /* Hi there! */ static foo() (x3)
// ^^^^^^^ (x6)
// public static foo() (x3)
```

### `getMissingAccessibilitySuggestions(node: | TSESTree.AccessorProperty
        | TSESTree.MethodDefinition
        | TSESTree.PropertyDefinition
        | TSESTree.TSAbstractAccessorProperty
        | TSESTree.TSAbstractMethodDefinition
        | TSESTree.TSAbstractPropertyDefinition
        | TSESTree.TSParameterProperty): TSESLint.ReportSuggestionArray<MessageIds>`

<details><summary>Code</summary>

```ts
function getMissingAccessibilitySuggestions(
      node:
        | TSESTree.AccessorProperty
        | TSESTree.MethodDefinition
        | TSESTree.PropertyDefinition
        | TSESTree.TSAbstractAccessorProperty
        | TSESTree.TSAbstractMethodDefinition
        | TSESTree.TSAbstractPropertyDefinition
        | TSESTree.TSParameterProperty,
    ): TSESLint.ReportSuggestionArray<MessageIds> {
      function fix(
        accessibility: TSESTree.Accessibility,
        fixer: TSESLint.RuleFixer,
      ): TSESLint.RuleFix | null {
        if (node.decorators.length) {
          const lastDecorator = node.decorators[node.decorators.length - 1];
          const nextToken = nullThrows(
            context.sourceCode.getTokenAfter(lastDecorator),
            NullThrowsReasons.MissingToken('token', 'last decorator'),
          );
          return fixer.insertTextBefore(nextToken, `${accessibility} `);
        }
        return fixer.insertTextBefore(node, `${accessibility} `);
      }

      return [
        {
          messageId: 'addExplicitAccessibility',
          data: { type: 'public' },
          fix: fixer => fix('public', fixer),
        },
        {
          messageId: 'addExplicitAccessibility',
          data: { type: 'private' },
          fix: fixer => fix('private', fixer),
        },
        {
          messageId: 'addExplicitAccessibility',
          data: { type: 'protected' },
          fix: fixer => fix('protected', fixer),
        },
      ];
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Creates a fixer that adds an accessibility modifier keyword
     */
```

- **Parameters**:
  - `node: | TSESTree.AccessorProperty
        | TSESTree.MethodDefinition
        | TSESTree.PropertyDefinition
        | TSESTree.TSAbstractAccessorProperty
        | TSESTree.TSAbstractMethodDefinition
        | TSESTree.TSAbstractPropertyDefinition
        | TSESTree.TSParameterProperty`
- **Return Type**: `TSESLint.ReportSuggestionArray<MessageIds>`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenAfter`
  - `NullThrowsReasons.MissingToken`
  - `fixer.insertTextBefore`
  - `fix`
### `fix(accessibility: TSESTree.Accessibility, fixer: TSESLint.RuleFixer): TSESLint.RuleFix | null`

<details><summary>Code</summary>

```ts
function fix(
        accessibility: TSESTree.Accessibility,
        fixer: TSESLint.RuleFixer,
      ): TSESLint.RuleFix | null {
        if (node.decorators.length) {
          const lastDecorator = node.decorators[node.decorators.length - 1];
          const nextToken = nullThrows(
            context.sourceCode.getTokenAfter(lastDecorator),
            NullThrowsReasons.MissingToken('token', 'last decorator'),
          );
          return fixer.insertTextBefore(nextToken, `${accessibility} `);
        }
        return fixer.insertTextBefore(node, `${accessibility} `);
      }
```
</details>

- **Parameters**:
  - `accessibility: TSESTree.Accessibility`
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix | null`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenAfter`
  - `NullThrowsReasons.MissingToken`
  - `fixer.insertTextBefore`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fix('public', fixer)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fix`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fix('public', fixer)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fix`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fix('private', fixer)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fix`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fix('private', fixer)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fix`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fix('protected', fixer)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fix`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fix('protected', fixer)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fix`
### `checkPropertyAccessibilityModifier(propertyDefinition: | TSESTree.AccessorProperty
        | TSESTree.PropertyDefinition
        | TSESTree.TSAbstractAccessorProperty
        | TSESTree.TSAbstractPropertyDefinition): void`

<details><summary>Code</summary>

```ts
function checkPropertyAccessibilityModifier(
      propertyDefinition:
        | TSESTree.AccessorProperty
        | TSESTree.PropertyDefinition
        | TSESTree.TSAbstractAccessorProperty
        | TSESTree.TSAbstractPropertyDefinition,
    ): void {
      if (propertyDefinition.key.type === AST_NODE_TYPES.PrivateIdentifier) {
        return;
      }

      const nodeType = 'class property';

      const { name: propertyName } = getNameFromMember(
        propertyDefinition,
        context.sourceCode,
      );
      if (
        propCheck === 'no-public' &&
        propertyDefinition.accessibility === 'public'
      ) {
        const publicKeywordRange = findPublicKeyword(propertyDefinition);
        context.report({
          loc: rangeToLoc(context.sourceCode, publicKeywordRange.range),
          messageId: 'unwantedPublicAccessibility',
          data: {
            name: propertyName,
            type: nodeType,
          },
          fix: fixer => fixer.removeRange(publicKeywordRange.rangeToRemove),
        });
      } else if (
        propCheck === 'explicit' &&
        !propertyDefinition.accessibility
      ) {
        context.report({
          loc: getMemberHeadLoc(context.sourceCode, propertyDefinition),
          messageId: 'missingAccessibility',
          data: {
            name: propertyName,
            type: nodeType,
          },
          suggest: getMissingAccessibilitySuggestions(propertyDefinition),
        });
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if property has an accessibility modifier.
     * @param propertyDefinition The node representing a PropertyDefinition.
     */
```

- **Parameters**:
  - `propertyDefinition: | TSESTree.AccessorProperty
        | TSESTree.PropertyDefinition
        | TSESTree.TSAbstractAccessorProperty
        | TSESTree.TSAbstractPropertyDefinition`
- **Return Type**: `void`
- **Calls**:
  - `getNameFromMember (from ../util)`
  - `findPublicKeyword`
  - `context.report`
  - `rangeToLoc (from ../util/rangeToLoc)`
  - `fixer.removeRange`
  - `getMemberHeadLoc (from ../util/getMemberHeadLoc)`
  - `getMissingAccessibilitySuggestions`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.removeRange(publicKeywordRange.rangeToRemove)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.removeRange(publicKeywordRange.rangeToRemove)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `checkParameterPropertyAccessibilityModifier(node: TSESTree.TSParameterProperty): void`

<details><summary>Code</summary>

```ts
function checkParameterPropertyAccessibilityModifier(
      node: TSESTree.TSParameterProperty,
    ): void {
      const nodeType = 'parameter property';
      // HAS to be an identifier or assignment or TSC will throw
      if (
        node.parameter.type !== AST_NODE_TYPES.Identifier &&
        node.parameter.type !== AST_NODE_TYPES.AssignmentPattern
      ) {
        return;
      }

      const nodeName =
        node.parameter.type === AST_NODE_TYPES.Identifier
          ? node.parameter.name
          : // has to be an Identifier or TSC will throw an error
            (node.parameter.left as TSESTree.Identifier).name;

      switch (paramPropCheck) {
        case 'explicit': {
          if (!node.accessibility) {
            context.report({
              loc: getParameterPropertyHeadLoc(
                context.sourceCode,
                node,
                nodeName,
              ),
              messageId: 'missingAccessibility',
              data: {
                name: nodeName,
                type: nodeType,
              },
              suggest: getMissingAccessibilitySuggestions(node),
            });
          }
          break;
        }
        case 'no-public': {
          if (node.accessibility === 'public' && node.readonly) {
            const publicKeyword = findPublicKeyword(node);
            context.report({
              loc: rangeToLoc(context.sourceCode, publicKeyword.range),
              messageId: 'unwantedPublicAccessibility',
              data: {
                name: nodeName,
                type: nodeType,
              },
              fix: fixer => fixer.removeRange(publicKeyword.rangeToRemove),
            });
          }
          break;
        }
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks that the parameter property has the desired accessibility modifiers set.
     * @param node The node representing a Parameter Property
     */
```

- **Parameters**:
  - `node: TSESTree.TSParameterProperty`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `getParameterPropertyHeadLoc (from ../util/getMemberHeadLoc)`
  - `getMissingAccessibilitySuggestions`
  - `findPublicKeyword`
  - `rangeToLoc (from ../util/rangeToLoc)`
  - `fixer.removeRange`
- **Internal Comments**:
```
// HAS to be an identifier or assignment or TSC will throw
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.removeRange(publicKeyword.rangeToRemove)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.removeRange(publicKeyword.rangeToRemove)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.removeRange(publicKeyword.rangeToRemove)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.removeRange(publicKeyword.rangeToRemove)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fix('public', fixer)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fix`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fix('public', fixer)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fix`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fix('private', fixer)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fix`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fix('private', fixer)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fix`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fix('protected', fixer)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fix`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fix('protected', fixer)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fix`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.removeRange(publicKeywordRange.rangeToRemove)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.removeRange(publicKeywordRange.rangeToRemove)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.removeRange(publicKeyword.rangeToRemove)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.removeRange(publicKeyword.rangeToRemove)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`

---

## Interfaces

### `Config`

<details><summary>Interface Code</summary>

```ts
export interface Config {
  accessibility?: AccessibilityLevel;
  ignoredMethodNames?: string[];
  overrides?: {
    accessors?: AccessibilityLevel;
    constructors?: AccessibilityLevel;
    methods?: AccessibilityLevel;
    parameterProperties?: AccessibilityLevel;
    properties?: AccessibilityLevel;
  };
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `accessibility` | `AccessibilityLevel` | ✓ |  |
| `ignoredMethodNames` | `string[]` | ✓ |  |
| `overrides` | `{
    accessors?: AccessibilityLevel;
    constructors?: AccessibilityLevel;
    methods?: AccessibilityLevel;
    parameterProperties?: AccessibilityLevel;
    properties?: AccessibilityLevel;
  }` | ✓ |  |


---

## Type Aliases

### `AccessibilityLevel`

```ts
type AccessibilityLevel = | 'explicit' // require an accessor (including public)
  | 'no-public' // don't require public
  | 'off';
```

### `Options`

```ts
type Options = [Config];
```

### `MessageIds`

```ts
type MessageIds = | 'addExplicitAccessibility'
  | 'missingAccessibility'
  | 'unwantedPublicAccessibility';
```


---