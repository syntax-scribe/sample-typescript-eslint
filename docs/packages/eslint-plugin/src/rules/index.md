[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `index.ts`

## 📚 Table of Contents

- [Imports](#imports)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 132
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/index.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Linter` | `@typescript-eslint/utils/ts-eslint` |
| `adjacentOverloadSignatures` | `./adjacent-overload-signatures` |
| `arrayType` | `./array-type` |
| `awaitThenable` | `./await-thenable` |
| `banTsComment` | `./ban-ts-comment` |
| `banTslintComment` | `./ban-tslint-comment` |
| `classLiteralPropertyStyle` | `./class-literal-property-style` |
| `classMethodsUseThis` | `./class-methods-use-this` |
| `consistentGenericConstructors` | `./consistent-generic-constructors` |
| `consistentIndexedObjectStyle` | `./consistent-indexed-object-style` |
| `consistentReturn` | `./consistent-return` |
| `consistentTypeAssertions` | `./consistent-type-assertions` |
| `consistentTypeDefinitions` | `./consistent-type-definitions` |
| `consistentTypeExports` | `./consistent-type-exports` |
| `consistentTypeImports` | `./consistent-type-imports` |
| `defaultParamLast` | `./default-param-last` |
| `dotNotation` | `./dot-notation` |
| `explicitFunctionReturnType` | `./explicit-function-return-type` |
| `explicitMemberAccessibility` | `./explicit-member-accessibility` |
| `explicitModuleBoundaryTypes` | `./explicit-module-boundary-types` |
| `initDeclarations` | `./init-declarations` |
| `maxParams` | `./max-params` |
| `memberOrdering` | `./member-ordering` |
| `methodSignatureStyle` | `./method-signature-style` |
| `namingConvention` | `./naming-convention` |
| `noArrayConstructor` | `./no-array-constructor` |
| `noArrayDelete` | `./no-array-delete` |
| `noBaseToString` | `./no-base-to-string` |
| `confusingNonNullAssertionLikeNotEqual` | `./no-confusing-non-null-assertion` |
| `noConfusingVoidExpression` | `./no-confusing-void-expression` |
| `noDeprecated` | `./no-deprecated` |
| `noDupeClassMembers` | `./no-dupe-class-members` |
| `noDuplicateEnumValues` | `./no-duplicate-enum-values` |
| `noDuplicateTypeConstituents` | `./no-duplicate-type-constituents` |
| `noDynamicDelete` | `./no-dynamic-delete` |
| `noEmptyFunction` | `./no-empty-function` |
| `noEmptyInterface` | `./no-empty-interface` |
| `noEmptyObjectType` | `./no-empty-object-type` |
| `noExplicitAny` | `./no-explicit-any` |
| `noExtraNonNullAssertion` | `./no-extra-non-null-assertion` |
| `noExtraneousClass` | `./no-extraneous-class` |
| `noFloatingPromises` | `./no-floating-promises` |
| `noForInArray` | `./no-for-in-array` |
| `noImpliedEval` | `./no-implied-eval` |
| `noImportTypeSideEffects` | `./no-import-type-side-effects` |
| `noInferrableTypes` | `./no-inferrable-types` |
| `noInvalidThis` | `./no-invalid-this` |
| `noInvalidVoidType` | `./no-invalid-void-type` |
| `noLoopFunc` | `./no-loop-func` |
| `noLossOfPrecision` | `./no-loss-of-precision` |
| `noMagicNumbers` | `./no-magic-numbers` |
| `noMeaninglessVoidOperator` | `./no-meaningless-void-operator` |
| `noMisusedNew` | `./no-misused-new` |
| `noMisusedPromises` | `./no-misused-promises` |
| `noMisusedSpread` | `./no-misused-spread` |
| `noMixedEnums` | `./no-mixed-enums` |
| `noNamespace` | `./no-namespace` |
| `noNonNullAssertedNullishCoalescing` | `./no-non-null-asserted-nullish-coalescing` |
| `noNonNullAssertedOptionalChain` | `./no-non-null-asserted-optional-chain` |
| `noNonNullAssertion` | `./no-non-null-assertion` |
| `noRedeclare` | `./no-redeclare` |
| `noRedundantTypeConstituents` | `./no-redundant-type-constituents` |
| `noRequireImports` | `./no-require-imports` |
| `noRestrictedImports` | `./no-restricted-imports` |
| `noRestrictedTypes` | `./no-restricted-types` |
| `noShadow` | `./no-shadow` |
| `noThisAlias` | `./no-this-alias` |
| `noTypeAlias` | `./no-type-alias` |
| `noUnnecessaryBooleanLiteralCompare` | `./no-unnecessary-boolean-literal-compare` |
| `noUnnecessaryCondition` | `./no-unnecessary-condition` |
| `noUnnecessaryParameterPropertyAssignment` | `./no-unnecessary-parameter-property-assignment` |
| `noUnnecessaryQualifier` | `./no-unnecessary-qualifier` |
| `noUnnecessaryTemplateExpression` | `./no-unnecessary-template-expression` |
| `noUnnecessaryTypeArguments` | `./no-unnecessary-type-arguments` |
| `noUnnecessaryTypeAssertion` | `./no-unnecessary-type-assertion` |
| `noUnnecessaryTypeConstraint` | `./no-unnecessary-type-constraint` |
| `noUnnecessaryTypeConversion` | `./no-unnecessary-type-conversion` |
| `noUnnecessaryTypeParameters` | `./no-unnecessary-type-parameters` |
| `noUnsafeArgument` | `./no-unsafe-argument` |
| `noUnsafeAssignment` | `./no-unsafe-assignment` |
| `noUnsafeCall` | `./no-unsafe-call` |
| `noUnsafeDeclarationMerging` | `./no-unsafe-declaration-merging` |
| `noUnsafeEnumComparison` | `./no-unsafe-enum-comparison` |
| `noUnsafeFunctionType` | `./no-unsafe-function-type` |
| `noUnsafeMemberAccess` | `./no-unsafe-member-access` |
| `noUnsafeReturn` | `./no-unsafe-return` |
| `noUnsafeTypeAssertion` | `./no-unsafe-type-assertion` |
| `noUnsafeUnaryMinus` | `./no-unsafe-unary-minus` |
| `noUnusedExpressions` | `./no-unused-expressions` |
| `noUnusedVars` | `./no-unused-vars` |
| `noUseBeforeDefine` | `./no-use-before-define` |
| `noUselessConstructor` | `./no-useless-constructor` |
| `noUselessEmptyExport` | `./no-useless-empty-export` |
| `noVarRequires` | `./no-var-requires` |
| `noWrapperObjectTypes` | `./no-wrapper-object-types` |
| `nonNullableTypeAssertionStyle` | `./non-nullable-type-assertion-style` |
| `onlyThrowError` | `./only-throw-error` |
| `parameterProperties` | `./parameter-properties` |
| `preferAsConst` | `./prefer-as-const` |
| `preferDestructuring` | `./prefer-destructuring` |
| `preferEnumInitializers` | `./prefer-enum-initializers` |
| `preferFind` | `./prefer-find` |
| `preferForOf` | `./prefer-for-of` |
| `preferFunctionType` | `./prefer-function-type` |
| `preferIncludes` | `./prefer-includes` |
| `preferLiteralEnumMember` | `./prefer-literal-enum-member` |
| `preferNamespaceKeyword` | `./prefer-namespace-keyword` |
| `preferNullishCoalescing` | `./prefer-nullish-coalescing` |
| `preferOptionalChain` | `./prefer-optional-chain` |
| `preferPromiseRejectErrors` | `./prefer-promise-reject-errors` |
| `preferReadonly` | `./prefer-readonly` |
| `preferReadonlyParameterTypes` | `./prefer-readonly-parameter-types` |
| `preferReduceTypeParameter` | `./prefer-reduce-type-parameter` |
| `preferRegexpExec` | `./prefer-regexp-exec` |
| `preferReturnThisType` | `./prefer-return-this-type` |
| `preferStringStartsEndsWith` | `./prefer-string-starts-ends-with` |
| `preferTsExpectError` | `./prefer-ts-expect-error` |
| `promiseFunctionAsync` | `./promise-function-async` |
| `relatedGetterSetterPairs` | `./related-getter-setter-pairs` |
| `requireArraySortCompare` | `./require-array-sort-compare` |
| `requireAwait` | `./require-await` |
| `restrictPlusOperands` | `./restrict-plus-operands` |
| `restrictTemplateExpressions` | `./restrict-template-expressions` |
| `returnAwait` | `./return-await` |
| `sortTypeConstituents` | `./sort-type-constituents` |
| `strictBooleanExpressions` | `./strict-boolean-expressions` |
| `switchExhaustivenessCheck` | `./switch-exhaustiveness-check` |
| `tripleSlashReference` | `./triple-slash-reference` |
| `typedef` | `./typedef` |
| `unboundMethod` | `./unbound-method` |
| `unifiedSignatures` | `./unified-signatures` |
| `useUnknownInCatchCallbackVariable` | `./use-unknown-in-catch-callback-variable` |


---

## 🔧 Functions

> No functions found in this file.


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