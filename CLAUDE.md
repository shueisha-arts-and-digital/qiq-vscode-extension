# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

qiq-vscode-extensionは、Qiqテンプレート言語用のVSCode拡張機能です。Qiqは、PHPファイル内で使用される`{{ }}`構文を持つテンプレート言語です。

## プロジェクト構造

```
qiq-vscode-extension/
├── package.json                 # VSCode拡張機能のマニフェスト
├── language-configuration.json  # 言語の基本設定（コメント、ブラケットなど）
└── syntaxes/
    └── qiq.tmLanguage.json     # TextMate文法によるシンタックスハイライト定義
```

## 開発コマンド

### 拡張機能のテスト
- VSCode内で`F5`を押すと、拡張機能がロードされた新しいVSCodeウィンドウが開きます
- 変更後は、デバッグツールバーから再起動するか、`Ctrl+R` (Mac: `Cmd+R`)でウィンドウをリロードできます

### ビルドとパッケージング

1. **vsceのインストール** (初回のみ)
   ```bash
   npm install -g @vscode/vsce
   ```

2. **拡張機能のビルド**
   ```bash
   vsce package
   ```
   これにより `qiq-vscode-extension-0.0.1.vsix` ファイルが作成されます

3. **ビルドした拡張機能のインストール**
   - コマンドラインから: `code --install-extension qiq-vscode-extension-0.0.1.vsix`
   - VSCode GUIから: 拡張機能ビュー → 「...」メニュー → 「VSIXからのインストール...」

### パブリッシュ
- Visual Studio Marketplaceへの公開: https://code.visualstudio.com/docs

## 技術詳細

### 対応ファイル
- `.php`ファイル
- `.qiq.php`ファイル

### Qiq言語の構文
- テンプレートブロック: `{{ }}` で囲まれたコード
- 制御構造: `if/else/elseif/endif`, `for/endfor`, `foreach/endforeach`, `while/endwhile`
- 変数: `$variable` 形式
- PHPネームスペース表記もサポート

### 主要ファイルの役割

**package.json**
- 拡張機能のメタデータと設定
- 言語IDは`qiq`
- ファイル拡張子の関連付け

**language-configuration.json**
- コメントスタイル: `//` (単行)、`/* */` (ブロック)
- ブラケットペア: `{}`, `[]`, `()`
- 自動閉じと囲み機能の設定

**syntaxes/qiq.tmLanguage.json**
- TextMate文法によるシンタックスハイライト
- Qiqテンプレートブロック、制御構造、変数、演算子などのパターン定義

## 注意事項

このプロジェクトは純粋な宣言的VSCode拡張機能のため：
- TypeScript/JavaScriptコードは含まれていません
- ビルドプロセスは不要です
- テストフレームワークは設定されていません
- Language Server Protocolは使用していません（シンタックスハイライトのみ）