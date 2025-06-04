[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `ConfigEslint.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 14 |
| 💠 JSX Elements | 1 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/config/ConfigEslint.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useCallback` | `react` |
| `useEffect` | `react` |
| `useMemo` | `react` |
| `useState` | `react` |
| `React` | `react` |
| `ConfigModel` | `../types` |
| `RuleDetails` | `../types` |
| `ConfigOptionsField` | `./ConfigEditor` |
| `ConfigOptionsType` | `./ConfigEditor` |
| `ensureObject` | `../lib/json` |
| `parseJSONObject` | `../lib/json` |
| `toJson` | `../lib/json` |
| `shallowEqual` | `../lib/shallowEqual` |
| `ConfigEditor` | `./ConfigEditor` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `ConfigEditor` | component | className={className}, onChange={onChange}, options={options}, values={configObject} | *none* |


---

## Functions

### `ConfigEslint(props: ConfigEslintProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function ConfigEslint(props: ConfigEslintProps): React.JSX.Element {
  const { className, config, onChange: onChangeProp, ruleOptions } = props;

  const [configObject, updateConfigObject] = useState<Record<string, unknown>>(
    () => ({}),
  );

  useEffect(() => {
    updateConfigObject(oldConfig => {
      const newConfig = ensureObject(parseJSONObject(config).rules);
      if (shallowEqual(oldConfig, newConfig)) {
        return oldConfig;
      }
      return newConfig;
    });
  }, [config]);

  const options = useMemo((): ConfigOptionsType[] => {
    const mappedRules: ConfigOptionsField[] = ruleOptions.map(item => ({
      defaults: ['error', 2, 'warn', 1, ['error'], ['warn'], [2], [1]],
      key: item.name,
      label: item.description,
      type: 'boolean',
    }));

    return [
      {
        fields: mappedRules.filter(item => item.key.startsWith('@typescript')),
        heading: 'Rules',
      },
      {
        fields: mappedRules.filter(item => !item.key.startsWith('@typescript')),
        heading: 'Core rules',
      },
    ];
  }, [ruleOptions]);

  const onChange = useCallback(
    (newConfig: Record<string, unknown>) => {
      const parsed = parseJSONObject(config);
      parsed.rules = newConfig;
      updateConfigObject(newConfig);
      onChangeProp({ eslintrc: toJson(parsed) });
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
  - `props: ConfigEslintProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useState (from react)`
  - `useEffect (from react)`
  - `updateConfigObject`
  - `ensureObject (from ../lib/json)`
  - `parseJSONObject (from ../lib/json)`
  - `shallowEqual (from ../lib/shallowEqual)`
  - `useMemo (from react)`
  - `ruleOptions.map`
  - `mappedRules.filter`
  - `item.key.startsWith`
  - `useCallback (from react)`
  - `onChangeProp`
  - `toJson (from ../lib/json)`

---

## Interfaces

### `ConfigEslintProps`

<details><summary>Interface Code</summary>

```ts
export interface ConfigEslintProps {
  readonly className?: string;
  readonly config?: string;
  readonly onChange: (value: Partial<ConfigModel>) => void;
  readonly ruleOptions: RuleDetails[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `className` | `string` | ✓ |  |
| `config` | `string` | ✓ |  |
| `onChange` | `(value: Partial<ConfigModel>) => void` | ✗ |  |
| `ruleOptions` | `RuleDetails[]` | ✗ |  |


---