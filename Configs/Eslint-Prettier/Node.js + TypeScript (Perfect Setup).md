## Step 1: Install deps

```bash
npm install -D eslint prettier eslint-config-prettier eslint-plugin-prettier \
  @typescript-eslint/eslint-plugin @typescript-eslint/parser \
  eslint-plugin-import eslint-plugin-node
```

---

## Step 2: Create `.eslintrc.json`

```json
{
  "root": true,
  "env": {
    "node": true,
    "es2022": true
  },
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint", "import", "node", "prettier"],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:import/recommended",
    "plugin:import/typescript",
    "plugin:node/recommended",
    "plugin:prettier/recommended"
  ],
  "rules": {
    "prettier/prettier": "error",

    "node/no-unsupported-features/es-syntax": "off",

    "@typescript-eslint/no-unused-vars": [
      "warn",
      { "argsIgnorePattern": "^_", "varsIgnorePattern": "^_" }
    ],

    "import/order": [
      "warn",
      {
        "groups": ["builtin", "external", "internal", "parent", "sibling", "index"],
        "alphabetize": { "order": "asc", "caseInsensitive": true }
      }
    ]
  }
}
```


---

## Step 3: Create `prettier.config.cjs`

```js
module.exports = {
  semi: true,
  singleQuote: false,
  trailingComma: "all",
  tabWidth: 2,
  printWidth: 100,
  bracketSpacing: true,
  arrowParens: "avoid"
};
```

---

## Step 4: Add lint script

```json
{
  "scripts": {
    "lint": "eslint . --ext ts --fix"
  }
}
```
