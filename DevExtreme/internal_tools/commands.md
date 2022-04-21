---
title: Commands
description: 
published: true
date: 2022-04-21T11:01:11.112Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:43:45.276Z
---

The **devextreme-internal-tools** package supports the following commands:

| Command                                                          | Description                                                                               |
| ---------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| [discover-declarations](#discover-declarations)                  | Runs discovering for js files and ts members meta                                         |
| [discover-ts-declarations](#discover-ts-declarations)            | Runs discovering for TS files only                                                        |
| [discover-renovation-declarations](#discover-renovation-declarations) | Runs discovering for TSX files only                                                  |
| [discover](#discover)                                            | Sequentially runs TS and JS discovering                                                   |
| [discover-renovation](#discover-renovation)                      | Sequentially runs TSX and JS discovering                                                  |
| [generate-modules-meta](#generate-modules-meta)                  | Generates the `modules-meta.json` file                                                    |
| [generate-extra-topics](#generate-extra-topics)                  | Generate MD files                                                                         |
| [generate-content-map](#generate-content-map)                    | Generates content maps necessary to run `WebSite.JS`. The actual content is not included. |
| [generate-ng-smd](#generate-ng-smd)                              | Generates the `NGMetaData.json` file                                                      |
| [generate-smd-ng](#generate-smd-ng)                              | Sequentially runs TS and JS discovering and then generates `NGMetaData.json` file         |
| [generate-smd](#generate-smd)                                    | Generates the `StrongMetaData.json` file                                                  |
| [generate-syntax-data](#generate-syntax-data)                    | Generate the `syntax-data.json file`                                                      |
| [generate-ts-bundle](#generate-ts-bundle)                        | Bundles all `*.d.ts` files to a single file (e.g. `dx.all.d.ts`)                          |
| [inject-descriptions-to-bundle](#inject-descriptions-to-bundle)  | Runs the injector for the `dx.all.d.ts` file only                                         |
| [inject-descriptions](#inject-descriptions)                      | Runs the injector for all `*.d.ts` files that equal the search pattern.                   |
| [integration-data-generator](#integration-data-generator)        | Generates `integration-data.json` and `integration-data-model.json`                       |
| [update-integration-meta](#update-integration-meta)              | Updates `integration-data.json` and `integration-data-model.json`                         |
| [update-links](#update-links)                                    | Updates links for the site. Logs are saved in the root directory.                         |
| [update-meta](#update-meta)                                      | Updates the `NGMetaData.json` file                                                        |
| [update-topics](#update-topics)                                  | Updates the documentation                                                                 |
| [update-ts-bundle](#update-ts-bundle)                            | Bundles all `*.d.ts` files to a single file (e.g. `dx.all.d.ts`)                          |
| [validate-declarations](#validate-declarations)                  | Validate `Declarations.json`                                                              |
| [validate-docs](#validate-docs)                                  | Validate MD files in devextreme-documenetation                                            |
| [validate-modules-guide](#validate-modules-guide)                | Validate 'DevExtreme Modules Structure' article                                           |
---


## discover-declarations
```
dx-tools discover-declarations
```
| Arg          | Default                            | Description                               |
| ------------ | ---------------------------------- | ----------------------------------------- |
| `js-scripts` | *rootDir*\js                       | See [common arguments](#common-arguments) |
| `artifacts`  | *rootDir*\artifacts\internal-tools | See [common arguments](#common-arguments) |
| `exclude`    | null                               | See [common arguments](#common-arguments) |

## discover-ts-declarations
```
dx-tools discover-ts-declarations
```
| Arg          | Default      | Description                               |
| ------------ | ------------ | ----------------------------------------- |
| `js-scripts` | *rootDir*\js | See [common arguments](#common-arguments) |
| `artifacts`  | *rootDir*\artifacts\internal-tools | See [common arguments](#common-arguments) |
| `exclude`    | null         | See [common arguments](#common-arguments) |

## discover-renovation-declarations
```
dx-tools discover-renovation-declarations
```
| Arg          | Default      | Description                               |
| ------------ | ------------ | ----------------------------------------- |
| `js-scripts` | *rootDir*\js | See [common arguments](#common-arguments) |
| `artifacts`  | *rootDir*\artifacts\internal-tools | See [common arguments](#common-arguments) |
| `exclude`    | null         | See [common arguments](#common-arguments) |


## discover
```
dx-tools discover
```
| Arg          | Default                            | Description                               |
| ------------ | ---------------------------------- | ----------------------------------------- |
| `js-scripts` | *rootDir*\js                       | See [common arguments](#common-arguments) |
| `artifacts`  | *rootDir*\artifacts\internal-tools | See [common arguments](#common-arguments) |
| `exclude`    | null                               | See [common arguments](#common-arguments) |

## discover-renovation
```
dx-tools discover-renovation
```
| Arg          | Default                            | Description                               |
| ------------ | ---------------------------------- | ----------------------------------------- |
| `js-scripts` | *rootDir*\js                       | See [common arguments](#common-arguments) |
| `artifacts`  | *rootDir*\artifacts\internal-tools | See [common arguments](#common-arguments) |
| `exclude`    | null                               | See [common arguments](#common-arguments) |

## generate-modules-meta
```
dx-tools generate-modules-meta
```
| Arg          | Default                            | Description                               |
| ------------ | ---------------------------------- | ----------------------------------------- |
| `js-scripts` | *rootDir*\js                       | See [common arguments](#common-arguments) |
| `exclude`    | null                               | See [common arguments](#common-arguments) |


## generate-extra-topics
```
dx-tools generate-extra-topics
```
| Arg          | Default                            | Description                               |
| ------------ | ---------------------------------- | ----------------------------------------- |
| `version`    | xx_x                               | See [common arguments](#common-arguments) |
| `docs-root`  |                                    | See [common arguments](#common-arguments) |

## generate-content-map
```
dx-tools generate-content-map
```
| Arg               | Default                   | Description                               |
| ----------------- | ------------------------- | ----------------------------------------- |
| `docs-root`       | *rootDir*                 | See [common arguments](#common-arguments) |
| `version`         | Version in `package.json` | See [common arguments](#common-arguments) |
| `syntaxdata-path` |                           |                                           |

## generate-ng-smd
```
dx-tools generate-ng-smd --version xx_x
```
| Arg                 | Default                                              | Description                               |
| ------------------- | ---------------------------------------------------- | ----------------------------------------- |
| `version`           | xx_x                                                 | See [common arguments](#common-arguments) |
| `output-path`       | *rootDir*\artifacts\internal-tools\NGMetaData.json   | See [common arguments](#common-arguments) |
| `declarations-path` | *rootDir*\artifacts\internal-tools\Declarations.json | See [common arguments](#common-arguments) |
| `js-scripts`        | *rootDir*\js                                         | See [common arguments](#common-arguments) |

## generate-smd-ng
```
dx-tools generate-smd-ng --version xx_x
```
| Arg                 | Default                                              | Description                               |
| ------------------- | ---------------------------------------------------- | ----------------------------------------- |
| `js-scripts`        | *rootDir*\js                                         | See [common arguments](#common-arguments) |
| `artifacts`         | *rootDir*\artifacts\internal-tools                   | See [common arguments](#common-arguments) |
| `exclude`           | null                                                 | See [common arguments](#common-arguments) |
| `version`           | xx_x                                                 | See [common arguments](#common-arguments) |
| `output-path`       | *rootDir*\artifacts\internal-tools\NGMetaData.json   | See [common arguments](#common-arguments) |
| `declarations-path` | *rootDir*\artifacts\internal-tools\Declarations.json | See [common arguments](#common-arguments) |

## generate-smd
```
dx-tools generate-smd --version xx_x
```
| Arg                 | Default                                                | Description                               |
| ------------------- | ------------------------------------------------------ | ----------------------------------------- |
| `version`           | xx_x                                                   | See [common arguments](#common-arguments) |
| `output-path`       | *rootDir*\artifacts\internal-tools\StrongMetaData.json | See [common arguments](#common-arguments) |
| `declarations-path` | *rootDir*\artifacts\internal-tools\Declarations.json   | See [common arguments](#common-arguments) |

## generate-syntax-data
```
dx-tools generate-syntax-data
```
| Arg                 | Default                                                | Description                               |
| ------------------- | ------------------------------------------------------ | ----------------------------------------- |
| output-path         |                                                        | See [common arguments](#common-arguments) |
| declarations-path   |                                                        | See [common arguments](#common-arguments) |

## generate-ts-bundle
```
dx-tools generate-ts-bundle --js-scripts D:\DevExtreme\js --output-path D:\DevExtreme\ts\dx.all.d.ts
```
| Arg           | Default                  | Description                               |
| ------------- | ------------------------ | ----------------------------------------- |
| `js-scripts`  | undefined                | See [common arguments](#common-arguments) |
| `output-path` | undefined                | See [common arguments](#common-arguments) |
| `exclude`     | null                     | See [common arguments](#common-arguments) |

For more information, see [Bundler specs](#bundler-specs)

## inject-descriptions-to-bundle
```
dx-tools inject-descriptions-to-bundle
```
| Arg                 | Default                                                          | Description                               |
| ------------------- | ---------------------------------------------------------------- | ----------------------------------------- |
| `js-scripts`        | *rootDir*\js                                                     | See [common arguments](#common-arguments) |
| `descriptions-path` | *rootDir*\artifacts\internal-tools\Descriptions.json             | Sets path to the Descriptions.json file   |
| `target-path`       | *rootDir*\node_modules\devextreme-internal-tools\bin\dx.all.d.ts | Sets the path to the `dx.all.d.ts` file   |
| `output-path`       | `target-path                                                     | See [common arguments](#common-arguments) |
| `exclude`           | null                                                             | See [common arguments](#common-arguments) |

## inject-descriptions
```
dx-tools inject-descriptions
```
| Arg                 | Default                                              | Description                               |
| ------------------- | ---------------------------------------------------- | ----------------------------------------- |
| `js-scripts`        | *rootDir*\js                                         | See [common arguments](#common-arguments) |
| `descriptions-path` | *rootDir*\artifacts\internal-tools\Descriptions.json | Sets path to the Descriptions.json file   |
| `search-pattern`    | *                                                    | Sets a pattern to find the files          |
| `exclude`           | null                                                 | See [common arguments](#common-arguments) |

## integration-data-generator
```
dx-tools integration-data-generator
```
| Arg                 | Default                                                  | Description                               |
| ------------------- | -------------------------------------------------------- | ----------------------------------------- |
| `output-path`       | *rootDir*\artifacts\internal-tools\integration-data.json | See [common arguments](#common-arguments) |
| `declarations-path` | *rootDir*\artifacts\internal-tools\Declarations.json     | See [common arguments](#common-arguments) |

## update-integration-meta
```
dx-tools update-integration-meta --js-scripts D:\DevExtreme\js --docs-root D:\devextreme-docs
```
| Arg                 | Default                                                  | Description                               |
| ------------------- | -------------------------------------------------------- | ----------------------------------------- |
| `js-scripts`        | *rootDir*\js                                             | See [common arguments](#common-arguments) |
| `artifacts`         | *rootDir*\artifacts\internal-tools                       | See [common arguments](#common-arguments) |
| `output-path`       | *rootDir*\artifacts\internal-tools\integration-data.json | See [common arguments](#common-arguments) |
| `declarations-path` | *rootDir*\artifacts\internal-tools\Declarations.json     | See [common arguments](#common-arguments) |
| `docs-root`         | Optional parameter                                       | See [common arguments](#common-arguments) |
| `exclude`         | null                                                     | See [common arguments](#common-arguments) |

## update-links
```
dx-tools update-links --check-all --validation
```
| Flag               | Description                                  |
| ------------------ | -------------------------------------------- |
| `--fail-on-change` | Check and update links in changed files only |
| `--check-all`      | Check and update links in all files          |
| `--validation`     | Check links without updating them            |

## update-meta
```
dx-tools update-meta --version xx_x --js-scripts D:\DevExtreme\js --docs-root D:\devextreme-docs
```
| Arg                 | Default                                              | Descriptions                              |
| ------------------- | ---------------------------------------------------- | ----------------------------------------- |
| `version`           | xx_x                                                 | See [common arguments](#common-arguments) |
| `js-scripts`        | *rootDir*\js                                         | See [common arguments](#common-arguments) |
| `artifacts`         | *rootDir*\artifacts\internal-tools                   | See [common arguments](#common-arguments) |
| `output-path`       | *rootDir*\artifacts\internal-tools\NGMetaData.json   | See [common arguments](#common-arguments) |
| `declarations-path` | *rootDir*\artifacts\internal-tools\Declarations.json | See [common arguments](#common-arguments) |
| `docs-root`         | Optional parameter                                   | See [common arguments](#common-arguments) |
| `exclude`           | null                                                 | See [common arguments](#common-arguments) |

## update-topics
```
dx-tools update-topics
```
| Arg          | Default                            | Description                               |
| ------------ | ---------------------------------- | ----------------------------------------- |
| `js-scripts` | *rootDir*\js                       | See [common arguments](#common-arguments) |
| `docs-root`  | *rootDir*                          | See [common arguments](#common-arguments) |
| `artifacts`  | *rootDir*\artifacts\internal-tools | See [common arguments](#common-arguments) |

## update-ts-bundle
```
dx-tools update-ts-bundle --js-scripts D:\DevExtreme\js --output-path D:\DevExtreme\ts\dx.all.d.ts
```
| Arg           | Default                  | Description                               |
| ------------- | ------------------------ | ----------------------------------------- |
| `js-scripts`  | undefined                | See [common arguments](#common-arguments) |
| `output-path` | undefined                | See [common arguments](#common-arguments) |
| `exclude`     | null                     | See [common arguments](#common-arguments) |

For more information, see [Bundler specs](#bundler-specs)

## validate-declarations
```
dx-tools validate-declarations
```
| Arg          | Default      | Description                               |
| ------------ | ------------ | ----------------------------------------- |
| `js-scripts` | *rootDir*\js | See [common arguments](#common-arguments) |
| `artifacts`  | *rootDir*\artifacts\internal-tools | See [common arguments](#common-arguments) |
| `exclude`    | null         | See [common arguments](#common-arguments) |

## validate-docs
```
dx-tools validate-docs
```
| Arg          | Default                            | Description                               |
| `docs-root`  | *rootDir*                          | See [common arguments](#common-arguments) |

## validate-modules-guide
```
dx-tools validate-modules-guide
```
| Arg                   | Default                            | Description                               |
| `modules-guide-path`  |                                    |                                           |
| `modules-meta`        |                                    | Path to the modules-meta.json             |

# Common Arguments

| Arg                 | Description                                                                                         |
| ------------------- | --------------------------------------------------------------------------------------------------- |
| `js-scripts`        | Path to the `js` folder in the [DevExtreme repo](https://github.com/DevExpress/DevExtreme)          |
| `docs-root`         | Path to the [devextreme-documentation repo](https://github.com/DevExpress/devextreme-documentation) |
| `version`           | Major version (for example, `20_1`)                                                                 |
| `artifacts`         | Path to the `artifacts` folder                                                                      |
| `declarations-path` | Path to the `Declarations.json` file                                                                |
| `output-path`       | Path to the output file                                                                             |
| `exclude`           | Pattern for ignoring files                                                                          |


# Development

We assume that [DevExtreme repo](https://github.com/DevExpress/DevExtreme) is located in the same parent directory:
```
···
├── devextreme/
│   ├── js/
│   └── ···
├── devextreme-internal-tools/
│   └── ···
···
```
If you need to target another directory, go to `./package.json` and change `--js-scripts` argument value.

## Discover TypeScript Declarations

```
npm run build-ts
npm run discover
```

The commands above run the TypeScript Discoverer only. The .NET Discoverer should be run separately.

## Discover TypeScript Declarations in Watch Mode

```
npm run build-ts-watch
npm run discover-watch
```

`build-ts-watch` recompiles the TypeScript Discoverer when its sources change.

`discover-watch` reruns the TypeScript Discoverer when Declarations change.