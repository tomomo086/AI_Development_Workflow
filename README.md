# AI統合ワークフロー - 実践的開発環境

## 🚀 概要

※本ドキュメントはエンジニア経験のない初心者（tomomo086）の主観的な感想・体験を多く含みます。

このリポジトリは、個人での開発で編み出した実際の開発ワークフローにおけるAI活用法を体系化したものです。理論ではなく、実際に使用している開発環境とワークフローを公開しています。

- **Claude統合開発環境**の構築・運用
- **開発効率化ワークフロー**の実践例
- **実証済み環境構築手順**の完全ガイド

### 📊 AI統合ワークフロー図（Gemini生成）

![Gemini生成AI統合ワークフロー図](assets/screenshots/ss_43.png)

*※このフロー図はGeminiで生成されたもので、実際の開発ワークフローを視覚化しています。*

### ⚠️ 重要な注意事項
**AI全般について**: AIが教えてくれることを鵜呑みにせず、批判的思考を忘れずにうまく活用することが、正しい答えにたどり着く方法です。AIは強力なツールですが、人間の判断と検証が不可欠です。

## 💡 特徴

### 各AIツールの主観的な利点・デメリット（初心者視点）

- **Claude Desktop**
  - 利点: チャットUIで視認性が高く直感的に対話可能／MCPによる拡張性で万能性あり／ZapierMCP連携でGoogleドライブ等にスマホからもアクセスしやすい
  - デメリット: 処理速度がやや遅い／ClaudeCodeと比べてプロンプト依存が強く、ファイル操作の現状が分かりにくい／途中停止は強制ストップが必要

- **ClaudeCode**
  - 利点: CLIベースで処理が速い／操作中のファイルが可視化される／途中で許可を求めてくるので進捗管理しやすい
  - デメリット: Cursorほど細かな調整ができない／CLIは初心者には複雑／視覚的に分かりにくい

- **Cursor**
  - 利点: Reject/Acceptによる細かな段階的修正／他のAIは時間ごとの制限があるが、Cursorは月ごとの制限のため制限を気にせず編集できる／複数AIを使い分け可能／リアルタイムエラー検出や自動フォーマットなど細やかな品質向上が可能
  - デメリット: ClaudeCodeほどのスピード感はない／AIの提案精度はプロンプトや文脈に依存する場合あり

※上記はすべてtomomo086（エンジニア未経験・初心者）の主観的な感想です。

### AI開発手法の実践例
- **Claude Desktop**: 開発前のアイデア出し・方向性決定（Grok3も併用）
- **ClaudeCode**: 具体的な実装・フォルダ構造作成
- **FilesystemMCP**: Claude Desktopでのフォルダ・ファイル操作の自動化
- **段階的開発**: アイデア→仕様書→実装の流れ

### Claude二刀流活用 + Cursor統合
- **ClaudeCode**: コマンドライン統合開発
- **Claude Desktop**: FilesystemMCP による自動化
- **FilesystemMCP**: フォルダ・ファイルの作成・編集・操作を自動化
- **Cursor**: 詳細編集・品質向上・最適化作業
  - **Reject/Accept機能**: 細かな段階的修正が可能
  - **時間制限なし**: 他のAIは時間ごとの制限があるが、Cursorは月ごとの制限のため制限を気にせず編集可能
  - **複数AI対応**: Claude、Gemini、その他のAIと使い分け可能

### 統合開発環境
- **WSL2 + Docker**統合開発環境
- **Git + GitHub**連携設定
- **実用レベル**の統合ワークフロー

## 🛠️ 環境構成

### ハードウェア構成

※このPC構成は、趣味であるオンラインゲームを快適に楽しみ、妻とも一緒にプレイできる性能を重視しつつ、開発用途とも両立できるバランスを意識しています。

- **OS**: Windows 11 Pro + WSL2 (Ubuntu 22.04.5 LTS)
- **CPU**: AMD Ryzen 7 7700X
- **GPU**: RX 7800 XT
- **RAM**: 32GB DDR5

### ソフトウェアスタック
- **AI環境**: 
  - Claude: ClaudeCode + Claude Desktop (FilesystemMCP) - メイン運用
  - Gemini: Google AI Pro - 検証中
  - Grok3: アイデア出し時の併用
- **開発ツール**:
  - Git: 2.49.0 + SSH鍵 (ED25519)
  - Node.js: v22.16.0 + npm 10.9.2
  - Docker: Desktop 28.1.1 + WSL2統合
  - Cursor: Git統合・Claude連携・AIアシスタント機能・Reject/Accept機能・複数AI対応

## 🔄 開発ワークフロー

### 1. アイデア出し・方向性決定
- **Claude Desktop**を使用して大まかな方向性を決定
- 必要に応じて**Grok3**も併用してアイデアを発展
- **FilesystemMCP**でフォルダ・ファイルの初期作成も実行
- 開発前の戦略立案と要件整理

![Claude Desktopでのアイデア出し](assets/screenshots/ss_01.png)

![アイデア出しと方向性決定の進行状況](assets/screenshots/ss_40.png)

### 2. 仕様書作成
- ローカルの`dev/projects`フォルダ内に仕様書を作成
- ClaudeCodeが理解しやすい形式で情報を整理
- 実装に必要な詳細情報を体系的にまとめる

![仕様書作成とClaudeCode用資料準備](assets/screenshots/ss_02.png)

![ClaudeCode実装用仕様書の詳細内容](assets/screenshots/ss_03.png)

### 3. 実装・フォルダ構造作成
- **PowerShell**で`projects`フォルダに移動
- **ClaudeCode**を起動して仕様書を参照
- 仕様書の内容を元にフォルダ構造を自動生成
- 段階的なタスク実行と進捗管理

