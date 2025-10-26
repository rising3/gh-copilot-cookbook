---
applyTo: "examples/ts/**"
---
GitHub Copilotへの指示は、原則日本語を利用します。
よってソースコードや開発に関する設定・サンプル以外の回答は極力日本語を利用して下さい。

# TypeScipt General Instructions
このリポジトリは、GitHub Copilotに対するTypeScript関連の指示をまとめたものです。
以下、ガイドに従ってください。


## 開発標準

### 開発環境
- Node.jsのバージョン: 22.x LTS以上
- パッケージマネージャー: npm
- TypeScriptのバージョン: 最新版
- TypeDocのバージョン: 最新版
- ESLintのバージョン: 8.4以上９未満
- Prettierのバージョン: 2.x以上
- Jestのバージョン: 27.x以上
- ts-nodeのバージョン: 最新版
- ts-jestのバージョン: 最新版
- rimrafのバージョン: 最新版
- npm-run-allのバージョン: 最新版
- その他必要なツールやライブラリは、プロジェクトごとに指示を追加してください。

以下は、上記の主なパッケージです。

- @types/jest
- @typescript-eslint/eslint-plugin
- @typescript-eslint/parser
- eslint
- eslint-config-prettier
- jest
- prettier
- ts-node
- ts-jest
- typescript
- rimraf
- npm-run-all
- typedoc

### プロジェクト構成
- .github/: GitHub関連の設定ファイル
- .vscode/: Visual Studio Code関連の設定ファイル
- src/: ソースコード
- tests/: テストコード
- dist/: ビルド出力
- docs/: ドキュメント出力
- .gitignore: Gitで無視するファイルやディレクトリを指定するファイル
- .prettierrc: Prettier設定ファイル
- .prettierignore: Prettierで無視するファイルやディレクトリを指定するファイル
- package.json: プロジェクトの依存関係とスクリプトを定義するファイル
- tsconfig.json: TypeScriptコンパイラ設定ファイル
- jest.config.js: Jest設定ファイル
- eslint.config.js: FlatConfig形式のESLint設定ファイル
- typedoc.json: TypeDoc設定ファイル
- README.md: プロジェクトの説明書

設定ファイルは以下の内容を基に作成してください。

package.json:
```json
{
  "name": "project-name",
  "version": "0.0.1",
  "description": "Project description",
  "keywords": [], 
  "author": "Your Name",
  "license": "ISC",
  "repository": {
    "type": "git",
    "url": "git+https://github.com/your-username/project-name.git"
  },
  "main": "dist/index.js",
  "types": "dist/index.d.ts",
  "scripts": {
    "clean": "rimraf dist coverage docs",
    "build": "tsc",
    "build:all": "npm-run-all clean lint format test build docs",
    "test": "jest",
    "test:coverage": "jest --coverage",
    "docs": "npx typedoc",
    "lint": "eslint 'src/**/*.{ts,tsx}' 'tests/**/*.{ts,tsx}'",
    "lint:fix": "eslint 'src/**/*.{ts,tsx}' 'tests/**/*.{ts,tsx}' --fix",
    "format": "prettier --check 'src/**/*.{ts,tsx}' 'tests/**/*.{ts,tsx}'",
    "format:fix": "prettier --write 'src/**/*.{ts,tsx}' 'tests/**/*.{ts,tsx}'",
  }
}
```

tsconfig.json:
```json
{
  "compilerOptions": {
    "target": "ES2021",
    "module": "commonjs",
    "outDir": "dist",
    "rootDir": "src",
    "declaration": true, 
    "strict": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "skipLibCheck": true

    },
  "include": ["src/**/*.ts"]
}
```

jest.config.js:
```javascript
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
  testMatch: ['**/tests/**/*.test.ts'],
  transform: {
    '^.+\\.ts$': 'ts-jest',
  },
  verbose: true,
};
```

.gitignore:
```
node_modules/
dist/
docs/
```

eslint.config.js:
```js
const { FlatCompat } = require('@eslint/eslintrc');
const prettier = require('eslint-config-prettier');
const eslintJs = require('@eslint/js');

const compat = new FlatCompat();

module.exports = [
  {
    files: ["src/**/*.{ts,tsx}", "tests/**/*.{ts,tsx}"],
    ...eslintJs.configs.recommended,
  },
  ...compat.config({
    extends: [
      'plugin:@typescript-eslint/recommended',
      'plugin:import/recommended',
      'plugin:import/typescript',
      'prettier',
    ],
    plugins: ['@typescript-eslint', 'import'],
    parser: '@typescript-eslint/parser',
    parserOptions: {
      ecmaVersion: 2021,
      sourceType: 'module',
    },
    env: {
      node: true,
      jest: true,
      es2021: true,
    },
    rules: {},
  }),
  prettier,
];
``` 

