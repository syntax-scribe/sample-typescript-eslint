[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `useHashState.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 10
- **Classes**: 0
- **Imports**: 10
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/hooks/useHashState.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useHistory` | `@docusaurus/router` |
| `useCallback` | `react` |
| `useState` | `react` |
| `ConfigFileType` | `../types` |
| `ConfigModel` | `../types` |
| `ConfigShowAst` | `../types` |
| `hasOwnProperty` | `../lib/has-own-property` |
| `toJsonConfig` | `../lib/json` |
| `shallowEqual` | `../lib/shallowEqual` |
| `fileTypes` | `../options` |


---

## Functions

### `writeQueryParam(value: string | null): string`

<details><summary>Code</summary>

```ts
function writeQueryParam(value: string | null): string {
  return (value && lz.compressToEncodedURIComponent(value)) ?? '';
}
```
</details>

- **Parameters**:
  - `value: string | null`
- **Return Type**: `string`
- **Calls**:
  - `lz.compressToEncodedURIComponent`
### `readQueryParam(value: string | null, fallback: string): string`

<details><summary>Code</summary>

```ts
function readQueryParam(value: string | null, fallback: string): string {
  return (value && lz.decompressFromEncodedURIComponent(value)) ?? fallback;
}
```
</details>

- **Parameters**:
  - `value: string | null`
  - `fallback: string`
- **Return Type**: `string`
- **Calls**:
  - `lz.decompressFromEncodedURIComponent`
### `readShowAST(value: string | null): ConfigShowAst`

<details><summary>Code</summary>

```ts
function readShowAST(value: string | null): ConfigShowAst {
  switch (value) {
    case 'es':
    case 'scope':
    case 'ts':
    case 'types':
      return value;
  }
  return value ? 'es' : false;
}
```
</details>

- **Parameters**:
  - `value: string | null`
- **Return Type**: `ConfigShowAst`
### `readFileType(value: string | null): ConfigFileType`

<details><summary>Code</summary>

```ts
function readFileType(value: string | null): ConfigFileType {
  if (value && (fileTypes as string[]).includes(value)) {
    return value as ConfigFileType;
  }
  return '.ts';
}
```
</details>

- **Parameters**:
  - `value: string | null`
- **Return Type**: `ConfigFileType`
- **Calls**:
  - `(fileTypes as string[]).includes`
### `readLegacyParam(data: string | null, prop: string): string | undefined`

<details><summary>Code</summary>

```ts
function readLegacyParam(
  data: string | null,
  prop: string,
): string | undefined {
  try {
    return toJsonConfig(JSON.parse(readQueryParam(data, '{}')), prop);
  } catch (e) {
    console.error(e, data, prop);
  }
  return undefined;
}
```
</details>

- **Parameters**:
  - `data: string | null`
  - `prop: string`
- **Return Type**: `string | undefined`
- **Calls**:
  - `toJsonConfig (from ../lib/json)`
  - `JSON.parse`
  - `readQueryParam`
  - `console.error`
### `parseStateFromUrl(hash: string, initialState: ConfigModel): Partial<ConfigModel> | undefined`

<details><summary>Code</summary>

```ts
(
  hash: string,
  initialState: ConfigModel,
): Partial<ConfigModel> | undefined => {
  if (!hash) {
    return;
  }

  try {
    const searchParams = new URLSearchParams(hash);

    let eslintrc: string | undefined;
    if (searchParams.has('eslintrc')) {
      eslintrc = readQueryParam(searchParams.get('eslintrc'), '');
    } else if (searchParams.has('rules')) {
      eslintrc = readLegacyParam(searchParams.get('rules'), 'rules');
    }

    let tsconfig: string | undefined;
    if (searchParams.has('tsconfig')) {
      tsconfig = readQueryParam(searchParams.get('tsconfig'), '');
    } else if (searchParams.has('tsConfig')) {
      tsconfig = readLegacyParam(
        searchParams.get('tsConfig'),
        'compilerOptions',
      );
    }

    let esQuery: ConfigModel['esQuery'] | undefined;
    if (searchParams.has('esQuery')) {
      esQuery = JSON.parse(
        readQueryParam(searchParams.get('esQuery'), ''),
      ) as ConfigModel['esQuery'];
    }

    const fileType =
      searchParams.get('jsx') === 'true'
        ? '.tsx'
        : readFileType(searchParams.get('fileType'));

    const code = searchParams.has('code')
      ? readQueryParam(searchParams.get('code'), '')
      : '';

    return {
      code,
      eslintrc: eslintrc ?? initialState.eslintrc,
      esQuery,
      fileType,
      showAST: readShowAST(searchParams.get('showAST')),
      showTokens: searchParams.get('tokens') === 'true',
      sourceType:
        searchParams.get('sourceType') === 'script' ? 'script' : 'module',
      ts: searchParams.get('ts') ?? process.env.TS_VERSION,
      tsconfig: tsconfig ?? initialState.tsconfig,
    };
  } catch (e) {
    console.warn(e);
  }
  return undefined;
}
```
</details>

- **Parameters**:
  - `hash: string`
  - `initialState: ConfigModel`
- **Return Type**: `Partial<ConfigModel> | undefined`
- **Calls**:
  - `searchParams.has`
  - `readQueryParam`
  - `searchParams.get`
  - `readLegacyParam`
  - `JSON.parse`
  - `readFileType`
  - `readShowAST`
  - `console.warn`
### `writeStateToUrl(newState: ConfigModel): string | undefined`

<details><summary>Code</summary>

```ts
(newState: ConfigModel): string | undefined => {
  try {
    const searchParams = new URLSearchParams();
    searchParams.set('ts', newState.ts.trim());
    if (newState.sourceType === 'script') {
      searchParams.set('sourceType', newState.sourceType);
    }
    if (newState.showAST) {
      searchParams.set('showAST', newState.showAST);
    }
    if (newState.fileType) {
      searchParams.set('fileType', newState.fileType);
    }
    if (newState.esQuery) {
      searchParams.set(
        'esQuery',
        writeQueryParam(JSON.stringify(newState.esQuery)),
      );
    }
    searchParams.set('code', writeQueryParam(newState.code));
    searchParams.set('eslintrc', writeQueryParam(newState.eslintrc));
    searchParams.set('tsconfig', writeQueryParam(newState.tsconfig));
    searchParams.set('tokens', String(!!newState.showTokens));
    return searchParams.toString();
  } catch (e) {
    console.warn(e);
  }
  return undefined;
}
```
</details>

- **Parameters**:
  - `newState: ConfigModel`
- **Return Type**: `string | undefined`
- **Calls**:
  - `searchParams.set`
  - `newState.ts.trim`
  - `writeQueryParam`
  - `JSON.stringify`
  - `String`
  - `searchParams.toString`
  - `console.warn`
### `retrieveStateFromLocalStorage(): Partial<ConfigModel> | undefined`

<details><summary>Code</summary>

```ts
(): Partial<ConfigModel> | undefined => {
  try {
    const configString = window.localStorage.getItem('config');
    if (!configString) {
      return undefined;
    }

    const config: unknown = JSON.parse(configString);
    if (typeof config !== 'object' || !config) {
      return undefined;
    }

    const state: Partial<ConfigModel> = {};
    if (hasOwnProperty('ts', config)) {
      const ts = config.ts;
      if (typeof ts === 'string') {
        state.ts = ts;
      }
    }
    if (hasOwnProperty('fileType', config)) {
      const fileType = config.fileType;
      if (fileType === 'true') {
        state.fileType = readFileType(fileType);
      }
    }
    if (hasOwnProperty('showAST', config)) {
      const showAST = config.showAST;
      if (typeof showAST === 'string') {
        state.showAST = readShowAST(showAST);
      }
    }
    state.scroll = hasOwnProperty('scroll', config) && !!config.scroll;

    return state;
  } catch (e) {
    console.warn(e);
  }
  return undefined;
}
```
</details>

- **Return Type**: `Partial<ConfigModel> | undefined`
- **Calls**:
  - `window.localStorage.getItem`
  - `JSON.parse`
  - `hasOwnProperty (from ../lib/has-own-property)`
  - `readFileType`
  - `readShowAST`
  - `console.warn`
### `writeStateToLocalStorage(newState: ConfigModel): void`

<details><summary>Code</summary>

```ts
(newState: ConfigModel): void => {
  const config: Partial<ConfigModel> = {
    fileType: newState.fileType,
    scroll: newState.scroll,
    showAST: newState.showAST,
    sourceType: newState.sourceType,
    ts: newState.ts,
  };
  window.localStorage.setItem('config', JSON.stringify(config));
}
```
</details>

- **Parameters**:
  - `newState: ConfigModel`
- **Return Type**: `void`
- **Calls**:
  - `window.localStorage.setItem`
  - `JSON.stringify`
### `useHashState(initialState: ConfigModel): [ConfigModel, (cfg: Partial<ConfigModel>) => void]`

<details><summary>Code</summary>

```ts
export function useHashState(
  initialState: ConfigModel,
): [ConfigModel, (cfg: Partial<ConfigModel>) => void] {
  const history = useHistory();
  const [state, setState] = useState<ConfigModel>(() => ({
    ...initialState,
    ...retrieveStateFromLocalStorage(),
    ...parseStateFromUrl(window.location.hash.slice(1), initialState),
  }));

  const updateState = useCallback(
    (cfg: Partial<ConfigModel>) => {
      console.info('[State] updating config diff', cfg);

      setState(oldState => {
        const newState = { ...oldState, ...cfg };

        if (shallowEqual(oldState, newState)) {
          return oldState;
        }

        writeStateToLocalStorage(newState);

        history.replace({
          ...history.location,
          hash: writeStateToUrl(newState),
        });

        if (cfg.ts) {
          window.location.reload();
        }
        return newState;
      });
    },
    [setState, history],
  );

  return [state, updateState];
}
```
</details>

- **Parameters**:
  - `initialState: ConfigModel`
- **Return Type**: `[ConfigModel, (cfg: Partial<ConfigModel>) => void]`
- **Calls**:
  - `useHistory (from @docusaurus/router)`
  - `useState (from react)`
  - `retrieveStateFromLocalStorage`
  - `parseStateFromUrl`
  - `window.location.hash.slice`
  - `useCallback (from react)`
  - `console.info`
  - `setState`
  - `shallowEqual (from ../lib/shallowEqual)`
  - `writeStateToLocalStorage`
  - `history.replace`
  - `writeStateToUrl`
  - `window.location.reload`

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