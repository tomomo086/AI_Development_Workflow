# 開発環境構築ガイド

※本ドキュメントはエンジニア未経験からAI(LLM)活用を実践する中で編み出した、独自の開発ワークフローを体系化したものです。理論だけでなく、個人の試行錯誤から生まれたリアルな知見を共有します。

## 概要

WSL2 + Docker + Git統合による開発環境の構築手順を詳細に説明します。

> **関連ドキュメント**:
> - [Claude統合環境](claude-integration.md) - ClaudeCode + Claude Desktopの使い分け戦略
> - [ワークフロー概要](workflow-overview.md) - 構築した環境での実践的ワークフロー
> - [Gemini検証記録](gemini-evaluation.md) - 構築済み環境でのGemini検証

### ⚠️ 重要な注意事項
**AI(LLM)全般について**: AI(LLM)が教えてくれることを鵜呑みにせず、批判的思考を忘れずに自分でも調べてAI(LLM)の舵を取ることが、正しい答えにたどり着く方法だと思いました。AI(LLM)は強力なツールですが、人間の判断と検証が不可欠です。

## ワークフローの核心コンセプト
私のワークフローの核心は、アイデア出しと自動化の『Claude Desktop』、高速な実装の『ClaudeCode』、そして**最終的な品質向上の『Cursor』**という3つのツールを連携させることです。この『適材適所』の使い分けにより、開発プロセス全体を効率化します。

## 🛠️ 環境構成

### ハードウェア構成

※このPC構成は、趣味であるオンラインゲームを快適に楽しみ、妻とも一緒にプレイできる性能を重視しつつ、開発用途とも両立できるバランスを意識しています。

- **OS**: Windows 11 + WSL2 (Ubuntu 22.04.5 LTS)
- **CPU**: AMD Ryzen 7 7700X
- **GPU**: RX 7800 XT
- **RAM**: 32GB DDR5

### ソフトウェアスタック
- **AI(LLM)環境**: 
  - Claude: ClaudeCode + Claude Desktop (FilesystemMCP) - メイン運用
  - Gemini: Google AI(LLM) Pro - 検証中
  - Grok3: アイデア出し時の併用
  - BlendrMCP: Claude DesktopでのBlender統合・3Dモデリング支援
- **開発ツール**:
  - Git: 2.49.0 + SSH鍵 (ED25519)
  - Node.js: v22.16.0 + npm 10.9.2
  - Docker: Desktop 28.1.1 + WSL2統合
  - Cursor: Git統合・Claude連携・AI(LLM)アシスタント機能・Reject/Accept機能・複数AI(LLM)対応

### WSL2 + Ubuntu環境構築

#### 1. WSL2有効化
```powershell
# PowerShellを管理者権限で実行
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

# 再起動後
wsl --set-default-version 2
```

#### 2. Ubuntu インストール
```bash
# Microsoft Store から Ubuntu 22.04.5 LTS をインストール
# または
wsl --install -d Ubuntu-22.04
```

#### 3. 基本設定
```bash
# パッケージ更新
sudo apt update && sudo apt upgrade -y

# 必要なツールインストール
sudo apt install -y curl wget git build-essential
```

## Docker Desktop統合

### インストール手順
1. [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop) をダウンロード
2. インストール時に「Use WSL 2 instead of Hyper-V」を選択
3. Settings → Resources → WSL Integration でUbuntuを有効化

### 動作確認
```bash
# WSL2内で実行
docker --version
docker run hello-world
```

## Git + GitHub連携

### SSH鍵生成（ED25519）
```bash
# SSH鍵生成
ssh-keygen -t ed25519 -C "your-email@example.com"

# SSH Agent起動
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# 公開鍵をGitHubに登録
cat ~/.ssh/id_ed25519.pub
```

### Git設定
```bash
# ユーザー情報設定
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"

# デフォルトブランチ設定
git config --global init.defaultBranch main

# エディタ設定
git config --global core.editor "code --wait"
```

## Node.js環境

### Node.js インストール（nvm使用）
```bash
# nvm インストール
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc

# 最新LTS版インストール
nvm install --lts
nvm use --lts

# バージョン確認
node --version  # v22.16.0
npm --version   # 10.9.2
```

### グローバルパッケージ
```bash
# よく使うパッケージをグローバルインストール
npm install -g @modelcontextprotocol/server-filesystem
npm install -g typescript
npm install -g nodemon
```

## 統合開発環境

### VSCode + Remote-WSL
```bash
# VSCode Extensions
code --install-extension ms-vscode-remote.remote-wsl
code --install-extension ms-vscode.vscode-json
code --install-extension bradlc.vscode-tailwindcss
```

### Cursor設定
- **Claude連携設定**: AIアシスタント機能の有効化
- **Git統合設定**: コミット・プッシュ・ブランチ管理
- **WSL2アクセス設定**: リモート開発環境への接続
- **AI機能設定**: 
  - コードレビュー機能の有効化
  - 自動フォーマット設定
  - インテリセンス機能の最適化
  - リアルタイムエラー検出設定
  - Reject/Accept機能の有効化
  - 複数AI(LLM)プロバイダーの設定（Claude、Gemini等）
- **利点**: 
  - 細かな段階的修正が可能
  - 用途に応じたAI(LLM)使い分けが可能

## トラブルシューティング

### よくある問題

#### WSL2メモリ使用量制限
```bash
# .wslconfig ファイル作成（C:\Users\%USERNAME%\.wslconfig）
[wsl2]
memory=16GB
processors=8
```

#### Docker Desktop起動エラー
```bash
# WSL2バージョン確認
wsl --list --verbose

# WSL2再起動
wsl --shutdown
```

#### SSH接続エラー
```bash
# SSH Agent確認
ssh-add -l

# GitHub接続テスト
ssh -T git@github.com
```

## パフォーマンス最適化

### WSL2最適化
- ファイルはWSL2内で作業（/home/username/projects/）
- Windowsファイルシステム（/mnt/c/）への頻繁アクセスを避ける

### Docker最適化
- WSL2統合を使用
- Docker Desktop設定でリソース制限を適切に設定

## 環境確認コマンド

```bash
# 環境情報一括確認
echo "=== System Info ==="
lsb_release -a
echo "=== WSL Version ==="
wsl --version
echo "=== Docker ==="
docker --version
echo "=== Node.js ==="
node --version
npm --version
echo "=== Git ==="
git --version
```

この環境構築により、AI統合開発環境の基盤が完成します。

## 次のステップ

環境構築完了後は、以下のドキュメントで実際の開発ワークフローを学んでください：

1. **[Claude統合環境ガイド](claude-integration.md)** - ClaudeCode + Claude Desktopの使い分け戦略を理解
2. **[ワークフロー概要](workflow-overview.md)** - 実践的な開発フローを体験
3. **[Gemini検証記録](gemini-evaluation.md)** - 追加のAIツール検証でさらなる品質向上
