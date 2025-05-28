[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `builtinSymbolLikes.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 8 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/src/builtinSymbolLikes.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `isSymbolFromDefaultLibrary` | `./isSymbolFromDefaultLibrary` |


---

## Functions

### `isPromiseLike(program: ts.Program, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
export function isPromiseLike(program: ts.Program, type: ts.Type): boolean {
  return isBuiltinSymbolLike(program, type, 'Promise');
}
```
</details>

- **JSDoc**:
```ts
/**
 * @example
 * ```ts
 * class DerivedClass extends Promise<number> {}
 * DerivedClass.reject
 * // ^ PromiseLike
 * ```
 */
```

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isBuiltinSymbolLike`
### `isPromiseConstructorLike(program: ts.Program, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
export function isPromiseConstructorLike(
  program: ts.Program,
  type: ts.Type,
): boolean {
  return isBuiltinSymbolLike(program, type, 'PromiseConstructor');
}
```
</details>

- **JSDoc**:
```ts
/**
 * @example
 * ```ts
 * const value = Promise
 * value.reject
 * // ^ PromiseConstructorLike
 * ```
 */
```

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isBuiltinSymbolLike`
### `isErrorLike(program: ts.Program, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
export function isErrorLike(program: ts.Program, type: ts.Type): boolean {
  return isBuiltinSymbolLike(program, type, 'Error');
}
```
</details>

- **JSDoc**:
```ts
/**
 * @example
 * ```ts
 * class Foo extends Error {}
 * new Foo()
 * //   ^ ErrorLike
 * ```
 */
```

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isBuiltinSymbolLike`
### `isReadonlyErrorLike(program: ts.Program, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
export function isReadonlyErrorLike(
  program: ts.Program,
  type: ts.Type,
): boolean {
  return isReadonlyTypeLike(program, type, subtype => {
    const [typeArgument] = subtype.aliasTypeArguments;
    return (
      isErrorLike(program, typeArgument) ||
      isReadonlyErrorLike(program, typeArgument)
    );
  });
}
```
</details>

- **JSDoc**:
```ts
/**
 * @example
 * ```ts
 * type T = Readonly<Error>
 * //   ^ ReadonlyErrorLike
 * ```
 */
```

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isReadonlyTypeLike`
  - `isErrorLike`
  - `isReadonlyErrorLike`
### `isReadonlyTypeLike(program: ts.Program, type: ts.Type, predicate: (
    subType: {
      aliasSymbol: ts.Symbol;
      aliasTypeArguments: readonly ts.Type[];
    } & ts.Type,
  ) => boolean): boolean`

<details><summary>Code</summary>

```ts
export function isReadonlyTypeLike(
  program: ts.Program,
  type: ts.Type,
  predicate?: (
    subType: {
      aliasSymbol: ts.Symbol;
      aliasTypeArguments: readonly ts.Type[];
    } & ts.Type,
  ) => boolean,
): boolean {
  return isBuiltinTypeAliasLike(program, type, subtype => {
    return (
      subtype.aliasSymbol.getName() === 'Readonly' && !!predicate?.(subtype)
    );
  });
}
```
</details>

- **JSDoc**:
```ts
/**
 * @example
 * ```ts
 * type T = Readonly<{ foo: 'bar' }>
 * //   ^ ReadonlyTypeLike
 * ```
 */
