[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `semantic-or-syntactic-errors.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/semantic-or-syntactic-errors.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Diagnostic` | `typescript` |
| `DiagnosticWithLocation` | `typescript` |
| `Program` | `typescript` |
| `SourceFile` | `typescript` |
| `flattenDiagnosticMessageText` | `typescript` |
| `sys` | `typescript` |


---

## Functions

### `getFirstSemanticOrSyntacticError(program: Program, ast: SourceFile): SemanticOrSyntacticError | undefined`

<details><summary>Code</summary>

```ts
export function getFirstSemanticOrSyntacticError(
  program: Program,
  ast: SourceFile,
): SemanticOrSyntacticError | undefined {
  try {
    const supportedSyntacticDiagnostics = allowlistSupportedDiagnostics(
      program.getSyntacticDiagnostics(ast),
    );
    if (supportedSyntacticDiagnostics.length > 0) {
      return convertDiagnosticToSemanticOrSyntacticError(
        supportedSyntacticDiagnostics[0],
      );
    }
    const supportedSemanticDiagnostics = allowlistSupportedDiagnostics(
      program.getSemanticDiagnostics(ast),
    );
    if (supportedSemanticDiagnostics.length > 0) {
      return convertDiagnosticToSemanticOrSyntacticError(
        supportedSemanticDiagnostics[0],
      );
    }
    return undefined;
  } catch (e) {
    /**
     * TypeScript compiler has certain Debug.fail() statements in, which will cause the diagnostics
     * retrieval above to throw.
     *
     * E.g. from ast-alignment-tests
     * "Debug Failure. Shouldn't ever directly check a JsxOpeningElement"
     *
     * For our current use-cases this is undesired behavior, so we just suppress it
     * and log a warning.
     */
    /* istanbul ignore next */
    console.warn(`Warning From TSC: "${(e as Error).message}`); // eslint-disable-line no-console
    /* istanbul ignore next */
    return undefined;
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * By default, diagnostics from the TypeScript compiler contain all errors - regardless of whether
 * they are related to generic ECMAScript standards, or TypeScript-specific constructs.
 *
 * Therefore, we filter out all diagnostics, except for the ones we explicitly want to consider when
 * the user opts in to throwing errors on semantic issues.
 */
```

- **Parameters**:
  - `program: Program`
  - `ast: SourceFile`
- **Return Type**: `SemanticOrSyntacticError | undefined`
- **Calls**:
  - `allowlistSupportedDiagnostics`
  - `program.getSyntacticDiagnostics`
  - `convertDiagnosticToSemanticOrSyntacticError`
  - `program.getSemanticDiagnostics`
  - `console.warn`
- **Internal Comments**:
```
/**
     * TypeScript compiler has certain Debug.fail() statements in, which will cause the diagnostics
     * retrieval above to throw.
     *
     * E.g. from ast-alignment-tests
     * "Debug Failure. Shouldn't ever directly check a JsxOpeningElement"
     *
     * For our current use-cases this is undesired behavior, so we just suppress it
     * and log a warning.
     */ (x4)
/* istanbul ignore next */ (x5)
```

### `allowlistSupportedDiagnostics(diagnostics: readonly (Diagnostic | DiagnosticWithLocation)[]): readonly (Diagnostic | DiagnosticWithLocation)[]`

<details><summary>Code</summary>

```ts
function allowlistSupportedDiagnostics(
  diagnostics: readonly (Diagnostic | DiagnosticWithLocation)[],
): readonly (Diagnostic | DiagnosticWithLocation)[] {
  return diagnostics.filter(diagnostic => {
    switch (diagnostic.code) {
      case 1013: // "A rest parameter or binding pattern may not have a trailing comma."
      case 1014: // "A rest parameter must be last in a parameter list."
      case 1044: // "'{0}' modifier cannot appear on a module or namespace element."
      case 1045: // "A '{0}' modifier cannot be used with an interface declaration."
      case 1048: // "A rest parameter cannot have an initializer."
      case 1049: // "A 'set' accessor must have exactly one parameter."
      case 1070: // "'{0}' modifier cannot appear on a type member."
      case 1071: // "'{0}' modifier cannot appear on an index signature."
      case 1085: // "Octal literals are not available when targeting ECMAScript 5 and higher. Use the syntax '{0}'."
      case 1090: // "'{0}' modifier cannot appear on a parameter."
      case 1096: // "An index signature must have exactly one parameter."
      case 1097: // "'{0}' list cannot be empty."
      case 1098: // "Type parameter list cannot be empty."
      case 1099: // "Type argument list cannot be empty."
      case 1117: // "An object literal cannot have multiple properties with the same name in strict mode."
      case 1121: // "Octal literals are not allowed in strict mode."
      case 1123: //  "Variable declaration list cannot be empty."
      case 1141: // "String literal expected."
      case 1162: // "An object member cannot be declared optional."
      case 1164: // "Computed property names are not allowed in enums."
      case 1172: // "'extends' clause already seen."
      case 1173: // "'extends' clause must precede 'implements' clause."
      case 1175: // "'implements' clause already seen."
      case 1176: // "Interface declaration cannot have 'implements' clause."
      case 1190: // "The variable declaration of a 'for...of' statement cannot have an initializer."
      case 1196: // "Catch clause variable type annotation must be 'any' or 'unknown' if specified."
      case 1200: // "Line terminator not permitted before arrow."
      case 1206: // "Decorators are not valid here."
      case 1211: // "A class declaration without the 'default' modifier must have a name."
      case 1242: // "'abstract' modifier can only appear on a class, method, or property declaration."
      case 1246: // "An interface property cannot have an initializer."
      case 1255: // "A definite assignment assertion '!' is not permitted in this context."
      case 1308: // "'await' expression is only allowed within an async function."
      case 2364: // "The left-hand side of an assignment expression must be a variable or a property access."
      case 2369: // "A parameter property is only allowed in a constructor implementation."
      case 2452: // "An enum member cannot have a numeric name."
      case 2462: // "A rest element must be last in a destructuring pattern."
      case 8017: // "Octal literal types must use ES2015 syntax. Use the syntax '{0}'."
      case 17012: // "'{0}' is not a valid meta-property for keyword '{1}'. Did you mean '{2}'?"
      case 17013: // "Meta-property '{0}' is only allowed in the body of a function declaration, function expression, or constructor."
        return true;
    }
    return false;
  });
}
```
</details>

- **Parameters**:
  - `diagnostics: readonly (Diagnostic | DiagnosticWithLocation)[]`
- **Return Type**: `readonly (Diagnostic | DiagnosticWithLocation)[]`
- **Calls**:
  - `diagnostics.filter`
### `convertDiagnosticToSemanticOrSyntacticError(diagnostic: Diagnostic): SemanticOrSyntacticError`

<details><summary>Code</summary>

```ts
function convertDiagnosticToSemanticOrSyntacticError(
  diagnostic: Diagnostic,
): SemanticOrSyntacticError {
  return {
    ...diagnostic,
    message: flattenDiagnosticMessageText(diagnostic.messageText, sys.newLine),
  };
}
```
</details>

- **Parameters**:
  - `diagnostic: Diagnostic`
- **Return Type**: `SemanticOrSyntacticError`
- **Calls**:
  - `flattenDiagnosticMessageText (from typescript)`

---

## Interfaces

### `SemanticOrSyntacticError`

<details><summary>Interface Code</summary>

```ts
export interface SemanticOrSyntacticError extends Diagnostic {
  message: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `message` | `string` | ✗ |  |


---