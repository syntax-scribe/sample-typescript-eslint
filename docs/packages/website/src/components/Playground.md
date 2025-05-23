[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Playground.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 33
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/Playground.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ImperativePanelHandle` | `react-resizable-panels` |
| `useWindowSize` | `@docusaurus/theme-common` |
| `clsx` | `clsx` |
| `useCallback` | `react` |
| `useEffect` | `react` |
| `useMemo` | `react` |
| `useRef` | `react` |
| `useState` | `react` |
| `React` | `react` |
| `Panel` | `react-resizable-panels` |
| `PanelGroup` | `react-resizable-panels` |
| `PanelResizeHandle` | `react-resizable-panels` |
| `UpdateModel` | `./linter/types` |
| `ErrorGroup` | `./types` |
| `RuleDetails` | `./types` |
| `SelectedRange` | `./types` |
| `TabType` | `./types` |
| `ASTViewer` | `./ast/ASTViewer` |
| `ConfigEslint` | `./config/ConfigEslint` |
| `ConfigTypeScript` | `./config/ConfigTypeScript` |
| `EditorEmbed` | `./editor/EditorEmbed` |
| `LoadingEditor` | `./editor/LoadingEditor` |
| `ErrorsViewer` | `./ErrorsViewer` |
| `ErrorViewer` | `./ErrorsViewer` |
| `ESQueryFilter` | `./ESQueryFilter` |
| `useHashState` | `./hooks/useHashState` |
| `EditorTabs` | `./layout/EditorTabs` |
| `Loader` | `./layout/Loader` |
| `defaultConfig` | `./options` |
| `detailTabs` | `./options` |
| `OptionsSelector` | `./OptionsSelector` |
| `styles` | `./Playground.module.css` |
| `TypesDetails` | `./typeDetails/TypesDetails` |


---

## Functions

### `Playground(): React.JSX.Element`

<details><summary>Code</summary>

```ts
function Playground(): React.JSX.Element {
  const windowSize = useWindowSize();
  const [state, setState] = useHashState(defaultConfig);
  const [astModel, setAstModel] = useState<UpdateModel>();
  const [markers, setMarkers] = useState<ErrorGroup[]>();
  const [ruleNames, setRuleNames] = useState<RuleDetails[]>([]);
  const [isLoading, setIsLoading] = useState(true);
  const [tsVersions, setTSVersion] = useState<readonly string[]>([]);
  const [selectedRange, setSelectedRange] = useState<SelectedRange>();
  const [position, setPosition] = useState<number>();
  const [activeTab, setTab] = useState<TabType>('code');
  const [esQueryError, setEsQueryError] = useState<Error>();
  const [visualEslintRc, setVisualEslintRc] = useState(false);
  const [visualTSConfig, setVisualTSConfig] = useState(false);
  const playgroundMenuRef = useRef<ImperativePanelHandle>(null);
  const optionsSize = useMemo(
    () =>
      Math.round(
        (parseFloat(getComputedStyle(document.documentElement).fontSize) *
          2000) /
          innerWidth,
      ),
    [],
  );

  const onLoaded = useCallback(
    (ruleNames: RuleDetails[], tsVersions: readonly string[]) => {
      setRuleNames(ruleNames);
      setTSVersion(tsVersions);
      setIsLoading(false);
    },
    [],
  );

  const ActiveVisualEditor =
    !isLoading &&
    {
      code: undefined,
      eslintrc: visualEslintRc && ConfigEslint,
      tsconfig: visualTSConfig && ConfigTypeScript,
    }[activeTab];

  const onVisualEditor = useCallback((tab: TabType) => {
    if (tab === 'tsconfig') {
      setVisualTSConfig(val => !val);
    } else if (tab === 'eslintrc') {
      setVisualEslintRc(val => !val);
    }
  }, []);

  useEffect(() => {
    if (windowSize === 'mobile') {
      playgroundMenuRef.current?.collapse();
    } else if (windowSize === 'desktop') {
      playgroundMenuRef.current?.expand();
    }
  }, [windowSize]);

  return (
    <div className={styles.codeContainer}>
      <PanelGroup
        autoSaveId="playground-size"
        className={styles.panelGroup}
        direction={windowSize === 'mobile' ? 'vertical' : 'horizontal'}
      >
        <Panel
          className={styles.PanelColumn}
          collapsible={true}
          defaultSize={windowSize === 'mobile' ? 0 : optionsSize}
          id="playgroundMenu"
          ref={playgroundMenuRef}
        >
          <div className={styles.playgroundMenu}>
            <OptionsSelector
              setState={setState}
              state={state}
              tsVersions={tsVersions}
            />
          </div>
        </Panel>
        <PanelResizeHandle
          className={styles.PanelResizeHandle}
          style={windowSize === 'mobile' ? { display: 'none' } : {}}
        />
        <Panel
          className={styles.PanelColumn}
          collapsible={true}
          id="playgroundEditor"
        >
          {isLoading && <Loader />}
          <EditorTabs
            active={activeTab}
            change={setTab}
            showModal={onVisualEditor}
            showVisualEditor={activeTab !== 'code'}
            tabs={['code', 'tsconfig', 'eslintrc']}
          />
          {ActiveVisualEditor && (
            <ActiveVisualEditor
              className={styles.tabCode}
              config={state[activeTab]}
              onChange={setState}
              ruleOptions={ruleNames}
            />
          )}
          <div
            className={clsx(
              styles.tabCode,
              ActiveVisualEditor && styles.hidden,
            )}
            key="monacoEditor"
          >
            <EditorEmbed />
          </div>
          <LoadingEditor
            {...state}
            activeTab={activeTab}
            onASTChange={setAstModel}
            onChange={setState}
            onLoaded={onLoaded}
            onMarkersChange={setMarkers}
            onSelect={setPosition}
            selectedRange={selectedRange}
          />
        </Panel>
        <PanelResizeHandle className={styles.PanelResizeHandle} />
        <Panel
          className={styles.PanelColumn}
          collapsible={true}
          id="playgroundInfo"
        >
          <div>
            <EditorTabs
              active={state.showAST ?? false}
              additionalTabsInfo={{
                Errors:
                  markers?.reduce((prev, cur) => prev + cur.items.length, 0) ||
                  0,
              }}
              change={showAST => setState({ showAST })}
              tabs={detailTabs}
            />
            {state.showAST === 'es' && (
              <ESQueryFilter
                defaultValue={state.esQuery?.filter}
                onChange={(filter, selector) =>
                  setState({ esQuery: { filter, selector } })
                }
                onError={setEsQueryError}
              />
            )}
          </div>
          <div className={styles.playgroundInfoContainer}>
            {state.showAST === 'es' && esQueryError ? (
              <ErrorViewer
                title="Invalid Selector"
                type="warning"
                value={esQueryError}
              />
            ) : state.showAST && astModel ? (
              state.showAST === 'types' && astModel.storedTsAST ? (
                <TypesDetails
                  cursorPosition={position}
                  onHoverNode={setSelectedRange}
                  typeChecker={astModel.typeChecker}
                  value={astModel.storedTsAST}
                />
              ) : (
                <ASTViewer
                  cursorPosition={position}
                  enableScrolling={state.scroll}
                  filter={
                    state.showAST === 'es' ? state.esQuery?.selector : undefined
                  }
                  key={state.showAST}
                  onHoverNode={setSelectedRange}
                  showTokens={state.showTokens}
                  value={
                    state.showAST === 'types'
                      ? undefined
                      : astModel[
                          `stored${({ es: 'AST', scope: 'Scope', ts: 'TsAST' } as const)[state.showAST]}` as const
                        ]
                  }
                />
              )
            ) : (
              <ErrorsViewer value={markers} />
            )}
          </div>
        </Panel>
      </PanelGroup>
    </div>
  );
}
```
</details>

- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useWindowSize (from @docusaurus/theme-common)`
  - `useHashState (from ./hooks/useHashState)`
  - `useState (from react)`
  - `useRef (from react)`
  - `useMemo (from react)`
  - `Math.round`
  - `parseFloat`
  - `getComputedStyle`
  - `useCallback (from react)`
  - `setRuleNames`
  - `setTSVersion`
  - `setIsLoading`
  - `setVisualTSConfig`
  - `setVisualEslintRc`
  - `useEffect (from react)`
  - `playgroundMenuRef.current?.collapse`
  - `playgroundMenuRef.current?.expand`
  - `clsx (from clsx)`
  - `markers?.reduce`
  - `setState`

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