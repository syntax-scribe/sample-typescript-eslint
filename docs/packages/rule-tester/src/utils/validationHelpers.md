[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `validationHelpers.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 6
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/validationHelpers.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `Parser` | `@typescript-eslint/utils/ts-eslint` |
| `SourceCode` | `@typescript-eslint/utils/ts-eslint` |
| `simpleTraverse` | `@typescript-eslint/typescript-estree` |


---

## Functions

### `sanitize(text: string): string`

<details><summary>Code</summary>

```ts
export function sanitize(text: string): string {
  if (typeof text !== 'string') {
    return '';
  }
  return text.replaceAll(
    // eslint-disable-next-line no-control-regex
    /[\u0000-\u0009\u000b-\u001a]/gu,
    // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
    c => `\\u${c.codePointAt(0)!.toString(16).padStart(4, '0')}`,
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Replace control characters by `\u00xx` form.
 */
```

- **Parameters**:
  - `text: string`
- **Return Type**: `string`
- **Calls**:
  - `text.replaceAll`
  - `c.codePointAt(0)!.toString(16).padStart`
- **Internal Comments**:
```
// eslint-disable-next-line no-control-regex
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x3)
```

### `wrapParser(parser: Parser.LooseParserModule): Parser.LooseParserModule`

<details><summary>Code</summary>

```ts
export function wrapParser(
  parser: Parser.LooseParserModule,
): Parser.LooseParserModule {
  /**
   * Define `start`/`end` properties of all nodes of the given AST as throwing error.
   */
  function defineStartEndAsErrorInTree(
    ast: TSESTree.Program,
    visitorKeys?: Readonly<SourceCode.VisitorKeys>,
  ): void {
    /**
     * Define `start`/`end` properties as throwing error.
     */
    function defineStartEndAsError(objName: string, node: unknown): void {
      Object.defineProperties(node, {
        end: {
          configurable: true,
          enumerable: false,
          get() {
            throw new Error(
              `Use ${objName}.range[1] instead of ${objName}.end`,
            );
          },
        },
        start: {
          configurable: true,
          enumerable: false,
          get() {
            throw new Error(
              `Use ${objName}.range[0] instead of ${objName}.start`,
            );
          },
        },
      });
    }

    simpleTraverse(ast, {
      enter: node => defineStartEndAsError('node', node),
      visitorKeys,
    });
    ast.tokens?.forEach(token => defineStartEndAsError('token', token));
    ast.comments?.forEach(comment => defineStartEndAsError('token', comment));
  }

  if ('parseForESLint' in parser) {
    return {
      parseForESLint(...args): Parser.ParseResult {
        const parsed = parser.parseForESLint(...args) as Parser.ParseResult;

        defineStartEndAsErrorInTree(parsed.ast, parsed.visitorKeys);
        return parsed;
      },

      // @ts-expect-error -- see above
      [parserSymbol]: parser,
    };
  }

  return {
    parse(...args): TSESTree.Program {
      const ast = parser.parse(...args) as TSESTree.Program;

      defineStartEndAsErrorInTree(ast);
      return ast;
    },

    // @ts-expect-error -- see above
    [parserSymbol]: parser,
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Wraps the given parser in order to intercept and modify return values from the `parse` and `parseForESLint` methods, for test purposes.
 * In particular, to modify ast nodes, tokens and comments to throw on access to their `start` and `end` properties.
 */
```

- **Parameters**:
  - `parser: Parser.LooseParserModule`
- **Return Type**: `Parser.LooseParserModule`
- **Calls**:
  - `Object.defineProperties`
  - `simpleTraverse (from @typescript-eslint/typescript-estree)`
  - `defineStartEndAsError`
  - `ast.tokens?.forEach`
  - `ast.comments?.forEach`
  - `parser.parseForESLint`
  - `defineStartEndAsErrorInTree`
  - `parser.parse`
- **Internal Comments**:
```
/**
   * Define `start`/`end` properties of all nodes of the given AST as throwing error.
   */
/**
     * Define `start`/`end` properties as throwing error.
     */
// @ts-expect-error -- see above (x4)
```

### `defineStartEndAsErrorInTree(ast: TSESTree.Program, visitorKeys: Readonly<SourceCode.VisitorKeys>): void`

<details><summary>Code</summary>

```ts
function defineStartEndAsErrorInTree(
    ast: TSESTree.Program,
    visitorKeys?: Readonly<SourceCode.VisitorKeys>,
  ): void {
    /**
     * Define `start`/`end` properties as throwing error.
     */
    function defineStartEndAsError(objName: string, node: unknown): void {
      Object.defineProperties(node, {
        end: {
          configurable: true,
          enumerable: false,
          get() {
            throw new Error(
              `Use ${objName}.range[1] instead of ${objName}.end`,
            );
          },
        },
        start: {
          configurable: true,
          enumerable: false,
          get() {
            throw new Error(
              `Use ${objName}.range[0] instead of ${objName}.start`,
            );
          },
        },
      });
    }

    simpleTraverse(ast, {
      enter: node => defineStartEndAsError('node', node),
      visitorKeys,
    });
    ast.tokens?.forEach(token => defineStartEndAsError('token', token));
    ast.comments?.forEach(comment => defineStartEndAsError('token', comment));
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Define `start`/`end` properties of all nodes of the given AST as throwing error.
   */
```

- **Parameters**:
  - `ast: TSESTree.Program`
  - `visitorKeys: Readonly<SourceCode.VisitorKeys>`
- **Return Type**: `void`
- **Calls**:
  - `Object.defineProperties`
  - `simpleTraverse (from @typescript-eslint/typescript-estree)`
  - `defineStartEndAsError`
  - `ast.tokens?.forEach`
  - `ast.comments?.forEach`
- **Internal Comments**:
```
/**
     * Define `start`/`end` properties as throwing error.
     */
```

### `defineStartEndAsError(objName: string, node: unknown): void`

<details><summary>Code</summary>

```ts
function defineStartEndAsError(objName: string, node: unknown): void {
      Object.defineProperties(node, {
        end: {
          configurable: true,
          enumerable: false,
          get() {
            throw new Error(
              `Use ${objName}.range[1] instead of ${objName}.end`,
            );
          },
        },
        start: {
          configurable: true,
          enumerable: false,
          get() {
            throw new Error(
              `Use ${objName}.range[0] instead of ${objName}.start`,
            );
          },
        },
      });
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Define `start`/`end` properties as throwing error.
     */
```

- **Parameters**:
  - `objName: string`
  - `node: unknown`
- **Return Type**: `void`
- **Calls**:
  - `Object.defineProperties`
### `enter(node: any): void`

<details><summary>Code</summary>

```ts
node => defineStartEndAsError('node', node)
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `defineStartEndAsError`
### `enter(node: any): void`

<details><summary>Code</summary>

```ts
node => defineStartEndAsError('node', node)
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `defineStartEndAsError`

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