# タスク管理UIデザイン仕様

## 概要

レスポンシブ対応のタスク管理インターフェースデザイン仕様。シンプルで直感的な操作性を重視し、モバイルファーストアプローチで設計。

## レイアウト構成

### デスクトップ（1024px以上）
```
┌─────────────────────────────────────────────────┐
│                    Header                       │
├─────────────────────────────────────────────────┤
│  ┌──────────────┐  ┌─────────────────────────┐  │
│  │   Sidebar    │  │      Main Content       │  │
│  │              │  │                         │  │
│  │  - Filters   │  │   ┌─────────────────┐   │  │
│  │  - Actions   │  │   │   Task Form     │   │  │
│  │              │  │   └─────────────────┘   │  │
│  │              │  │                         │  │
│  │              │  │   ┌─────────────────┐   │  │
│  │              │  │   │   Task List     │   │  │
│  │              │  │   │                 │   │  │
│  │              │  │   │   [Task Item]   │   │  │
│  │              │  │   │   [Task Item]   │   │  │
│  │              │  │   │   [Task Item]   │   │  │
│  │              │  │   └─────────────────┘   │  │
│  └──────────────┘  └─────────────────────────┘  │
└─────────────────────────────────────────────────┘
```

### タブレット（768px-1023px）
```
┌─────────────────────────────────────────────────┐
│                    Header                       │
├─────────────────────────────────────────────────┤
│              Filter Bar & Actions               │
├─────────────────────────────────────────────────┤
│                Task Form                        │
├─────────────────────────────────────────────────┤
│                                                 │
│               Task List                         │
│                                                 │
│         [Task Item (expanded)]                  │
│         [Task Item (expanded)]                  │
│         [Task Item (expanded)]                  │
│                                                 │
└─────────────────────────────────────────────────┘
```

### モバイル（767px以下）
```
┌─────────────────┐
│     Header      │
├─────────────────┤
│   Quick Actions │
├─────────────────┤
│   Task Form     │
│   (Collapsible) │
├─────────────────┤
│   Filter Chips  │
├─────────────────┤
│                 │
│   Task List     │
│                 │
│  [Task (card)]  │
│  [Task (card)]  │
│  [Task (card)]  │
│                 │
│                 │
└─────────────────┘
```

## コンポーネント詳細

### 1. Header Component
```
目的: アプリタイトルとグローバルナビゲーション
要素:
- アプリロゴ・タイトル
- ダークモード切り替え (将来拡張用)
高さ: 64px (デスクトップ), 56px (モバイル)
```

### 2. Sidebar Component (デスクトップのみ)
```
目的: フィルタとアクション管理
幅: 280px
要素:
- ステータスフィルタ (All, Todo, In Progress, Done)
- ソート設定 (作成日順, 締切日順)
- 新規タスク作成ボタン
- タスク数統計
```

### 3. Filter Bar Component (タブレット・モバイル)
```
目的: コンパクトなフィルタ操作
要素:
- フィルタチップス (横スクロール可能)
- ソートドロップダウン
- 新規作成FAB (Floating Action Button)
```

### 4. Task Form Component
```
目的: タスクの作成・編集フォーム
状態: 展開/折りたたみ可能
要素:
- タイトル入力 (必須, max 200文字)
- 説明入力 (任意, max 1000文字)
- 締切日選択 (任意)
- 保存/キャンセルボタン
```

### 5. Task List Component
```
目的: タスク一覧表示とソート
機能:
- 仮想スクロール (パフォーマンス対応)
- ドラッグ&ドロップ (将来拡張)
- 空状態メッセージ
```

### 6. Task Item Component
```
目的: 個別タスク表示・操作
レイアウト:
┌─────────────────────────────────────────┐
│ [✓] Task Title              [⋮] Menu    │
│     Description preview...              │
│     📅 Due: 2024-01-01 | Status: Todo   │
│                                         │
│ Actions: [Edit] [Delete] [Status]       │
└─────────────────────────────────────────┘

ステータス表示:
- Todo: グレー背景 + グレーテキスト
- In Progress: 黄色背景 + ダークテキスト  
- Done: 緑背景 + 白テキスト + 取り消し線
```