```

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
  - `predicate: (
    subType: {
      aliasSymbol: ts.Symbol;
      aliasTypeArguments: readonly ts.Type[];
    } & ts.Type,
  ) => boolean`
- **Return Type**: `boolean`
- **Calls**:
  - `isBuiltinTypeAliasLike`
  - `subtype.aliasSymbol.getName`
  - `predicate`
### `isBuiltinTypeAliasLike(program: ts.Program, type: ts.Type, predicate: (
    subType: {
      aliasSymbol: ts.Symbol;
      aliasTypeArguments: readonly ts.Type[];
    } & ts.Type,
  ) => boolean): boolean`

<details><summary>Code</summary>

```ts
export function isBuiltinTypeAliasLike(
  program: ts.Program,
  type: ts.Type,
  predicate: (
    subType: {
      aliasSymbol: ts.Symbol;
      aliasTypeArguments: readonly ts.Type[];
    } & ts.Type,
  ) => boolean,
): boolean {
  return isBuiltinSymbolLikeRecurser(program, type, subtype => {
    const { aliasSymbol, aliasTypeArguments } = subtype;

    if (!aliasSymbol || !aliasTypeArguments) {
      return false;
    }

    if (
      isSymbolFromDefaultLibrary(program, aliasSymbol) &&
      predicate(
        subtype as {
          aliasSymbol: ts.Symbol;
          aliasTypeArguments: readonly ts.Type[];
        } & ts.Type,
      )
    ) {
      return true;
    }

    return null;
  });
}
```
</details>

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
  - `predicate: (
    subType: {
      aliasSymbol: ts.Symbol;
      aliasTypeArguments: readonly ts.Type[];
    } & ts.Type,
  ) => boolean`
- **Return Type**: `boolean`
- **Calls**:
  - `isBuiltinSymbolLikeRecurser`
  - `isSymbolFromDefaultLibrary (from ./isSymbolFromDefaultLibrary)`
  - `predicate`
### `isBuiltinSymbolLike(program: ts.Program, type: ts.Type, symbolName: string | string[]): boolean`

<details><summary>Code</summary>

```ts
export function isBuiltinSymbolLike(
  program: ts.Program,
  type: ts.Type,
  symbolName: string | string[],
): boolean {
  return isBuiltinSymbolLikeRecurser(program, type, subType => {
    const symbol = subType.getSymbol();
    if (!symbol) {
      return false;
    }

    const actualSymbolName = symbol.getName();

    if (
      (Array.isArray(symbolName)
        ? symbolName.some(name => actualSymbolName === name)
        : actualSymbolName === symbolName) &&
      isSymbolFromDefaultLibrary(program, symbol)
    ) {
      return true;
    }

    return null;
  });
}
```
</details>

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
  - `symbolName: string | string[]`
- **Return Type**: `boolean`
- **Calls**:
  - `isBuiltinSymbolLikeRecurser`
  - `subType.getSymbol`
  - `symbol.getName`
  - `Array.isArray`
  - `symbolName.some`
  - `isSymbolFromDefaultLibrary (from ./isSymbolFromDefaultLibrary)`
### `isBuiltinSymbolLikeRecurser(program: ts.Program, type: ts.Type, predicate: (subType: ts.Type) => boolean | null): boolean`

<details><summary>Code</summary>

```ts
export function isBuiltinSymbolLikeRecurser(
  program: ts.Program,
  type: ts.Type,
  predicate: (subType: ts.Type) => boolean | null,
): boolean {
  if (type.isIntersection()) {
    return type.types.some(t =>
      isBuiltinSymbolLikeRecurser(program, t, predicate),
    );
  }
  if (type.isUnion()) {
    return type.types.every(t =>
      isBuiltinSymbolLikeRecurser(program, t, predicate),
    );
  }
  if (tsutils.isTypeParameter(type)) {
    const t = type.getConstraint();

    if (t) {
      return isBuiltinSymbolLikeRecurser(program, t, predicate);
    }

    return false;
  }

  const predicateResult = predicate(type);
  if (typeof predicateResult === 'boolean') {
    return predicateResult;
  }

  const symbol = type.getSymbol();
  if (
    symbol &&
    symbol.flags & (ts.SymbolFlags.Class | ts.SymbolFlags.Interface)
  ) {
    const checker = program.getTypeChecker();
    for (const baseType of checker.getBaseTypes(type as ts.InterfaceType)) {
      if (isBuiltinSymbolLikeRecurser(program, baseType, predicate)) {
        return true;
      }
    }
  }
  return false;
}
```
</details>

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
  - `predicate: (subType: ts.Type) => boolean | null`
- **Return Type**: `boolean`
- **Calls**:
  - `type.isIntersection`
  - `type.types.some`
  - `isBuiltinSymbolLikeRecurser`
  - `type.isUnion`
  - `type.types.every`
  - `tsutils.isTypeParameter`
  - `type.getConstraint`
  - `predicate`
  - `type.getSymbol`
  - `program.getTypeChecker`
  - `checker.getBaseTypes`

---