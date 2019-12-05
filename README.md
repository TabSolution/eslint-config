# TabSolution™ Eslint and Prettier Setup
These are my settings for ESLint and Prettier

Don't worry we can always update them.

## What it does
* Lints JavaScript based on the latest standards
* Fixes issues and formatting errors with Prettier
* Lints + Fixes inside of html script tags
* Lints + Fixes React via eslint-config-airbnb
* You can see all the [rules here](https://github.com/TabSolution/eslint-config/blob/master/.eslintrc.js) - these generally abide by the code written in my courses. You are very welcome to overwrite any of these settings, or just fork the entire thing to create your own.

## Installing

You can use eslint globally and/or locally per project.

It's usually best to install this locally once per project, that way you can have project specific settings as well as sync those settings with others working on your project via git.

I also install globally so that any project or rogue JS file I write will have linting and formatting applied without having to go through the setup. You might disagree and that is okay, just don't do it then 😃.


## Local / Per Project Install

1. If you don't already have a `package.json` file, create one with `npm init`.

2. Then we need to install everything needed by the config:

```
npx install-peerdeps --dev @tabsolution/eslint-config
```

3. You can see in your package.json there are now a big list of devDependencies.

4. You can add two scripts to your package.json to lint and/or fix:

```json
"scripts": {
  "test": "echo \"No test specified\"",
  "lint": "eslint .",
  "lint:fix": "eslint . --fix"
},
```

6. Now you can manually lint your code by running `npm run lint` and fix all fixable issues with `npm run lint:fix`. You probably want your editor to do this though.

## Global Install

1. First install everything needed:

```
npx install-peerdeps --dev @tabsolution/eslint-config
```
(**note:** npx is not a spelling mistake of **npm**. `npx` comes with when `node` and `npm` are installed and makes script running easier 😃)

2. Then you need to make a global `.eslintrc` file:

ESLint will look for one in your home directory

* `~/.eslintrc` for mac
* `C:\Users\username\.eslintrc` for windows
In your `.eslintrc` file, it should look like this:

```json
{
  "extends": [
    "wesbos"
  ]
}
```

3. To use from the CLI, you can now run `eslint .` or configure your editor as we show next.

## Settings

### .eslintrc settings
If you'd like to overwrite eslint or prettier settings, you can add the rules in your `.eslintrc` file. The [ESLint rules](https://eslint.org/docs/rules/) go directly under `"rules"` while [prettier options](https://prettier.io/docs/en/options.html) go under `"prettier/prettier"`. 

```js
module.exports = {
  root: true,
  extends: ['@tabsolution/eslint-config', 'prettier', 'prettier/react'],
  plugins: ['prettier'],
  rules: {
    camelcase: 'off',

    // 'global-require': 0,
    'react/prop-types': 0,
    'no-use-before-define': ['error', { variables: false }],
    // 'no-undef': 0,
    // 'react/no-this-in-sfc': 0,
    // 'react/jsx-no-bind': 0,
    // 'no-prototype-builtins': 0,
    // 'react/no-unused-prop-types': 0,
    // 'import/no-extraneous-dependencies': 0,
    // 'react/no-unused-state': 0,
    // 'react/destructuring-assignment': 0,
    // 'react/jsx-no-duplicate-props': 0,
    'no-shadow': 0,
    'array-callback-return': 0,
    // "no-console": 2,
    "prettier/prettier": "error"
  },
  globals: {
    // "__CLIENT__": true,
    // "__SERVER__": true,
    __DEV__: true,
  },
  settings: {
    'import/resolver': {
      'babel-module': {},
    },
  },
};

```
### .prettierrc settings
If you'd like to overwrite eslint or prettier settings, you can add the rules in your `.prettierrc` file. Note that prettier rules overwrite anything in my config (trailing comma, and single quote), so you'll need to include those as well. 

```js
module.exports = {
  bracketSpacing: true,
  jsxBracketSameLine: false,
  singleQuote: true,
  trailingComma: 'all',
  tabWidth: 2,
};
```

## With VS Code

You should read this entire thing. Serious!

Once you have done one, or both, of the above installs. You probably want your editor to lint and fix for you. Here are the instructions for VS Code:

1. Install the [ESLint package](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
2. Now we need to setup some VS Code settings via `Code/File` → `Preferences` → `Settings`. It's easier to enter these settings while editing the `settings.json` file, so click the `{}` icon in the top right corner:
  ```js
  {
    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode",
    },
    // tell the ESLint plugin to run on save
    "eslint.autoFixOnSave": true,
    "javascript.updateImportsOnFileMove.enabled": "always",
}
  ```

## With Create React App

1. You gotta eject first `npm run eject` or `yarn eject`
2. Run `npx install-peerdeps --dev @tabsolution/eslint-config`