# Claude統合環境ガイド

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
- **時間制限なし**: AI使用時間の制限を考慮せずにじっくり編集可能
- **複数AI使い分け**: 用途に応じてClaude、Gemini、その他のAIを選択

### ClaudeCode → Cursor 連携
- ClaudeCodeで作成したコードをCursorで開く
- AIアシスタント機能で品質向上を実行
- **Reject/Accept機能**で細かな段階的修正を実行
- **時間制限なし**でじっくり編集・最適化
- **複数AI使い分け**で用途に応じた最適なAIを選択
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