.prettierrc:
```json
{
  "trailingComma": "es5",
  "tabWidth": 2,
  "semi": true,
  "singleQuote": true,
  "printWidth": 100,
  "endOfLine": "lf"
}  
```

.prettierignore:
```
.gitignore
.eslintrc.json
.prettierrc
.prettierignore

package.json
package-lock.json
tsconfig.json
jest.config.js
typedoc.json
README.md
LICENSE

dist/
docs/
```

typedoc.json:
```json
{
  "entryPoints": ["src/index.ts"],
  "out": "docs",
  "includeVersion": true,
  "excludePrivate": true,
  "excludeProtected": true,
  "excludeInternal": true,
  "hideGenerator": false
}
```

ドキュメントは以下の内容を基に作成してください。

README.md:
```markdown
# Project Name
```


### 開発の流れ
- パッケージのインストール: `npm install`
- 開発中のコードのテスト: `npm run test`
- コードの静的解析: `npm run lint`
- コードのフォーマットチェック: `npm run format`
- コードのビルド: `npm run build`
- ドキュメント生成: `npm run docs`
- 出力先の削除: `npm run clean`
- パッケージアーカイブの作成: `npm pack`
- パッケージの公開: `npm publish`
- CI/CDの設定: GitHub Actionsを使用して、自動テストとビルドを実行する
- その他の開発フローは、プロジェクトごとに指示を追加してください。

### コミット
- コミットを行う前に、必ずコードの静的解析とフォーマット及びテストを実行し、エラーがないことを確認すること。
- コミットは、小さな単位で行い、意味のある変更ごとにコミットすること。
- コミットメッセージは、以下のフォーマットに従うこと:
  - feat: 新機能の追加
  - fix: バグ修正
  - docs: ドキュメントの変更
  - style: フォーマットの変更（コードの動作に影響しない）
  - refactor: リファクタリング
  - test: テストの追加・修正
  - chore: その他の変更（ビルドプロセスや補助ツールの変更など）

### コーディング規約
原則、ESLintとPrettierの設定に従うこと。
追加のコーディング規約として、以下を遵守すること:
- TSDocコメントを使用して、関数やクラスの説明、引数、戻り値を明確にすること。
- コメントは必要に応じて適切に追加し、コードの意図を明確にすること。
- その他のコーディング規約は、プロジェクトごとに指示を追加してください。

### 開発補足
- index.tsファイルは、モジュールのエントリーポイントとして機能し、主要なクラスや関数をエクスポートすること。
- 非同期処理にはasync/awaitを使用し、Promiseチェーンは避けること。
- エラーハンドリングはtry/catchブロックを使用し、適切なエラーメッセージを提供すること。
- 型定義は可能な限り厳密に行い、any型の使用は最小限に抑えること。
- 変数名、関数名、クラス名は意味のある名前を付け、一貫性を保つこと。
- コードの可読性を向上させるために、適切なインデントと空白を使用すること。
- コードのコメントは適切に記述する必要がある。
- クラスや関数のモジュール化は、適切な単位で行い、再利用性を高めること。
- その他の開発補足は、プロジェクトごとに指示を追加してください。

### テスト
- ユニットテストはJestを使用して作成し、各関数やクラスの主要な機能をカバーすること。

### 外部モジュールと依存関係
- 外部モジュールのライセンスは必ず確認し、非コピーレフトの外部モジュールを利用すること。
- 依存関係は必要最低限に抑え、信頼できるパッケージのみを使用すること。
- 依存関係のバージョンは定期的に更新し、セキュリティリスクを最小限に抑えること。
- その他のモジュールと依存関係に関する指示は、プロジェクトごとに追加してください。

### ドキュメント
- 各プロジェクトにはREADME.mdファイルを含め、プロジェクトの概要、セットアップ手順、使用方法、貢献方法などを記載すること。
- 重要な関数やクラスにはそれぞれの開発言語のドキュメント形式のコメントを追加し、使用方法や引数、戻り値を明確にすること。
- その他のドキュメントに関する指示は、プロジェクトごとに追加してください。

### その他のファイル
ライセンスや貢献ガイドライン、変更履歴など、以下のファイルも含めることを推奨します:
- LICENSE: プロジェクトのライセンス情報を記載するファイル
- CONTRIBUTING.md: 貢献ガイドラインを記載するファイル
- CHANGELOG.md: 変更履歴を記載するファイル
- その他の必要なファイルは、プロジェクトごとに指示を追加してください。

## 作成後の完了の条件
- Constructionsで定義したプロジェクト構成に準拠していること。
- Constructions内のpackage.jsonで定義したスクリプトが全て実行できること。
- jestのテストコードをindex.tsを除く全てのモジュール単位で作成し、全てグリーンであること。
- 静的解析とフォーマットを実行し、指摘がないこと。
