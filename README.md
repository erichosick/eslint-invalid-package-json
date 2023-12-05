# ESLint Error on Invalid json file named `package.json`

When testing linter settings, a [`lint-tests`](./lint-tests/) was created which contained valid and invalid files. These were being used to verify if the lint configuration and associated rules were running as expected.

One of the test files we created was `./lint-tests/package.json` which had a comment in it (for testing).

This caused ESLint, in the Visual Studio Code Environment, to throw the following error:

```
Error: Request eslint/noLibrary failed with message: command 'npm.packageManager' not found
    at /.../.vscode/extensions/dbaeumer.vscode-eslint-2.4.2/server/out/eslintServer.js:1:56556
    at oe (/.../.vscode/extensions/dbaeumer.vscode-eslint-2.4.2/server/out/eslintServer.js:1:56850)
    at /.../.vscode/extensions/dbaeumer.vscode-eslint-2.4.2/server/out/eslintServer.js:1:51634
    at Immediate.<anonymous> (/.../.vscode/extensions/dbaeumer.vscode-eslint-2.4.2/server/out/eslintServer.js:1:51654)
    at process.processImmediate (node:internal/timers:476:21)
```

However, running eslint at the command line `ESLINT_USE_FLAT_CONFIG=true npx eslint --config eslint.config.mjs .` works and the invalid `package.json` file is linted successfully.

```
# works from the command line.
$ pnpm eslint
/.../lint-tests/package.json
  1:1  error  Unexpected comment  jsonc/no-comments
```

## Issue

VSCode ESLint issue [1742](https://github.com/microsoft/vscode-eslint/issues/1742).
