[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Playground.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 33 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 23 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ActiveVisualEditor` | `any` | const | `!isLoading &&
    {
      code: undefined,
      eslintrc: visualEslintRc && ConfigEslint,
      tsconfig: visualTSConfig && ConfigTypeScript,
    }[activeTab]` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | className={styles.codeContainer} | <PanelGroup> |
| `PanelGroup` | component | autoSaveId="playground-size", className={styles.panelGroup}, direction={windowSize === 'mobile' ? 'vertical' : 'horizontal'} | <Panel>, <PanelResizeHandle>, <Panel>, <PanelResizeHandle>, <Panel> |
| `Panel` | component | className={styles.PanelColumn}, collapsible={true}, defaultSize={windowSize === 'mobile' ? 0 : optionsSize}, id="playgroundMenu", ref={playgroundMenuRef} | <div> |
| `div` | element | className={styles.playgroundMenu} | <OptionsSelector> |
| `OptionsSelector` | component | setState={setState}, state={state}, tsVersions={tsVersions} | *none* |
| `PanelResizeHandle` | component | className={styles.PanelResizeHandle}, style={windowSize === 'mobile' ? { display: 'none' } : {}} | *none* |
| `Panel` | component | className={styles.PanelColumn}, collapsible={true}, id="playgroundEditor" | {isLoading && <Loader />}, <EditorTabs>, {ActiveVisualEditor && (
            <ActiveVisualEditor
              className={styles.tabCode}
              config={state[activeTab]}
              onChange={setState}
              ruleOptions={ruleNames}
            />
          )}, <div>, <LoadingEditor> |
| `Loader` | component | *none* | *none* |
| `EditorTabs` | component | active={activeTab}, change={setTab}, showModal={onVisualEditor}, showVisualEditor={activeTab !== 'code'}, tabs={['code', 'tsconfig', 'eslintrc']} | *none* |
| `ActiveVisualEditor` | component | className={styles.tabCode}, config={state[activeTab]}, onChange={setState}, ruleOptions={ruleNames} | *none* |
| `div` | element | className={clsx(
              styles.tabCode,
              ActiveVisualEditor && styles.hidden,
            )}, key="monacoEditor" | <EditorEmbed> |
| `EditorEmbed` | component | *none* | *none* |
| `LoadingEditor` | component | activeTab={activeTab}, onASTChange={setAstModel}, onChange={setState}, onLoaded={onLoaded}, onMarkersChange={setMarkers}, onSelect={setPosition}, selectedRange={selectedRange} | *none* |
| `PanelResizeHandle` | component | className={styles.PanelResizeHandle} | *none* |
| `Panel` | component | className={styles.PanelColumn}, collapsible={true}, id="playgroundInfo" | <div>, <div> |
| `div` | element | *none* | <EditorTabs>, {state.showAST === 'es' && (
              <ESQueryFilter
                defaultValue={state.esQuery?.filter}
                onChange={(filter, selector) =>
                  setState({ esQuery: { filter, selector } })
                }
                onError={setEsQueryError}
              />
            )} |
| `EditorTabs` | component | active={state.showAST ?? false}, additionalTabsInfo={{
                Errors:
                  markers?.reduce((prev, cur) => prev + cur.items.length, 0) ||
                  0,
              }}, change={showAST => setState({ showAST })}, tabs={detailTabs} | *none* |
| `ESQueryFilter` | component | defaultValue={state.esQuery?.filter}, onChange={(filter, selector) =>
                  setState({ esQuery: { filter, selector } })
                }, onError={setEsQueryError} | *none* |
| `div` | element | className={styles.playgroundInfoContainer} | {state.showAST === 'es' && esQueryError ? (
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
            )} |
| `ErrorViewer` | component | title="Invalid Selector", type="warning", value={esQueryError} | *none* |
| `TypesDetails` | component | cursorPosition={position}, onHoverNode={setSelectedRange}, typeChecker={astModel.typeChecker}, value={astModel.storedTsAST} | *none* |
| `ASTViewer` | component | cursorPosition={position}, enableScrolling={state.scroll}, filter={
                    state.showAST === 'es' ? state.esQuery?.selector : undefined
                  }, key={state.showAST}, onHoverNode={setSelectedRange}, showTokens={state.showTokens}, value={
                    state.showAST === 'types'
                      ? undefined
                      : astModel[
                          `stored${({ es: 'AST', scope: 'Scope', ts: 'TsAST' } as const)[state.showAST]}` as const
                        ]
                  } | *none* |
| `ErrorsViewer` | component | value={markers} | *none* |


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