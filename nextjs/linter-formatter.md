# LinterとFormatter
## Formatter
### Prettierの設定
VSCode拡張機能の[Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)をインストールする。

`setting.json`に以下のように設定する。

```setting.json
{
  "editor.formatOnSave": true,
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

上記の設定で、ファイル保存時に自動フォーマットされます。

コマンドでフォーマットするには、必要なパッケージをインストールする必要がある。  
以下のコマンドを実行する。

```
npm install -D prettier eslint-config-prettier
```

`.prettierrc`のプラグインに、`prettier-plugin-organize-imports`を設定する場合には、以下のパッケージも必要です。

```
npm install -D prettier prettier-plugin-organize-imports typescript
```

プロジェクトのルートに`.prettierrc`ファイルを作成する。

```.prettierrc
{
  "printWidth": 80,
  "tabWidth": 2,
  "useTabs": false,
  "semi": true,
  "singleQuote": true,
  "quoteProps": "as-needed",
  "jsxSingleQuote": false,
  "trailingComma": "es5",
  "bracketSpacing": true,
  "arrowParens": "always",
  "endOfLine": "lf",
  "plugins": ["prettier-plugin-organize-imports"]
}
```

プロジェクトルートに`.prettierignore`を作成する。

```.prettierignore
# Build outputs
.next/
build/
dist/
out/
coverage/

# Dependencies
node_modules/
package-lock.json

# Environment variables
.env*

# Static assets
public/
```

以下のコマンドで現在のディレクトリとそのサブディレクトリ内のPrettierがサポートするすべてのファイルをフォーマットします。

```
npx prettier . --write
```

## Linter
### ESLintの設定
