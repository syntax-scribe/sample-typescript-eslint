[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `OptionsSelector.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 20 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 28 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/OptionsSelector.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `NavbarSecondaryMenuFiller` | `@docusaurus/theme-common` |
| `useWindowSize` | `@docusaurus/theme-common` |
| `CopyIcon` | `@theme/Icon/Copy` |
| `IconExternalLink` | `@theme/Icon/ExternalLink` |
| `SuccessIcon` | `@theme/Icon/Success` |
| `useCallback` | `react` |
| `useMemo` | `react` |
| `React` | `react` |
| `semverSatisfies` | `semver/functions/satisfies` |
| `ConfigModel` | `./types` |
| `useClipboard` | `../hooks/useClipboard` |
| `Checkbox` | `./inputs/Checkbox` |
| `Dropdown` | `./inputs/Dropdown` |
| `Tooltip` | `./inputs/Tooltip` |
| `ActionLabel` | `./layout/ActionLabel` |
| `Expander` | `./layout/Expander` |
| `InputLabel` | `./layout/InputLabel` |
| `createMarkdown` | `./lib/markdown` |
| `createMarkdownParams` | `./lib/markdown` |
| `fileTypes` | `./options` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `MIN_TS_VERSION_SEMVER` | `">=4.7.4"` | const | `'>=4.7.4'` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `Fragment` | fragment | *none* | <Expander>, <Expander>, <Expander> |
| `Expander` | component | label="Info" | <InputLabel>, <InputLabel>, <InputLabel> |
| `InputLabel` | component | name="TypeScript" | <Dropdown> |
| `Dropdown` | component | className="text--right", disabled={!tsVersionsFiltered.length}, name="ts", onChange={(ts): void => setState({ ts })}, options={
              tsVersionsFiltered.length ? tsVersionsFiltered : [state.ts]
            }, value={state.ts} | *none* |
| `InputLabel` | component | name="Eslint" | {process.env.ESLINT_VERSION} |
| `InputLabel` | component | name="TSESlint" | {process.env.TS_ESLINT_VERSION} |
| `Expander` | component | label="Options" | <InputLabel>, <InputLabel>, <InputLabel>, <InputLabel> |
| `InputLabel` | component | name="File type" | <Dropdown> |
| `Dropdown` | component | name="fileType", onChange={(fileType): void => setState({ fileType })}, options={fileTypes}, value={state.fileType} | *none* |
| `InputLabel` | component | name="Source type" | <Dropdown> |
| `Dropdown` | component | name="sourceType", onChange={(sourceType): void => setState({ sourceType })}, options={['script', 'module']}, value={state.sourceType} | *none* |
| `InputLabel` | component | name="Auto scroll" | <Checkbox> |
| `Checkbox` | component | checked={state.scroll}, name="enableScrolling", onChange={(scroll): void => setState({ scroll })} | *none* |
| `InputLabel` | component | name="Show tokens" | <Checkbox> |
| `Checkbox` | component | checked={state.showTokens}, name="showTokens", onChange={(showTokens): void => setState({ showTokens })} | *none* |
| `Expander` | component | label="Actions" | <ActionLabel>, <ActionLabel>, <ActionLabel> |
| `ActionLabel` | component | name="Copy link", onClick={copyLinkToClipboard} | <Tooltip> |
| `Tooltip` | component | open={copyLink}, text="Copied" | {copyLink ? (
              <SuccessIcon height="13.5" width="13.5" />
            ) : (
              <CopyIcon height="13.5" width="13.5" />
            )} |
| `SuccessIcon` | component | height="13.5", width="13.5" | *none* |
| `CopyIcon` | component | height="13.5", width="13.5" | *none* |
| `ActionLabel` | component | name="Copy Markdown", onClick={copyMarkdownToClipboard} | <Tooltip> |
| `Tooltip` | component | open={copyMarkdown}, text="Copied" | {copyMarkdown ? (
              <SuccessIcon height="13.5" width="13.5" />
            ) : (
              <CopyIcon height="13.5" width="13.5" />
            )} |
| `SuccessIcon` | component | height="13.5", width="13.5" | *none* |
| `CopyIcon` | component | height="13.5", width="13.5" | *none* |
| `ActionLabel` | component | name="Report as Issue", onClick={openIssue} | <IconExternalLink> |
| `IconExternalLink` | component | height="13.5", width="13.5" | *none* |
| `NavbarSecondaryMenuFiller` | component | component={OptionsSelectorContent}, props={props} | *none* |
| `OptionsSelectorContent` | component | *none* | *none* |


---

## Functions

### `OptionsSelectorContent({
  setState,
  state,
  tsVersions,
}: OptionsSelectorParams): React.JSX.Element`

<details><summary>Code</summary>

```ts
function OptionsSelectorContent({
  setState,
  state,
  tsVersions,
}: OptionsSelectorParams): React.JSX.Element {
  const [copyLink, copyLinkToClipboard] = useClipboard(() =>
    document.location.toString(),
  );
  const [copyMarkdown, copyMarkdownToClipboard] = useClipboard(() =>
    createMarkdown(state),
  );

  const openIssue = useCallback(() => {
    const params = createMarkdownParams(state);

    window
      .open(
        `https://github.com/typescript-eslint/typescript-eslint/issues/new?${params}`,
        '_blank',
      )
      ?.focus();
  }, [state]);

  const tsVersionsFiltered = useMemo(
    () =>
      tsVersions.filter(version =>
        semverSatisfies(version, MIN_TS_VERSION_SEMVER),
      ),
    [tsVersions],
  );

  return (
    <>
      <Expander label="Info">
        <InputLabel name="TypeScript">
          <Dropdown
            className="text--right"
            disabled={!tsVersionsFiltered.length}
            name="ts"
            onChange={(ts): void => setState({ ts })}
            options={
              tsVersionsFiltered.length ? tsVersionsFiltered : [state.ts]
            }
            value={state.ts}
          />
        </InputLabel>
        <InputLabel name="Eslint">{process.env.ESLINT_VERSION}</InputLabel>
        <InputLabel name="TSESlint">{process.env.TS_ESLINT_VERSION}</InputLabel>
      </Expander>
      <Expander label="Options">
        <InputLabel name="File type">
          <Dropdown
            name="fileType"
            onChange={(fileType): void => setState({ fileType })}
            options={fileTypes}
            value={state.fileType}
          />
        </InputLabel>
        <InputLabel name="Source type">
          <Dropdown
            name="sourceType"
            onChange={(sourceType): void => setState({ sourceType })}
            options={['script', 'module']}
            value={state.sourceType}
          />
        </InputLabel>
        <InputLabel name="Auto scroll">
          <Checkbox
            checked={state.scroll}
            name="enableScrolling"
            onChange={(scroll): void => setState({ scroll })}
          />
        </InputLabel>
        <InputLabel name="Show tokens">
          <Checkbox
            checked={state.showTokens}
            name="showTokens"
            onChange={(showTokens): void => setState({ showTokens })}
          />
        </InputLabel>
      </Expander>
      <Expander label="Actions">
        <ActionLabel name="Copy link" onClick={copyLinkToClipboard}>
          <Tooltip open={copyLink} text="Copied">
            {copyLink ? (
              <SuccessIcon height="13.5" width="13.5" />
            ) : (
              <CopyIcon height="13.5" width="13.5" />
            )}
          </Tooltip>
        </ActionLabel>
        <ActionLabel name="Copy Markdown" onClick={copyMarkdownToClipboard}>
          <Tooltip open={copyMarkdown} text="Copied">
            {copyMarkdown ? (
              <SuccessIcon height="13.5" width="13.5" />
            ) : (
              <CopyIcon height="13.5" width="13.5" />
            )}
          </Tooltip>
        </ActionLabel>
        <ActionLabel name="Report as Issue" onClick={openIssue}>
          <IconExternalLink height="13.5" width="13.5" />
        </ActionLabel>
      </Expander>
    </>
  );
}
```
</details>

- **Parameters**:
  - `{
  setState,
  state,
  tsVersions,
}: OptionsSelectorParams`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useClipboard (from ../hooks/useClipboard)`
  - `document.location.toString`
  - `createMarkdown (from ./lib/markdown)`
  - `useCallback (from react)`
  - `createMarkdownParams (from ./lib/markdown)`
  - `window
      .open(
        `https://github.com/typescript-eslint/typescript-eslint/issues/new?${params}`,
        '_blank',
      )
      ?.focus`
  - `useMemo (from react)`
  - `tsVersions.filter`
  - `semverSatisfies (from semver/functions/satisfies)`
  - `setState`
### `OptionsSelector(props: OptionsSelectorParams): React.JSX.Element`

<details><summary>Code</summary>

```ts
function OptionsSelector(props: OptionsSelectorParams): React.JSX.Element {
  const windowSize = useWindowSize();
  if (windowSize === 'mobile') {
    return (
      <NavbarSecondaryMenuFiller
        component={OptionsSelectorContent}
        props={props}
      />
    );
  }
  return <OptionsSelectorContent {...props} />;
}
```
</details>

- **Parameters**:
  - `props: OptionsSelectorParams`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useWindowSize (from @docusaurus/theme-common)`

---

## Interfaces

### `OptionsSelectorParams`

<details><summary>Interface Code</summary>

```ts
export interface OptionsSelectorParams {
  readonly setState: (cfg: Partial<ConfigModel>) => void;
  readonly state: ConfigModel;
  readonly tsVersions: readonly string[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `setState` | `(cfg: Partial<ConfigModel>) => void` | ✗ |  |
| `state` | `ConfigModel` | ✗ |  |
| `tsVersions` | `readonly string[]` | ✗ |  |


---