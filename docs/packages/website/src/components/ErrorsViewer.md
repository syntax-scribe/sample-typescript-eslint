[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ErrorsViewer.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 5 |
| 🧱 Classes | 0 |
| 📦 Imports | 12 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 26 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 4 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/ErrorsViewer.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Monaco` | `monaco-editor` |
| `Link` | `@docusaurus/Link` |
| `IconExternalLink` | `@theme/Icon/ExternalLink` |
| `clsx` | `clsx` |
| `useEffect` | `react` |
| `useState` | `react` |
| `React` | `react` |
| `AlertBlockProps` | `./layout/AlertBlock` |
| `ErrorGroup` | `./types` |
| `ErrorItem` | `./types` |
| `styles` | `./ErrorsViewer.module.css` |
| `AlertBlock` | `./layout/AlertBlock` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `button` | element | className="button button--primary button--sm", disabled={props.disabled}, onClick={(): void => {
        props.fix();
        props.setIsLocked(true);
      }} | {props.children} |
| `AlertBlock` | component | type={severityClass(item.severity)} | <div>, {item.suggestions.length > 0 && (
        <div>
          {item.suggestions.map((fixer, index) => (
            <div
              className={clsx(styles.fixerContainer, styles.fixer)}
              key={index}
            >
              <span>&gt; {fixer.message}</span>
              <FixButton
                disabled={isLocked}
                fix={fixer.fix}
                setIsLocked={setIsLocked}
              >
                apply suggestion
              </FixButton>
            </div>
          ))}
        </div>
      )} |
| `div` | element | className={clsx(!!item.fixer && styles.fixerContainer)} | <pre>, {item.fixer && (
          <FixButton
            disabled={isLocked}
            fix={item.fixer.fix}
            setIsLocked={setIsLocked}
          >
            apply fix
          </FixButton>
        )} |
| `pre` | element | className={styles.errorPre} | {item.message}, {item.location} |
| `FixButton` | component | disabled={isLocked}, fix={item.fixer.fix}, setIsLocked={setIsLocked} | text: "apply fix" |
| `div` | element | *none* | {item.suggestions.map((fixer, index) => (
            <div
              className={clsx(styles.fixerContainer, styles.fixer)}
              key={index}
            >
              <span>&gt; {fixer.message}</span>
              <FixButton
                disabled={isLocked}
                fix={fixer.fix}
                setIsLocked={setIsLocked}
              >
                apply suggestion
              </FixButton>
            </div>
          ))} |
| `div` | element | className={clsx(styles.fixerContainer, styles.fixer)}, key={index} | <span>, <FixButton> |
| `span` | element | *none* | text: "&gt;", {fixer.message} |
| `FixButton` | component | disabled={isLocked}, fix={fixer.fix}, setIsLocked={setIsLocked} | text: "apply suggestion" |
| `div` | element | className={styles.list} | <div> |
| `div` | element | className="margin-top--md" | <AlertBlock> |
| `AlertBlock` | component | type={type} | <div>, <pre> |
| `div` | element | className={styles.fixerContainer} | <h4> |
| `h4` | element | *none* | {title} |
| `pre` | element | className={styles.errorPre} | {type === 'danger' ? value.stack : value.message} |
| `div` | element | className={styles.list} | {value?.length ? (
        value.map(({ group, items, uri }) => {
          return (
            <div className="margin-top--md" key={group}>
              <h4>
                {group}
                {uri && (
                  <>
                    {' - '}
                    <Link href={uri} target="_blank">
                      docs <IconExternalLink height={13.5} width={13.5} />
                    </Link>
                  </>
                )}
              </h4>
              {items.map((item, index) => (
                <div className="margin-bottom--sm" key={index}>
                  <ErrorBlock
                    isLocked={isLocked}
                    item={item}
                    setIsLocked={setIsLocked}
                  />
                </div>
              ))}
            </div>
          );
        })
      ) : (
        <div className="margin-top--md">
          <AlertBlock type="success">
            <div>All is ok!</div>
          </AlertBlock>
        </div>
      )} |
| `div` | element | className="margin-top--md", key={group} | <h4>, {items.map((item, index) => (
                <div className="margin-bottom--sm" key={index}>
                  <ErrorBlock
                    isLocked={isLocked}
                    item={item}
                    setIsLocked={setIsLocked}
                  />
                </div>
              ))} |
| `h4` | element | *none* | {group}, {uri && (
                  <>
                    {' - '}
                    <Link href={uri} target="_blank">
                      docs <IconExternalLink height={13.5} width={13.5} />
                    </Link>
                  </>
                )} |
| `Fragment` | fragment | *none* | <Link> |
| `Link` | component | href={uri}, target="_blank" | text: "docs", <IconExternalLink> |
| `IconExternalLink` | component | height={13.5}, width={13.5} | *none* |
| `div` | element | className="margin-bottom--sm", key={index} | <ErrorBlock> |
| `ErrorBlock` | component | isLocked={isLocked}, item={item}, setIsLocked={setIsLocked} | *none* |
| `div` | element | className="margin-top--md" | <AlertBlock> |
| `AlertBlock` | component | type="success" | <div> |
| `div` | element | *none* | text: "All is ok!" |


---

## Functions

### `severityClass(severity: Monaco.MarkerSeverity): AlertBlockProps['type']`

<details><summary>Code</summary>

```ts
function severityClass(
  severity: Monaco.MarkerSeverity,
): AlertBlockProps['type'] {
  switch (severity) {
    /* eslint-disable @typescript-eslint/no-unsafe-enum-comparison -- Monaco is imported as a type */
    case 2:
      return 'note';
    case 4:
      return 'warning';
    case 8:
      return 'danger';
    /* eslint-enable @typescript-eslint/no-unsafe-enum-comparison */
  }
  return 'info';
}
```
</details>

- **Parameters**:
  - `severity: Monaco.MarkerSeverity`
- **Return Type**: `AlertBlockProps['type']`
- **Internal Comments**:
```
/* eslint-disable @typescript-eslint/no-unsafe-enum-comparison -- Monaco is imported as a type */
```

### `FixButton(props: FixButtonProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function FixButton(props: FixButtonProps): React.JSX.Element {
  return (
    <button
      className="button button--primary button--sm"
      disabled={props.disabled}
      onClick={(): void => {
        props.fix();
        props.setIsLocked(true);
      }}
    >
      {props.children}
    </button>
  );
}
```
</details>

- **Parameters**:
  - `props: FixButtonProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `props.fix`
  - `props.setIsLocked`
### `ErrorBlock({
  isLocked,
  item,
  setIsLocked,
}: ErrorBlockProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function ErrorBlock({
  isLocked,
  item,
  setIsLocked,
}: ErrorBlockProps): React.JSX.Element {
  return (
    <AlertBlock type={severityClass(item.severity)}>
      <div className={clsx(!!item.fixer && styles.fixerContainer)}>
        <pre className={styles.errorPre}>
          {item.message} {item.location}
        </pre>
        {item.fixer && (
          <FixButton
            disabled={isLocked}
            fix={item.fixer.fix}
            setIsLocked={setIsLocked}
          >
            apply fix
          </FixButton>
        )}
      </div>
      {item.suggestions.length > 0 && (
        <div>
          {item.suggestions.map((fixer, index) => (
            <div
              className={clsx(styles.fixerContainer, styles.fixer)}
              key={index}
            >
              <span>&gt; {fixer.message}</span>
              <FixButton
                disabled={isLocked}
                fix={fixer.fix}
                setIsLocked={setIsLocked}
              >
                apply suggestion
              </FixButton>
            </div>
          ))}
        </div>
      )}
    </AlertBlock>
  );
}
```
</details>

- **Parameters**:
  - `{
  isLocked,
  item,
  setIsLocked,
}: ErrorBlockProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `severityClass`
  - `clsx (from clsx)`
  - `item.suggestions.map`
### `ErrorViewer({
  title,
  type,
  value,
}: ErrorViewerProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function ErrorViewer({
  title,
  type,
  value,
}: ErrorViewerProps): React.JSX.Element {
  return (
    <div className={styles.list}>
      <div className="margin-top--md">
        <AlertBlock type={type}>
          <div className={styles.fixerContainer}>
            <h4>{title}</h4>
          </div>
          <pre className={styles.errorPre}>
            {type === 'danger' ? value.stack : value.message}
          </pre>
        </AlertBlock>
      </div>
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  title,
  type,
  value,
}: ErrorViewerProps`
- **Return Type**: `React.JSX.Element`
### `ErrorsViewer({ value }: ErrorsViewerProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function ErrorsViewer({ value }: ErrorsViewerProps): React.JSX.Element {
  const [isLocked, setIsLocked] = useState(false);

  useEffect(() => {
    setIsLocked(false);
  }, [value]);

  return (
    <div className={styles.list}>
      {value?.length ? (
        value.map(({ group, items, uri }) => {
          return (
            <div className="margin-top--md" key={group}>
              <h4>
                {group}
                {uri && (
                  <>
                    {' - '}
                    <Link href={uri} target="_blank">
                      docs <IconExternalLink height={13.5} width={13.5} />
                    </Link>
                  </>
                )}
              </h4>
              {items.map((item, index) => (
                <div className="margin-bottom--sm" key={index}>
                  <ErrorBlock
                    isLocked={isLocked}
                    item={item}
                    setIsLocked={setIsLocked}
                  />
                </div>
              ))}
            </div>
          );
        })
      ) : (
        <div className="margin-top--md">
          <AlertBlock type="success">
            <div>All is ok!</div>
          </AlertBlock>
        </div>
      )}
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{ value }: ErrorsViewerProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useState (from react)`
  - `useEffect (from react)`
  - `setIsLocked`
  - `value.map`
  - `items.map`

---

## Interfaces

### `ErrorsViewerProps`

<details><summary>Interface Code</summary>

```ts
export interface ErrorsViewerProps {
  readonly value?: ErrorGroup[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `value` | `ErrorGroup[]` | ✓ |  |

### `ErrorViewerProps`

<details><summary>Interface Code</summary>

```ts
export interface ErrorViewerProps {
  readonly title: string;
  readonly type: AlertBlockProps['type'];
  readonly value: Error;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `title` | `string` | ✗ |  |
| `type` | `AlertBlockProps['type']` | ✗ |  |
| `value` | `Error` | ✗ |  |

### `ErrorBlockProps`

<details><summary>Interface Code</summary>

```ts
export interface ErrorBlockProps {
  readonly isLocked: boolean;
  readonly item: ErrorItem;
  readonly setIsLocked: (value: boolean) => void;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `isLocked` | `boolean` | ✗ |  |
| `item` | `ErrorItem` | ✗ |  |
| `setIsLocked` | `(value: boolean) => void` | ✗ |  |

### `FixButtonProps`

<details><summary>Interface Code</summary>

```ts
export interface FixButtonProps {
  readonly children?: React.ReactNode;
  readonly disabled: boolean;
  readonly fix: () => void;
  readonly setIsLocked: (value: boolean) => void;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `children` | `React.ReactNode` | ✓ |  |
| `disabled` | `boolean` | ✗ |  |
| `fix` | `() => void` | ✗ |  |
| `setIsLocked` | `(value: boolean) => void` | ✗ |  |


---