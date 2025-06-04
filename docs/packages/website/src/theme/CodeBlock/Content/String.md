[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `String.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 17 |
| 📊 Variables & Constants | 6 |
| 💠 JSX Elements | 11 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/theme/CodeBlock/Content/String.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Props` | `@theme/CodeBlock/Content/String` |
| `usePrismTheme` | `@docusaurus/theme-common` |
| `useThemeConfig` | `@docusaurus/theme-common` |
| `containsLineNumbers` | `@docusaurus/theme-common/internal` |
| `parseCodeBlockTitle` | `@docusaurus/theme-common/internal` |
| `parseLanguage` | `@docusaurus/theme-common/internal` |
| `parseLines` | `@docusaurus/theme-common/internal` |
| `useCodeWordWrap` | `@docusaurus/theme-common/internal` |
| `Container` | `@theme/CodeBlock/Container` |
| `CopyButton` | `@theme/CodeBlock/CopyButton` |
| `Line` | `@theme/CodeBlock/Line` |
| `WordWrapButton` | `@theme/CodeBlock/WordWrapButton` |
| `clsx` | `clsx` |
| `Highlight` | `prism-react-renderer` |
| `React` | `react` |
| `TryInPlayground` | `../../MDXComponents/TryInPlayground` |
| `styles` | `./styles.module.css` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `language` | `any` | const | `languageProp ?? parseLanguage(blockClassName) ?? defaultLanguage` | ✗ |
| `title` | `any` | const | `parseCodeBlockTitle(metastring) || titleProp` | ✗ |
| `showLineNumbers` | `any` | const | `showLineNumbersProp ?? containsLineNumbers(metastring)` | ✗ |
| `lastLineOfCodeLength` | `any` | const | `codeLines.at(-1)?.length ?? 0` | ✗ |
| `needsMorePadding` | `boolean` | const | `lastLineOfCodeLength > 50` | ✗ |
| `eslintrcHashRegex` | `RegExp` | const | `/eslintrcHash=(?<quote>["'])(?<eslintrcHash>.*?)\1/` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `Container` | component | as="div", className={clsx(
        blockClassName,
        language &&
          !blockClassName.includes(`language-${language}`) &&
          `language-${language}`,
      )} | {title && <div className={styles.codeBlockTitle}>{title}</div>}, <div> |
| `div` | element | className={styles.codeBlockTitle} | {title} |
| `div` | element | className={styles.codeBlockContent} | <Highlight>, {eslintrcHash && (
          <TryInPlayground
            className={clsx(
              'button button--primary button--outline',
              styles.playgroundButton,
            )}
            codeHash={lz.compressToEncodedURIComponent(copiedCode)}
            eslintrcHash={eslintrcHash}
            language={language}
          >
            Open in Playground
          </TryInPlayground>
        )}, <div> |
| `Highlight` | component | code={code}, language={language ?? 'text'}, theme={prismTheme} | {({
            className,
            getLineProps,
            getTokenProps,
            tokens,
          }): React.JSX.Element => (
            <pre
              className={clsx(className, styles.codeBlock, 'thin-scrollbar')}
              ref={wordWrap.codeBlockRef}
              // eslint-disable-next-line jsx-a11y/no-noninteractive-tabindex
              tabIndex={0}
            >
              <code
                className={clsx(
                  styles.codeBlockLines,
                  eslintrcHash &&
                    needsMorePadding &&
                    styles.codeBlockLinesMorePadding,
                  showLineNumbers && styles.codeBlockLinesWithNumbering,
                )}
              >
                {tokens.map((line, i) => (
                  <Line
                    classNames={lineClassNames[i]}
                    getLineProps={getLineProps}
                    getTokenProps={getTokenProps}
                    key={i}
                    line={line}
                    showLineNumbers={showLineNumbers}
                  />
                ))}
              </code>
            </pre>
          )} |
| `pre` | element | className={clsx(className, styles.codeBlock, 'thin-scrollbar')}, ref={wordWrap.codeBlockRef}, tabIndex={0} | <code> |
| `code` | element | className={clsx(
                  styles.codeBlockLines,
                  eslintrcHash &&
                    needsMorePadding &&
                    styles.codeBlockLinesMorePadding,
                  showLineNumbers && styles.codeBlockLinesWithNumbering,
                )} | {tokens.map((line, i) => (
                  <Line
                    classNames={lineClassNames[i]}
                    getLineProps={getLineProps}
                    getTokenProps={getTokenProps}
                    key={i}
                    line={line}
                    showLineNumbers={showLineNumbers}
                  />
                ))} |
| `Line` | component | classNames={lineClassNames[i]}, getLineProps={getLineProps}, getTokenProps={getTokenProps}, key={i}, line={line}, showLineNumbers={showLineNumbers} | *none* |
| `TryInPlayground` | component | className={clsx(
              'button button--primary button--outline',
              styles.playgroundButton,
            )}, codeHash={lz.compressToEncodedURIComponent(copiedCode)}, eslintrcHash={eslintrcHash}, language={language} | text: "Open in Playground" |
| `div` | element | className={styles.buttonGroup} | {(wordWrap.isEnabled || wordWrap.isCodeScrollable) && (
            <WordWrapButton
              className={styles.codeButton}
              isEnabled={wordWrap.isEnabled}
              onClick={(): void => wordWrap.toggle()}
            />
          )}, <CopyButton> |
| `WordWrapButton` | component | className={styles.codeButton}, isEnabled={wordWrap.isEnabled}, onClick={(): void => wordWrap.toggle()} | *none* |
| `CopyButton` | component | className={styles.codeButton}, code={copiedCode} | *none* |


---

## Functions

### `CodeBlockString({
  children,
  className: blockClassName = '',
  language: languageProp,
  metastring,
  showLineNumbers: showLineNumbersProp,
  title: titleProp,
}: Props): React.JSX.Element`

<details><summary>Code</summary>

```ts
export default function CodeBlockString({
  children,
  className: blockClassName = '',
  language: languageProp,
  metastring,
  showLineNumbers: showLineNumbersProp,
  title: titleProp,
}: Props): React.JSX.Element {
  const {
    prism: { defaultLanguage, magicComments },
  } = useThemeConfig();
  const language =
    languageProp ?? parseLanguage(blockClassName) ?? defaultLanguage;
  const prismTheme = usePrismTheme();
  const wordWrap = useCodeWordWrap();

  // We still parse the metastring in case we want to support more syntax in the
  // future. Note that MDX doesn't strip quotes when parsing metastring:
  // "title=\"xyz\"" => title: "\"xyz\""
  const title = parseCodeBlockTitle(metastring) || titleProp;

  const { code, lineClassNames } = parseLines(children, {
    language,
    magicComments,
    metastring,
  });
  const showLineNumbers =
    showLineNumbersProp ?? containsLineNumbers(metastring);

  const codeLines = code
    .split('\n')
    .filter(
      (c, i) =>
        !(lineClassNames[i] as string[] | undefined)?.includes(
          'code-block-removed-line',
        ),
    );
  const copiedCode = codeLines.join('\n');
  const lastLineOfCodeLength = codeLines.at(-1)?.length ?? 0;
  const needsMorePadding = lastLineOfCodeLength > 50;

  const eslintrcHash = parseEslintrc(metastring);

  return (
    <Container
      as="div"
      className={clsx(
        blockClassName,
        language &&
          !blockClassName.includes(`language-${language}`) &&
          `language-${language}`,
      )}
    >
      {title && <div className={styles.codeBlockTitle}>{title}</div>}
      <div className={styles.codeBlockContent}>
        <Highlight code={code} language={language ?? 'text'} theme={prismTheme}>
          {({
            className,
            getLineProps,
            getTokenProps,
            tokens,
          }): React.JSX.Element => (
            <pre
              className={clsx(className, styles.codeBlock, 'thin-scrollbar')}
              ref={wordWrap.codeBlockRef}
              // eslint-disable-next-line jsx-a11y/no-noninteractive-tabindex
              tabIndex={0}
            >
              <code
                className={clsx(
                  styles.codeBlockLines,
                  eslintrcHash &&
                    needsMorePadding &&
                    styles.codeBlockLinesMorePadding,
                  showLineNumbers && styles.codeBlockLinesWithNumbering,
                )}
              >
                {tokens.map((line, i) => (
                  <Line
                    classNames={lineClassNames[i]}
                    getLineProps={getLineProps}
                    getTokenProps={getTokenProps}
                    key={i}
                    line={line}
                    showLineNumbers={showLineNumbers}
                  />
                ))}
              </code>
            </pre>
          )}
        </Highlight>
        {eslintrcHash && (
          <TryInPlayground
            className={clsx(
              'button button--primary button--outline',
              styles.playgroundButton,
            )}
            codeHash={lz.compressToEncodedURIComponent(copiedCode)}
            eslintrcHash={eslintrcHash}
            language={language}
          >
            Open in Playground
          </TryInPlayground>
        )}
        <div className={styles.buttonGroup}>
          {(wordWrap.isEnabled || wordWrap.isCodeScrollable) && (
            <WordWrapButton
              className={styles.codeButton}
              isEnabled={wordWrap.isEnabled}
              onClick={(): void => wordWrap.toggle()}
            />
          )}
          <CopyButton className={styles.codeButton} code={copiedCode} />
        </div>
      </div>
    </Container>
  );
}
```
</details>

- **Parameters**:
  - `{
  children,
  className: blockClassName = '',
  language: languageProp,
  metastring,
  showLineNumbers: showLineNumbersProp,
  title: titleProp,
}: Props`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useThemeConfig (from @docusaurus/theme-common)`
  - `parseLanguage (from @docusaurus/theme-common/internal)`
  - `usePrismTheme (from @docusaurus/theme-common)`
  - `useCodeWordWrap (from @docusaurus/theme-common/internal)`
  - `parseCodeBlockTitle (from @docusaurus/theme-common/internal)`
  - `parseLines (from @docusaurus/theme-common/internal)`
  - `containsLineNumbers (from @docusaurus/theme-common/internal)`
  - `code
    .split('\n')
    .filter`
  - `(lineClassNames[i] as string[] | undefined)?.includes`
  - `codeLines.join`
  - `codeLines.at`
  - `parseEslintrc`
  - `clsx (from clsx)`
  - `blockClassName.includes`
  - `tokens.map`
  - `lz.compressToEncodedURIComponent`
  - `wordWrap.toggle`
- **Internal Comments**:
```
// We still parse the metastring in case we want to support more syntax in the (x2)
// future. Note that MDX doesn't strip quotes when parsing metastring: (x2)
// "title=\"xyz\"" => title: "\"xyz\"" (x2)
// eslint-disable-next-line jsx-a11y/no-noninteractive-tabindex (x2)
```

### `parseEslintrc(metastring: string): string`

<details><summary>Code</summary>

```ts
function parseEslintrc(metastring?: string): string {
  return metastring?.match(eslintrcHashRegex)?.groups?.eslintrcHash ?? '';
}
```
</details>

- **Parameters**:
  - `metastring: string`
- **Return Type**: `string`
- **Calls**:
  - `metastring?.match`

---