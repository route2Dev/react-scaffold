# react-scaffold
React Scaffolding Instructions

## Scaffold the react project using [vite](https://vitejs.dev/guide/#scaffolding-your-first-vite-project)
```bash
npm create vite@latest
```
  
  - Name your project
  - Choose `react`
  - Choose `Typescript` (the default)

Open the project in VS Code.
```bash
cd <project-name>
code .
```
Open a terminal
```bash
# install dependencies
npm i
```

## Configure Engine versions
Add the the current LTS versions of Node and npm to the `package.json` file. Use the current LTS version instead of the settings below.
```json
"engines": {
  "npm": ">=10.0.0",
  "node": ">=20.0.0"
},
```

## Configure ESLint for Production
- Install [eslint-plugin-react](https://github.com/jsx-eslint/eslint-plugin-react)
```bash
npm i --save-dev eslint-plugin-react
```
- Add the following lines to the `extends` list in the `.eslint.cjs` file
```js
// other extends
'plugin:react/recommended',
'plugin:react/jsx-runtime'
```

- Add the following `settings` section to the `.eslint.cjs` file
```js
  settings: {
    react: {
      version: 'detect',
    },
  },
```

## [Prettier](https://prettier.io/docs/en/install)
```bash
npm i --save-dev prettier

# Configure
echo "{ \"singleQuote\": true }" > .prettierrc

```

Add ignore file 
```bash
touch .prettierignore
```

Add the following lines
```sh
# Ignore artifacts
dist
coverage
```

## [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)
* eslintrc: Add "prettier" to the "extends" array in your .eslintrc.* file. Make sure to put it last, so it gets the chance to override other configs.
```js
// other extends
"prettier"
```

Format all files
```bash
npx prettier . --write
```

## [husky](https://typicode.github.io/husky/get-started.html#install)
```bash
npm install --save-dev husky

# Configure
npx husky init
```

## [commitLint](https://commitlint.js.org/#/?id=getting-started)

```bash
npm install --save-dev @commitlint/config-conventional @commitlint/cli

# Configure
echo "{ extends: ['@commitlint/config-conventional'] }" > .commitlintrc

# Add commit message linting to commit-msg hook
echo "npx --no -- commitlint --edit \$1" > .husky/commit-msg
```

## [lint-staged](https://github.com/lint-staged/lint-staged#readme)

```bash
npm install --save-dev lint-staged

# Configure
echo "{'src/**/*.{ts,tsx}': ['npm run lint']}" > .lintstagedrc
```

Add husky hook to `.husky/pre-commit`
```js
#!/usr/bin/env sh
. "$(dirname "$0")/_/husky.sh"

npx --no -- lint-staged --quiet
```

## TypeScript / Vite
Configure relative paths

### tsconfig.json - add the following lines to the `"compilerOptions"` section
```
    /* Paths */
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
```

### vite.config 
- Import path (top of the file)
```js
import path from 'path;
```

- Add the following lines to `defineConfig`
```
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
    },
  },
```

## vscode settings
- Execute `Preferences: Open Workspace Settings (JSON)` from the vs code command palette
### settings.json
```
"editor.defaultFormatter": "esbenp.prettier-vscode",
"typescript.preferences.importModuleSpecifier": "non-relative",
"editor.formatOnSave": true
```

### Extension Recommendations
Create the extensions.json
```bash
touch .vscode/extensions.json
```

Then paste the following lines in the extensions.json file.
```json
{
  "recommendations": [
    "mikestead.dotenv",
    "dsznajder.es7-react-js-snippets",
    "dbaeumer.vscode-eslint",
    "eamodio.gitlens",
    "esbenp.prettier-vscode",
    "christian-kohler.path-intellisense"
  ]
}
```

## git
Add the project to git specifying `main` as the master branch
```bash
git init -b main
```

Delete following lines from the generated `.gitignore`
```
.vscode/*
!.vscode/extensions.json
```
