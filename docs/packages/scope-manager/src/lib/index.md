[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `index.ts`

## 📚 Table of Contents

- [Imports](#imports)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 107
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/lib/index.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `LibDefinition` | `../variable` |
| `decorators` | `./decorators` |
| `decorators_legacy` | `./decorators.legacy` |
| `dom` | `./dom` |
| `dom_asynciterable` | `./dom.asynciterable` |
| `dom_iterable` | `./dom.iterable` |
| `es5` | `./es5` |
| `es6` | `./es6` |
| `es7` | `./es7` |
| `es2015` | `./es2015` |
| `es2015_collection` | `./es2015.collection` |
| `es2015_core` | `./es2015.core` |
| `es2015_generator` | `./es2015.generator` |
| `es2015_iterable` | `./es2015.iterable` |
| `es2015_promise` | `./es2015.promise` |
| `es2015_proxy` | `./es2015.proxy` |
| `es2015_reflect` | `./es2015.reflect` |
| `es2015_symbol` | `./es2015.symbol` |
| `es2015_symbol_wellknown` | `./es2015.symbol.wellknown` |
| `es2016` | `./es2016` |
| `es2016_array_include` | `./es2016.array.include` |
| `es2016_full` | `./es2016.full` |
| `es2016_intl` | `./es2016.intl` |
| `es2017` | `./es2017` |
| `es2017_arraybuffer` | `./es2017.arraybuffer` |
| `es2017_date` | `./es2017.date` |
| `es2017_full` | `./es2017.full` |
| `es2017_intl` | `./es2017.intl` |
| `es2017_object` | `./es2017.object` |
| `es2017_sharedmemory` | `./es2017.sharedmemory` |
| `es2017_string` | `./es2017.string` |
| `es2017_typedarrays` | `./es2017.typedarrays` |
| `es2018` | `./es2018` |
| `es2018_asyncgenerator` | `./es2018.asyncgenerator` |
| `es2018_asynciterable` | `./es2018.asynciterable` |
| `es2018_full` | `./es2018.full` |
| `es2018_intl` | `./es2018.intl` |
| `es2018_promise` | `./es2018.promise` |
| `es2018_regexp` | `./es2018.regexp` |
| `es2019` | `./es2019` |
| `es2019_array` | `./es2019.array` |
| `es2019_full` | `./es2019.full` |
| `es2019_intl` | `./es2019.intl` |
| `es2019_object` | `./es2019.object` |
| `es2019_string` | `./es2019.string` |
| `es2019_symbol` | `./es2019.symbol` |
| `es2020` | `./es2020` |
| `es2020_bigint` | `./es2020.bigint` |
| `es2020_date` | `./es2020.date` |
| `es2020_full` | `./es2020.full` |
| `es2020_intl` | `./es2020.intl` |
| `es2020_number` | `./es2020.number` |
| `es2020_promise` | `./es2020.promise` |
| `es2020_sharedmemory` | `./es2020.sharedmemory` |
| `es2020_string` | `./es2020.string` |
| `es2020_symbol_wellknown` | `./es2020.symbol.wellknown` |
| `es2021` | `./es2021` |
| `es2021_full` | `./es2021.full` |
| `es2021_intl` | `./es2021.intl` |
| `es2021_promise` | `./es2021.promise` |
| `es2021_string` | `./es2021.string` |
| `es2021_weakref` | `./es2021.weakref` |
| `es2022` | `./es2022` |
| `es2022_array` | `./es2022.array` |
| `es2022_error` | `./es2022.error` |
| `es2022_full` | `./es2022.full` |
| `es2022_intl` | `./es2022.intl` |
| `es2022_object` | `./es2022.object` |
| `es2022_regexp` | `./es2022.regexp` |
| `es2022_string` | `./es2022.string` |
| `es2023` | `./es2023` |
| `es2023_array` | `./es2023.array` |
| `es2023_collection` | `./es2023.collection` |
| `es2023_full` | `./es2023.full` |
| `es2023_intl` | `./es2023.intl` |
| `es2024` | `./es2024` |
| `es2024_arraybuffer` | `./es2024.arraybuffer` |
| `es2024_collection` | `./es2024.collection` |
| `es2024_full` | `./es2024.full` |
| `es2024_object` | `./es2024.object` |
| `es2024_promise` | `./es2024.promise` |
| `es2024_regexp` | `./es2024.regexp` |
| `es2024_sharedmemory` | `./es2024.sharedmemory` |
| `es2024_string` | `./es2024.string` |
| `esnext` | `./esnext` |
| `esnext_array` | `./esnext.array` |
| `esnext_asynciterable` | `./esnext.asynciterable` |
| `esnext_bigint` | `./esnext.bigint` |
| `esnext_collection` | `./esnext.collection` |
| `esnext_decorators` | `./esnext.decorators` |
| `esnext_disposable` | `./esnext.disposable` |
| `esnext_float16` | `./esnext.float16` |
| `esnext_full` | `./esnext.full` |
| `esnext_intl` | `./esnext.intl` |
| `esnext_iterator` | `./esnext.iterator` |
| `esnext_object` | `./esnext.object` |
| `esnext_promise` | `./esnext.promise` |
| `esnext_regexp` | `./esnext.regexp` |
| `esnext_string` | `./esnext.string` |
| `esnext_symbol` | `./esnext.symbol` |
| `esnext_weakref` | `./esnext.weakref` |
| `libBase` | `./lib` |
| `scripthost` | `./scripthost` |
| `webworker` | `./webworker` |
| `webworker_asynciterable` | `./webworker.asynciterable` |
| `webworker_importscripts` | `./webworker.importscripts` |
| `webworker_iterable` | `./webworker.iterable` |


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