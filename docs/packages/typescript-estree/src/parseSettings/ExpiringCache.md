[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ExpiringCache.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 1 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 3 |
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
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/parseSettings/ExpiringCache.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `CacheDurationSeconds` | `@typescript-eslint/types` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `DEFAULT_TSCONFIG_CACHE_DURATION_SECONDS` | `30` | const | `30` | ✓ |
| `ZERO_HR_TIME` | `[number, number]` | const | `[0, 0]` | ✗ |
| `ageSeconds` | `number` | const | `process.hrtime(entry.lastSeen)[0]` | ✗ |


---

## Functions

### `ExpiringCache.clear(): void`

<details><summary>Code</summary>

```ts
clear(): void {
    this.#map.clear();
  }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `this.#map.clear`
### `ExpiringCache.get(key: Key): Value | undefined`

<details><summary>Code</summary>

```ts
get(key: Key): Value | undefined {
    const entry = this.#map.get(key);
    if (entry?.value != null) {
      if (this.#cacheDurationSeconds === 'Infinity') {
        return entry.value;
      }

      const ageSeconds = process.hrtime(entry.lastSeen)[0];
      if (ageSeconds < this.#cacheDurationSeconds) {
        // cache hit woo!
        return entry.value;
      }
      // key has expired - clean it up to free up memory
      this.#map.delete(key);
    }
    // no hit :'(
    return undefined;
  }
```
</details>

- **Parameters**:
  - `key: Key`
- **Return Type**: `Value | undefined`
- **Calls**:
  - `this.#map.get`
  - `process.hrtime`
  - `this.#map.delete`
- **Internal Comments**:
```
// cache hit woo!
// key has expired - clean it up to free up memory (x5)
// no hit :'(
```

### `ExpiringCache.set(key: Key, value: Value): this`

<details><summary>Code</summary>

```ts
set(key: Key, value: Value): this {
    this.#map.set(key, {
      lastSeen:
        this.#cacheDurationSeconds === 'Infinity'
          ? // no need to waste time calculating the hrtime in infinity mode as there's no expiry
            ZERO_HR_TIME
          : process.hrtime(),
      value,
    });
    return this;
  }
```
</details>

- **Parameters**:
  - `key: Key`
  - `value: Value`
- **Return Type**: `this`
- **Calls**:
  - `this.#map.set`
  - `process.hrtime`

---

## Classes

### `ExpiringCache`

<details><summary>Class Code</summary>

```ts
export class ExpiringCache<Key, Value> implements CacheLike<Key, Value> {
  readonly #cacheDurationSeconds: CacheDurationSeconds;

  readonly #map = new Map<
    Key,
    Readonly<{
      lastSeen: [number, number];
      value: Value;
    }>
  >();

  constructor(cacheDurationSeconds: CacheDurationSeconds) {
    this.#cacheDurationSeconds = cacheDurationSeconds;
  }

  clear(): void {
    this.#map.clear();
  }

  get(key: Key): Value | undefined {
    const entry = this.#map.get(key);
    if (entry?.value != null) {
      if (this.#cacheDurationSeconds === 'Infinity') {
        return entry.value;
      }

      const ageSeconds = process.hrtime(entry.lastSeen)[0];
      if (ageSeconds < this.#cacheDurationSeconds) {
        // cache hit woo!
        return entry.value;
      }
      // key has expired - clean it up to free up memory
      this.#map.delete(key);
    }
    // no hit :'(
    return undefined;
  }

  set(key: Key, value: Value): this {
    this.#map.set(key, {
      lastSeen:
        this.#cacheDurationSeconds === 'Infinity'
          ? // no need to waste time calculating the hrtime in infinity mode as there's no expiry
            ZERO_HR_TIME
          : process.hrtime(),
      value,
    });
    return this;
  }
}
```
</details>

#### Methods

##### `clear(): void`

<details><summary>Code</summary>

```ts
clear(): void {
    this.#map.clear();
  }
```
</details>

##### `get(key: Key): Value | undefined`

<details><summary>Code</summary>

```ts
get(key: Key): Value | undefined {
    const entry = this.#map.get(key);
    if (entry?.value != null) {
      if (this.#cacheDurationSeconds === 'Infinity') {
        return entry.value;
      }

      const ageSeconds = process.hrtime(entry.lastSeen)[0];
      if (ageSeconds < this.#cacheDurationSeconds) {
        // cache hit woo!
        return entry.value;
      }
      // key has expired - clean it up to free up memory
      this.#map.delete(key);
    }
    // no hit :'(
    return undefined;
  }
```
</details>

##### `set(key: Key, value: Value): this`

<details><summary>Code</summary>

```ts
set(key: Key, value: Value): this {
    this.#map.set(key, {
      lastSeen:
        this.#cacheDurationSeconds === 'Infinity'
          ? // no need to waste time calculating the hrtime in infinity mode as there's no expiry
            ZERO_HR_TIME
          : process.hrtime(),
      value,
    });
    return this;
  }
```
</details>


---

## Interfaces

### `CacheLike<Key, Value>`

<details><summary>Interface Code</summary>

```ts
export interface CacheLike<Key, Value> {
  get(key: Key): Value | undefined;
  set(key: Key, value: Value): this;
}
```
</details>


---