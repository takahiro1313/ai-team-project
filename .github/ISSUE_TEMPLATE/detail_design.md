---
name: 詳細設計
about: モジュール設計・API仕様・デザインシステムを定義する
title: "[DD] "
labels: detail-design, gate-3-pending
assignees: ''
---

## 対応する基本設計

Closes #

## モジュール設計（Engineerが記入）

### モジュール構成

<!-- 各モジュールの責務を明記 -->

| モジュール | 責務 | 依存先 |
|-----------|------|--------|
| | | |

### ディレクトリ構成

```
src/
├── app/           # エントリポイント
├── features/      # 機能ごとのモジュール
│   ├── auth/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── api/
│   │   └── types.ts
│   └── dashboard/
├── shared/        # 共通ユーティリティ
│   ├── components/
│   ├── hooks/
│   └── utils/
└── infrastructure/ # 外部サービス連携
```

### API仕様

<!-- OpenAPI形式 or テーブル形式で記載 -->

| Method | Path | 概要 | Request | Response | 認証 |
|--------|------|------|---------|----------|------|
| GET | /api/v1/xxx | | | | 要 |
| POST | /api/v1/xxx | | | | 要 |

### エラーハンドリング方針

| エラー種別 | HTTPステータス | レスポンス形式 |
|-----------|---------------|---------------|
| バリデーション | 400 | `{ error: { code, message, details[] } }` |
| 認証エラー | 401 | `{ error: { code, message } }` |
| サーバーエラー | 500 | `{ error: { code, message, request_id } }` |

### ブランチ戦略

```
main ← tag: v1.0.0 (semver)
  └── develop
       ├── feature/impl-001-xxx
       ├── fix/bug-002-xxx
       └── hotfix/sec-003-xxx
```

- feature/* → develop: squash merge
- develop → main: merge commit + tag

### コーディング規約

<!-- 主要なルールだけ記載。詳細はlint設定に委ねる -->

- 命名: camelCase (変数/関数), PascalCase (型/クラス), UPPER_SNAKE (定数)
- 関数: 20行以内。超えたら分割検討
- ネスト: 3段まで。早期リターンで平坦化
- コメント: 「なぜ」を書く。「何を」はコードで表現

## デザインシステム（Designerが記入）

### カラートークン

| トークン名 | Light | Dark | 用途 |
|-----------|-------|------|------|
| `--color-primary` | | | ブランドカラー |
| `--color-bg-primary` | #FFFFFF | #0A0A0A | 背景 |
| `--color-text-primary` | #1A1A1A | #F5F5F5 | テキスト |
| `--color-success` | | | 成功状態 |
| `--color-error` | | | エラー状態 |

### タイポグラフィ

| トークン名 | size | weight | line-height | 用途 |
|-----------|------|--------|-------------|------|
| `--text-h1` | 32px | 700 | 1.2 | ページタイトル |
| `--text-h2` | 24px | 600 | 1.3 | セクション見出し |
| `--text-body` | 16px | 400 | 1.6 | 本文 |
| `--text-caption` | 12px | 400 | 1.4 | 補足テキスト |

### スペーシング

4px基準グリッド: `4 / 8 / 12 / 16 / 24 / 32 / 48 / 64`

### コンポーネント一覧

| コンポーネント | バリアント | ステート |
|--------------|-----------|---------|
| Button | primary / secondary / ghost | default / hover / active / disabled / loading |
| Input | text / password / search | default / focus / error / disabled |
| Card | default / interactive | default / hover |

### ブレイクポイント

| 名前 | 幅 | 用途 |
|------|-----|------|
| mobile | 〜767px | スマートフォン |
| tablet | 768〜1023px | タブレット |
| desktop | 1024px〜 | デスクトップ |

## ログ設計（Engineerが記入）

| レベル | 用途 | 例 |
|--------|------|-----|
| ERROR | 回復不可能なエラー | DB接続失敗 |
| WARN | 回復可能だが注意が必要 | リトライ発生 |
| INFO | 正常な業務イベント | ユーザーログイン |
| DEBUG | 開発用の詳細情報 | リクエストパラメータ |

---

### Gate 3 チェックリスト

- [ ] モジュール構成が基本設計と整合している（CTO承認）
- [ ] API仕様が全ユーザーストーリーをカバーしている
- [ ] エラーハンドリング方針が定義されている
- [ ] デザインシステムが定義されている（Designer承認）
- [ ] ブランチ戦略が合意されている
- [ ] テスト計画が策定されている（SET承認 ← 別Issue参照）

> 全チェック通過後 → `gate-3-approved` ラベルを付与