## レスポンシブブレークポイント

```css
/* モバイル優先 */
.mobile-first {
  /* 基本スタイル: 320px - 767px */
}

@media (min-width: 768px) {
  /* タブレット: 768px - 1023px */
}

@media (min-width: 1024px) {
  /* デスクトップ: 1024px以上 */
}

@media (min-width: 1440px) {
  /* 大画面: 1440px以上 */
  max-width: 1200px;
  margin: 0 auto;
}
```

## カラーパレット

### プライマリカラー
- Primary: `#3B82F6` (青)
- Primary Dark: `#1D4ED8`
- Primary Light: `#93C5FD`

### ステータスカラー
- Todo: `#6B7280` (グレー)
- In Progress: `#F59E0B` (アンバー)
- Done: `#10B981` (緑)

### UIカラー
- Background: `#FFFFFF` / `#F9FAFB`
- Surface: `#FFFFFF`
- Border: `#E5E7EB`
- Text Primary: `#111827`
- Text Secondary: `#6B7280`
- Error: `#EF4444`

## タイポグラフィ

```css
/* フォントファミリー */
font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;

/* サイズスケール */
.text-xs: 12px
.text-sm: 14px
.text-base: 16px
.text-lg: 18px
.text-xl: 20px
.text-2xl: 24px

/* 行間 */
line-height: 1.5 (基本)
line-height: 1.25 (見出し)
```

## スペーシング

```css
/* パディング・マージンスケール */
.space-1: 4px
.space-2: 8px
.space-3: 12px
.space-4: 16px
.space-6: 24px
.space-8: 32px
.space-12: 48px
.space-16: 64px
```

## インタラクション

### ホバー効果
- ボタン: 0.2s ease-in-out transition
- カード: 軽いシャドウ + 3px上昇
- リンク: カラー変更

### フォーカス状態
- アウトライン: 2px solid primary color
- ボックスシャドウ: 0 0 0 3px rgba(59, 130, 246, 0.1)

### ローディング状態
- スケルトンローダー (タスクリスト)
- スピナー (フォーム送信)
- プレースホルダー (空状態)

## アクセシビリティ

### キーボードナビゲーション
- Tab順序: Header → Sidebar/Filter → Form → Task List
- Enter/Space: ボタン実行
- Escape: モーダル・フォームクローズ
- Arrow Keys: リストナビゲーション

### スクリーンリーダー対応
- aria-label: すべてのアクションボタン
- aria-describedby: フォーム入力説明
- role="region": 主要セクション
- live regions: 動的コンテンツ更新

### コントラスト
- テキスト: 最低 4.5:1
- アイコン: 最低 3:1
- フォーカス: 最低 3:1

## パフォーマンス考慮

### 仮想化
- タスクリスト: 50件以上で仮想スクロール
- 画像: 遅延読み込み (将来の添付ファイル機能)

### バンドルサイズ
- Tree shaking対応
- 動的インポート (モーダル等)
- CSS-in-JS最小化

## モバイルUX最適化

### タッチ操作
- タップ領域: 最小44px × 44px
- スワイプジェスチャー: タスク削除/完了
- プルリフレッシュ: リスト更新

### モバイル固有機能
- FAB (Floating Action Button): 新規作成
- ボトムシート: アクションメニュー
- Toast通知: 操作フィードバック

## 状態管理

### ローカル状態
- フォーム入力値
- UI表示状態 (展開/折りたたみ)
- フィルタ・ソート設定

### グローバル状態
- タスクデータ
- ローディング状態
- エラー状態

## エラーハンドリングUI

### バリデーションエラー
- インライン表示 (フォーム入力下)
- 赤色テキスト + アイコン
- スクリーンリーダー対応

### ネットワークエラー
- Toast通知
- 再試行ボタン
- オフライン状態表示

### 空状態
- イラスト + メッセージ
- アクションボタン (新規作成)
- ヘルプテキスト