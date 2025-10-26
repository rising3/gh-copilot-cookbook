Constructionsを参照し、examples/ts 以下に作成して下さい。

フォルダ名は ts-sample
内容はGitHub Copilotのinstructionsの評価用のサンプルプロジェクト。
必要なパッケージをインストールして以下のソースコードを作って欲しい。

仕様は以下の通り。
- TypeScriptで実装する。
- 四則演算の関数を持ったクラス(Calculator)を別モジュールをして開発する。
- index.tsファイルは、モジュールのエントリーポイントとして機能し、主要なクラスや関数をエクスポートする
- howto.tsでは、開発したCalculatorの動作確認を行い、結果をコンソールに出力する。

達成条件は以下の通り。
- Constructionsで定義したプロジェクト構成に準拠していること。
- Constructions内のpackage.jsonで定義したスクリプトが全て実行できること。
- jestのテストコードをindex.tsを除く全てのモジュール単位で作成し、全てグリーンであること。
- 静的解析とフォーマットを実行し、指摘がないこと。
