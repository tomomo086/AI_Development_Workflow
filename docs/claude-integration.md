# Claude統合環境ガイド

※本ドキュメントはエンジニア未経験からAI(LLM)活用を実践する中で編み出した、独自の開発ワークフローを体系化したものです。理論だけでなく、個人の試行錯誤から生まれたリアルな知見を共有します。

## 各AI(LLM)ツールの主観的な利点・デメリット（実践的視点）

- **Claude Desktop**
  - 利点: チャットUIで視認性が高く直感的に対話可能／MCPによる拡張性で万能性あり／ZapierMCP連携でGoogleドライブ等にスマホからもアクセスしやすい
  - デメリット: 処理速度がやや遅い／ファイル操作の現状が分かりにくい／途中停止は強制ストップが必要

- **ClaudeCode**
  - 利点: CLIベースで処理が速い／操作中のファイルが可視化される／途中で許可を求めてくるので進捗管理しやすい
  - デメリット: Cursorほど細かな調整ができない／CLIは初心者には複雑／視覚的に分かりにくい

- **Cursor**
  - 利点: Reject/Acceptによる細かな段階的修正／複数AI(LLM)を使い分け可能／リアルタイムエラー検出や自動フォーマットなど細やかな品質向上が可能
  - デメリット: ClaudeCodeほどのスピード感はない／AI(LLM)の提案精度はプロンプトや文脈に依存する場合あり

※上記はすべてtomomo086（エンジニア未経験から実践で習得）の主観的な感想です。

### ⚠️ 重要な注意事項
**AI(LLM)全般について**: AI(LLM)が教えてくれることを鵜呑みにせず、批判的思考を忘れずに自分でも調べてAI(LLM)の舵を取ることが、正しい答えにたどり着く方法だと思いました。AI(LLM)は強力なツールですが、人間の判断と検証が不可欠です。

## ワークフローの核心コンセプト
私のワークフローの核心は、アイデア出しと自動化の『Claude Desktop』、高速な実装の『ClaudeCode』、そして**最終的な品質向上の『Cursor』**という3つのツールを連携させることです。この『適材適所』の使い分けにより、開発プロセス全体を効率化します。

## 概要

ClaudeCode + Claude Desktop の二刀流活用による開発環境統合について説明します。

> **関連ドキュメント**:
> - [ワークフロー概要](workflow-overview.md) - 実践的開発ワークフロー全体の流れ
> - [開発環境構築](development-setup.md) - WSL2 + Docker環境構築手順
> - [Gemini検証記録](gemini-evaluation.md) - Gemini活用検証の進捗

## AI(LLM)開発手法の実践例
- **Claude Desktop**: 開発前のアイデア出し・方向性決定（Grok3も併用）
- **ClaudeCode**: 具体的な実装・フォルダ構造作成
- **FilesystemMCP**: Claude Desktopでのフォルダ・ファイル操作の自動化
- **BlendrMCP**: Claude DesktopでのBlender統合・3Dモデリング支援
  - **[Honeycomb_Coaster - BlendrMCP活用例](https://github.com/tomomo086/Honeycomb_Coaster)** - 3Dモデリングプロジェクトの実践例
  - **幾何学図形・用途限定**: 基本的な幾何学図形の生成や用途が限定的な場面で効果を発揮
  - **アドオン連携**: SketchfabやHyper3Dなどのアドオンとの連携により、より高度な機能を活用可能
  - **デザイン適性**: 機械設計よりもキャラクターや有機的なデザインの作成に適している
- **段階的開発**: アイデア→仕様書→実装の流れ







## Claude二刀流活用 + Cursor統合
- **ClaudeCode**: コマンドライン統合開発
- **Claude Desktop**: FilesystemMCP による自動化
- **FilesystemMCP**: フォルダ・ファイルの作成・編集・操作を自動化
- **BlendrMCP**: Blender統合・3Dモデリング支援・自動化
- **Cursor**: 詳細編集・品質向上・最適化作業
  - **Reject/Accept機能**: 細かな段階的修正が可能
  - **複数AI(LLM)対応**: Claude、Gemini、その他のAI(LLM)と使い分け可能

## 統合開発環境
- **WSL2 + Docker**統合開発環境 → [詳細な構築手順](development-setup.md#wsl2--ubuntu環境構築)
- **Git + GitHub**連携設定 → [SSH鍵設定手順](development-setup.md#git--github連携)
- **実用レベル**の統合ワークフロー → [完全なワークフロー手順](workflow-overview.md#実践的ai統合開発ワークフロー)

## 継続的改善による品質向上

Claude統合環境では、**基本はどこに戻ってもいい**という柔軟性を重視しています：

- **Claude Desktop** ↔ **ClaudeCode** ↔ **Cursor** の自由な往復
- 任意のタイミングでの改善サイクル実行
- 人間がAIに適切な指示と情報を渡すための繰り返し改善

詳細なサイクル回し手法については[ワークフロー概要の継続的改善セクション](workflow-overview.md#6-継続的改善とブランチ戦略)を参照してください。

