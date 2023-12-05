# TS-node + ESM + Paths

This is a reproduction to show that TS-node does not support ESM + Paths.

## Requirements 

- Node 20.10.0

## Configuration

- `tsconfig.json` -> `compilerOptions.module` is set to `esnext`
- `tsconfig.json` -> `compilerOptions.target` is set to `esnext`
- `package.json`  -> `type` is set to `module`
- I then defined paths in `tsconfig.json` -> `compilerOptions.paths`

## Steps to reproduce

1. Clone this repo
2. Run `npm install`

Now you have 5 different `dev` scripts you can run, and they all fail. Each have a different `loader`:
- `npm run dev:1` -> use of `ts-node/esm/transpile-only`
    which fails with `ERR_INVALID_MODULE_SPECIFIER @utils is not a valid package name`
- `npm run dev:2` -> use of `@bleed/believer/path-alias`
    which fails with `TypeError: [ERR_UNKNOWN_FILE_EXTENSION]: Unknown file extension ".ts"`
- `npm run dev:3` -> use of `ts-paths-esm-loader/transpile-only`
    which fails with `ERR_UNSUPPORTED_DIR_IMPORT /home/coder/tmp/ts-node-esm-paths-repro/src/utils`
- `npm run dev:4` -> use of custom `./loaders/loaders1.js`
    which fails with `TypeError [Error]: Unknown file extension ".ts"`
- `npm run dev:5` -> use of custom `./loaders/loaders2.js`
    which fails with `TypeError [ERR_UNKNOWN_FILE_EXTENSION]: Unknown file extension ".ts"`