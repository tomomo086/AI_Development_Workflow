# Claude統合環境ガイド

※本ドキュメントはエンジニア未経験からAI(LLM)活用を実践する中で編み出した、独自の開発ワークフローを体系化したものです。理論だけでなく、個人の試行錯誤から生まれたリアルな知見を共有します。

## 各AI(LLM)ツールの主観的な利点・デメリット（実践的視点）

- **Claude Desktop**
  - 利点: チャットUIで視認性が高く直感的に対話可能／MCPによる拡張性で万能性あり／ZapierMCP連携でGoogleドライブ等にスマホからもアクセスしやすい
  - デメリット: 処理速度がやや遅い／ClaudeCodeと比べてプロンプト依存が強く、ファイル操作の現状が分かりにくい／途中停止は強制ストップが必要

- **ClaudeCode**
  - 利点: CLIベースで処理が速い／操作中のファイルが可視化される／途中で許可を求めてくるので進捗管理しやすい
  - デメリット: Cursorほど細かな調整ができない／CLIは初心者には複雑／視覚的に分かりにくい

- **Cursor**
  - 利点: Reject/Acceptによる細かな段階的修正／複数AI(LLM)を使い分け可能／リアルタイムエラー検出や自動フォーマットなど細やかな品質向上が可能
  - デメリット: ClaudeCodeほどのスピード感はない／AI(LLM)の提案精度はプロンプトや文脈に依存する場合あり

※上記はすべてtomomo086（エンジニア未経験から実践で習得）の主観的な感想です。

## 概要

ClaudeCode + Claude Desktop の二刀流活用による開発環境統合について説明します。

## ClaudeCode vs Claude Desktop 使い分け戦略

### ClaudeCode（コマンドライン）
- **コーディング作業**: ファイル編集、デバッグ、テスト実行
- **プロジェクト管理**: Git操作、ファイル操作
- **環境構築**: 設定ファイル作成、依存関係管理

### Claude Desktop（GUI + MCP）
- **ファイル管理**: FilesystemMCP による一括操作
- **ドキュメント作成**: README、仕様書作成
- **計画・設計**: アーキテクチャ設計、タスク管理

## Cursor連携

### Cursorでの詳細編集ワークフロー
- **コードレビュー**: AIアシスタントによる自動レビュー
- **パフォーマンス最適化**: ボトルネック検出と改善提案
- **セキュリティチェック**: 脆弱性検出と修正提案
- **テスト生成**: ユニットテスト・統合テストの自動生成
- **ドキュメント整備**: コメント、API文書の自動生成
- **Reject/Accept機能**: 細かな段階的修正による高品質なコード生成
- **複数AI(LLM)対応**: 用途に応じてClaude、Gemini、その他のAI(LLM)と使い分け可能

### ClaudeCode → Cursor 連携
- ClaudeCodeで作成したコードをCursorで開く
- AIアシスタント機能で品質向上を実行
- **Reject/Accept機能**で細かな段階的修正を実行
- **複数AI(LLM)対応**で用途に応じた最適なAI(LLM)を選択
- 修正・最適化後にGitHub Desktopでコミット

## FilesystemMCP 活用

### 設定方法
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem"],
      "env": {
        "ALLOWED_DIRECTORIES": "C:\\Users\\tomon\\dev\\projects"
      }
    }
  }
}
```

### 活用例
- プロジェクト全体のファイル一覧取得
- 設定ファイルの一括更新
- ドキュメント間のリンク管理

## 統合ワークフロー

### 開発フェーズ
1. **設計**: Claude Desktop でアーキテクチャ設計
2. **実装**: ClaudeCode でコーディング
3. **詳細編集**: Cursor でコード品質向上・最適化
4. **テスト**: ClaudeCode でテスト実行
5. **ドキュメント**: Claude Desktop でドキュメント更新

### 実際のコマンド例
```bash
# ClaudeCode での典型的な開発フロー
claude code
> プロジェクトを分析して、新機能の実装方針を提案してください
> tests/test_feature.py を作成してテストを追加
> npm test で動作確認
```

## トラブルシューティング

### 一般的な問題と解決策
- **MCP接続エラー**: Node.js バージョン確認
- **ファイルアクセス権限**: ALLOWED_DIRECTORIES 設定確認
- **日本語文字化け**: UTF-8 エンコーディング設定

詳細は [開発環境構築ガイド](development-setup.md) を参照してください。