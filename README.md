# Simple typescript monorepo example

## Purpose

The goal of this template is to provide a simple way of organizing TypeScript projects that meet the following criteria:

- Do not require additional dependencies for managing a monorepository.
- Can be easily integrated into existing projects with minimal effort.
- Allow referencing neighboring packages without the need for their prior build.

## Requirements

- TypeScript version 3 or higher.
- npm version 7 or higher.

## Features

### NPM Workspaces

NPM Workspaces is a key feature of this template, which:

- Allows referencing of neighboring packages without extra configuration.
- Optimizes the organization of dependencies within the node_modules directory.
- Letting you run commands across several projects at once.
- Works "out of the box" without the need for additional setup or builder.

### TypeScript Project References

- Prevents the need to rebuild packages if their code has not been modified.
- Enhances performance when working with the codebase in TypeScript-supporting editors.
- Helps TypeScript figure out the best build order, considering project dependencies.

## Setup Method

Add the `workspaces` field to the `package.json` in the root directory:

```json
"workspaces": { "packages": ["any-package", "packages/*", "etc"] }
```

In each package that reuses another package, specify it in the `tsconfig.json`:

```json
{
  "compilerOptions": {
    "paths": {
      "package-shared/*": ["../shared/src/*"]
    }
  },
  "references": [
    {"path": "../shared"}
  ]
}
```

In each reusable package, add the following to the `tsconfig.json`:

```json
"composite": true,
```

In each reusable package, add exports to the `package.json`:

```json
"exports": {
	".": "./dist/index.js",
	"./*": "./dist/*.js",
	"./folder": "./dist/folder/index.js"
}
```

Exports are recognized by `Node.js`, `webpack`, and other bundlers ([read more](https://webpack.js.org/guides/package-exports/)).
