[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Jsx.vue`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 1
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/integration-tests/fixtures/vue-jsx/Jsx.vue`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Vue` | `vue` |
| `mapMutations` | `vuex` |
| `Component` | `vue-property-decorator` |


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

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---