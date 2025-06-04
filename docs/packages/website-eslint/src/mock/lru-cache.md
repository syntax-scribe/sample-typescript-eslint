[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `lru-cache.js`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/website-eslint/src/mock/lru-cache.js`**

## Functions

### `LruCache.get(name: any): any`

<details><summary>Code</summary>

```ts
get(name) {
    return this.cache.get(name);
  }
```
</details>

- **Parameters**:
  - `name: any`
- **Return Type**: `any`
- **Calls**:
  - `this.cache.get`
### `LruCache.set(name: any, value: any): any`

<details><summary>Code</summary>

```ts
set(name, value) {
    this.cache.set(name, value);
    return value;
  }
```
</details>

- **Parameters**:
  - `name: any`
  - `value: any`
- **Return Type**: `any`
- **Calls**:
  - `this.cache.set`

---

## Classes

### `LruCache`

<details><summary>Class Code</summary>

```ts
class LruCache {
  constructor() {
    this.cache = new Map();
  }
  get(name) {
    return this.cache.get(name);
  }
  set(name, value) {
    this.cache.set(name, value);
    return value;
  }
}
```
</details>

#### Methods

##### `get(name: any): any`

<details><summary>Code</summary>

```ts
get(name) {
    return this.cache.get(name);
  }
```
</details>

##### `set(name: any, value: any): any`

<details><summary>Code</summary>

```ts
set(name, value) {
    this.cache.set(name, value);
    return value;
  }
```
</details>


---