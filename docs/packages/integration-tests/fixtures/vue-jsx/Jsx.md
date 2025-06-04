[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Jsx.vue`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 1 |
| 💠 JSX Elements | 6 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Decorators](#decorators)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/integration-tests/fixtures/vue-jsx/Jsx.vue`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Vue` | `vue` |
| `mapMutations` | `vuex` |
| `Component` | `vue-property-decorator` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `path` | `any` | const | `'/'` | ✗ |


---

## Decorators

| Name | Target | Target Type | Arguments |
|------|--------|-------------|----------|
| `@Component` | `Jsx` | class | {
  created() {
    this.toggleHeader(false);
  },
  methods: {
    ...mapMutations('APP_SCOPE_NAME', ['toggleHeader']),
  },
} |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | class="mg-notFound" | <div> |
| `div` | element | class="fixed-center text-center" | <p>, <p>, <q-btn> |
| `p` | element | *none* | text: "img goes here" |
| `p` | element | class="text-faded" | text: "Sorry, nothing here...", <strong> |
| `strong` | element | *none* | text: "(404)" |
| `q-btn` | element | color="secondary", style="width:200px;", onClick={() => console.log(path)} | text: "Go back" |


---

## Functions

### `Jsx.render(): JSX.Element`

<details><summary>Code</summary>

```ts
render(): JSX.Element {
    // expected error - no-explicit-any
    const path: any = '/';
    return (
      // An error occurred in the next line: "Parsing error: '>' expected.eslint"
      <div class="mg-notFound">
        <div class="fixed-center text-center">
          <p>img goes here</p>
          <p class="text-faded">
            Sorry, nothing here...<strong>(404)</strong>
          </p>
          <q-btn
            color="secondary"
            style="width:200px;"
            onClick={() => console.log(path)}
          >
            Go back
          </q-btn>
        </div>
      </div>
    );
  }
```
</details>

- **Return Type**: `JSX.Element`
- **Calls**:
  - `console.log`
- **Internal Comments**:
```
// expected error - no-explicit-any (x2)
// An error occurred in the next line: "Parsing error: '>' expected.eslint" (x2)
```


---

## Classes

### `Jsx`

<details><summary>Class Code</summary>

```ts
@Component({
  created() {
    this.toggleHeader(false);
  },
  methods: {
    ...mapMutations('APP_SCOPE_NAME', ['toggleHeader']),
  },
})
export default class Jsx extends Vue {
  render(): JSX.Element {
    // expected error - no-explicit-any
    const path: any = '/';
    return (
      // An error occurred in the next line: "Parsing error: '>' expected.eslint"
      <div class="mg-notFound">
        <div class="fixed-center text-center">
          <p>img goes here</p>
          <p class="text-faded">
            Sorry, nothing here...<strong>(404)</strong>
          </p>
          <q-btn
            color="secondary"
            style="width:200px;"
            onClick={() => console.log(path)}
          >
            Go back
          </q-btn>
        </div>
      </div>
    );
  }
}
```
</details>

#### Methods

##### `render(): JSX.Element`

<details><summary>Code</summary>

```ts
render(): JSX.Element {
    // expected error - no-explicit-any
    const path: any = '/';
    return (
      // An error occurred in the next line: "Parsing error: '>' expected.eslint"
      <div class="mg-notFound">
        <div class="fixed-center text-center">
          <p>img goes here</p>
          <p class="text-faded">
            Sorry, nothing here...<strong>(404)</strong>
          </p>
          <q-btn
            color="secondary"
            style="width:200px;"
            onClick={() => console.log(path)}
          >
            Go back
          </q-btn>
        </div>
      </div>
    );
  }
```
</details>


---