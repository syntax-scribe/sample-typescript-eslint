[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `ConfigTypeScript.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 13 |
| 📊 Variables & Constants | 1 |
| 💠 JSX Elements | 1 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/config/ConfigTypeScript.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useCallback` | `react` |
| `useEffect` | `react` |
| `useMemo` | `react` |
| `useState` | `react` |
| `React` | `react` |
| `ConfigModel` | `../types` |
| `ConfigOptionsType` | `./ConfigEditor` |
| `ensureObject` | `../lib/json` |
| `parseJSONObject` | `../lib/json` |
| `toJson` | `../lib/json` |
| `getTypescriptOptions` | `../lib/jsonSchema` |
| `shallowEqual` | `../lib/shallowEqual` |
| `ConfigEditor` | `./ConfigEditor` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `category` | `any` | const | `item.category.message` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `ConfigEditor` | component | className={className}, onChange={onChange}, options={options}, values={configObject} | *none* |


---

## Functions

### `ConfigTypeScript(props: ConfigTypeScriptProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function ConfigTypeScript(props: ConfigTypeScriptProps): React.JSX.Element {
  const { className, config, onChange: onChangeProp } = props;

  const [configObject, updateConfigObject] = useState<Record<string, unknown>>(
    () => ({}),
  );

  useEffect(() => {
    updateConfigObject(oldConfig => {
      const newConfig = ensureObject(parseJSONObject(config).compilerOptions);
      if (shallowEqual(oldConfig, newConfig)) {
        return oldConfig;
      }
      return newConfig;
    });
  }, [config]);

  const options = useMemo((): ConfigOptionsType[] => {
    return Object.values(
      getTypescriptOptions().reduce<Record<string, ConfigOptionsType>>(
        (group, item) => {
          const category = item.category.message;
          group[category] ??= {
            fields: [],
            heading: category,
          };
          if (item.type === 'boolean') {
            group[category].fields.push({
              key: item.name,
              label: item.description.message,
              type: 'boolean',
            });
          } else if (item.type instanceof Map) {
            group[category].fields.push({
              enum: ['', ...item.type.keys()],
              key: item.name,
              label: item.description.message,
              type: 'string',
            });
          }
          return group;
        },
        {},
      ),
    );
  }, []);

  const onChange = useCallback(
    (newConfig: Record<string, unknown>) => {
      const parsed = parseJSONObject(config);
      parsed.compilerOptions = newConfig;
      updateConfigObject(newConfig);
      onChangeProp({ tsconfig: toJson(parsed) });
    },
    [config, onChangeProp],
  );

  return (
    <ConfigEditor
      className={className}
      onChange={onChange}
      options={options}
      values={configObject}
    />
  );
}
```
</details>

- **Parameters**:
  - `props: ConfigTypeScriptProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useState (from react)`
  - `useEffect (from react)`
  - `updateConfigObject`
  - `ensureObject (from ../lib/json)`
  - `parseJSONObject (from ../lib/json)`
  - `shallowEqual (from ../lib/shallowEqual)`
  - `useMemo (from react)`
  - `Object.values`
  - `getTypescriptOptions().reduce`
  - `group[category].fields.push`
  - `item.type.keys`
  - `useCallback (from react)`
  - `onChangeProp`
  - `toJson (from ../lib/json)`

---

## Interfaces

### `ConfigTypeScriptProps`

<details><summary>Interface Code</summary>

```ts
interface ConfigTypeScriptProps {
  readonly className?: string;
  readonly config?: string;
  readonly onChange: (config: Partial<ConfigModel>) => void;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `className` | `string` | ✓ |  |
| `config` | `string` | ✓ |  |
| `onChange` | `(config: Partial<ConfigModel>) => void` | ✗ |  |


---