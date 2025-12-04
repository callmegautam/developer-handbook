
## Step 1: Install deps

```bash
npm install -D eslint prettier eslint-config-prettier eslint-plugin-prettier \
  @typescript-eslint/eslint-plugin @typescript-eslint/parser \
  eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-import \
  eslint-plugin-jsx-a11y
```


---

## Step 2: Create `.eslintrc.json`

```json
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": [
    "@typescript-eslint",
    "react",
    "react-hooks",
    "jsx-a11y",
    "import",
    "prettier"
  ],
  "extends": [
    "next/core-web-vitals",
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:react/recommended",
    "plugin:react-hooks/recommended",
    "plugin:jsx-a11y/recommended",
    "plugin:import/recommended",
    "plugin:import/typescript",
    "plugin:prettier/recommended"
  ],
  "settings": {
    "react": {
      "version": "detect"
    }
  },
  "rules": {
    "prettier/prettier": "error",

    "react/react-in-jsx-scope": "off",
    "react/jsx-uses-react": "off",

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

## Step 4: Add lint scripts

```json
{
  "scripts": {
    "lint": "eslint . --ext ts,tsx --fix"
  }
}
```

---

## Step 5: Enable auto-fix on save (VS Code)

```json
"editor.codeActionsOnSave": {
  "source.fixAll.eslint": true
}
```

---