![フォルダ構造作成の進行状況](assets/screenshots/ss_07.png)

![ClaudeCodeでのタスク実行](assets/screenshots/ss_09.png)

![実装完了とファイル作成確認](assets/screenshots/ss_10.png)

![段階的タスク実行と進捗管理の進行状況](assets/screenshots/ss_13.png)

### 4. Cursorでの詳細編集・品質向上・最適化作業
- **GitHub Desktop**でローカルリポジトリの状態を確認
- **Cursor**でプロジェクトを開いて詳細編集を実行
  - **AIアシスタント機能**を活用したコード品質向上
  - **リアルタイムエラー検出**と修正提案
  - **自動フォーマット**とコーディング規約適用
  - **インテリセンス機能**による効率的なコーディング
- **AIアシスタント**を使用してMITライセンスファイルを自動生成
- 写真配置ファイルの作成とファイル名の最適化
- 段階的なファイル管理とコミット準備
- **コードレビュー**: AIアシスタントによる自動コードレビュー
- **パフォーマンス最適化**: ボトルネック検出と改善提案
- **セキュリティチェック**: 脆弱性検出と修正提案
- **ドキュメント整備**: README、コメント、API文書の自動生成・更新
- **テスト強化**: ユニットテスト、統合テストの自動生成
- **依存関係管理**: パッケージ更新とセキュリティ修正
- **Reject/Accept機能**: 細かな段階的修正による高品質なコード生成
- **時間制限なし**: 他のAI（Claude、Gemini等）は時間ごとの制限があるが、Cursorは月ごとの制限のため、制限を気にせずにじっくり編集可能
- **複数AI使い分け**: 用途に応じてClaude、Gemini、その他のAIを選択

![GitHub Desktopでのローカルリポジトリ状態確認](assets/screenshots/ss_22.png)

![Cursorでのプロジェクト編集開始](assets/screenshots/ss_23.png)

![AIアシスタントでのMITライセンス作成依頼](assets/screenshots/ss_25.png)

![MITライセンスファイルの作成と確認](assets/screenshots/ss_26.png)

![GitHub DesktopでのMITライセンス関連ファイルコミット](assets/screenshots/ss_28.png)

![GitHub Desktopでのプッシュ準備状態](assets/screenshots/ss_29.png)

![AIアシスタントでの写真配置ファイル作成依頼](assets/screenshots/ss_31.png)

![写真配置ファイルの作成と設定](assets/screenshots/ss_32.png)

![写真ファイル名の短縮処理実行](assets/screenshots/ss_33.png)

![ファイル名変更の実行と確認](assets/screenshots/ss_35.png)

![変更されたファイル構造の確認](assets/screenshots/ss_36.png)

![最終的なファイル構造と管理状態](assets/screenshots/ss_39.png)

![CursorでのAIアシスタント活用によるコード品質向上](assets/screenshots/ss_23.png)

### 5. GitHubへの公開
- **GitHub Desktop**でローカルリポジトリの状態を確認
- リポジトリ名、説明、プライベート設定を指定してGitHubにパブリッシュ
- 公開されたリポジトリの確認と初期コミットの確認
- 開発成果の共有とバージョン管理の開始
- **メインブランチ直接コミット**: AI活用のワークフローはプログラムのコードとは異なり、間違えても損害が少なくAIで容易に修正できるため、あえてメインブランチに直接コミット

![GitHub Desktopでのローカルリポジトリ状態確認](assets/screenshots/ss_15.png)

![GitHub Desktopでのリポジトリパブリッシュ設定](assets/screenshots/ss_19.png)

![リポジトリパブリッシュ設定の詳細](assets/screenshots/ss_20.png)

![GitHub上での公開されたリポジトリ確認](assets/screenshots/ss_21.png)

## 📖 ドキュメント

### 詳細ガイド
- [Claude統合環境](docs/claude-integration.md) - ClaudeCode + Claude Desktop使い分け戦略
- [開発環境構築](docs/development-setup.md) - WSL2 + Docker環境構築手順
- [ワークフロー概要](docs/workflow-overview.md) - 実践的開発ワークフロー
- [Gemini検証記録](docs/gemini-evaluation.md) - Gemini活用検証

## 📊 検証・評価

### 開発効率改善実績
- 開発時間の大幅短縮を実現
- 自動化によるヒューマンエラーの削減
- 実用レベルでの継続運用中

### Gemini活用検証（進行中）
- 2025-07-25より検証開始
- Claude比較での使用感評価
- 物理作業支援での活用可能性検証
- **ElegooSlicer一時停止方法の教示**: GeminiにElegooSlicerの一時停止方法を教えてもらえた実例
- **視覚認識・物体世界知識の優位性**: Claudeと比較して、Geminiの方が視覚認識と物体世界に対する知識が広く、助言の質が高い（結果が証明済み）
- **フロー図生成能力**: AI統合ワークフローの視覚化に成功し、開発プロセスの理解促進に効果的

![GeminiでのElegooSlicer一時停止方法の教示](assets/screenshots/ss_41.png)

## 🔧 クイックスタート

1. **ドキュメント確認**
- [開発環境構築ガイド](docs/development-setup.md)を参照
- 環境に応じて設定手順を実行

2. **Claude統合設定**
- [Claude統合環境ガイド](docs/claude-integration.md)を参照
- ClaudeCode + Claude Desktop設定

## 📝 ライセンス

このプロジェクトはMITライセンスの下で公開されています。詳細は[LICENSE](LICENSE)ファイルを参照してください。

## 🤝 コントリビューション

このリポジトリは個人での開発で編み出した主観的なワークフロー記録です。

---

**実際の開発環境で使用している設定とワークフローを公開しています。転職活動でのポートフォリオとしても活用中。**
