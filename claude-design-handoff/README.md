# Claude Code の design-handoff スキルで開発者向け仕様書を作る

> 出典: [claude-media.com — Claude Codeのdesign-handoffスキル](https://claude-media.com/articles/claude-code-design-handoff-skill)
> 本ファイルは上記記事の内容をまとめたものです。

デザインから開発者向け仕様書を自動生成する Claude Code の「design-handoff」スキルについて、導入から活用までをまとめます。

---

## 1. design-handoff の位置づけ

- **提供元**: Anthropic の `knowledge-work-plugins` リポジトリの `design` プラグイン
- **役割**: 「デザインから開発者向け仕様書を作る」スキル
- **対応ツール**: Figma など複数のデザインツール

---

## 2. 導入と呼び出し方

### インストール

```bash
claude plugin marketplace add anthropics/knowledge-work-plugins
claude plugin install design@knowledge-work-plugins
```

### スラッシュコマンドでの呼び出し

```
/design:design-handoff https://www.figma.com/design/xxxx/checkout-flow
```

### 注意点

- コマンド名は `/design-handoff` ではなく、プラグイン名前空間付きの **`/design:design-handoff`**。
- 複数語の説明を渡すときは引用符で囲む:

```
/design:design-handoff "注文確認画面: 商品リスト..."
```

---

## 3. 出力される仕様書の構造

生成される仕様書は、おおむね次の節で構成されます。

| 節 | 内容 |
|---|---|
| Overview / Layout | 画面の目的、グリッド、ブレークポイント |
| Design Tokens Used | トークン名・値・使いどころの表 |
| Components | コンポーネント・バリアント・props |
| States and Interactions | 要素ごとの状態と挙動 |
| Responsive / Edge Cases | ブレークポイント別の変更点 |
| Animation / Motion | 要素・トリガー・動き・ミリ秒 |
| Accessibility Notes | フォーカス順・ARIA ラベル・キーボード操作 |

---

## 4. スキルが従う 4 つの原則

1. **完全性** — 「指定のないものは開発者が推測する。だから全部を指定する」
2. **トークン化** — 値ではなくトークン名で記述する（`16px` ではなく `spacing-md`）
3. **全状態の列挙** — 既定・ホバー・押下・無効・読み込み・エラー・空状態をすべて示す
4. **理由の記述** — 設計判断の背景を説明し、開発者の自己判断を助ける

---

## 5. 効果的な渡し方

### 3 つのヒント

1. **Figma リンクを渡す**
2. **エッジケースを明示する**（例: 「商品が 100 件あったら?」）
3. **技術スタックを伝える**（例: 「React + Tailwind」）

### 実装例

```
/design:design-handoff "https://www.figma.com/design/xxxx/checkout-flow
スタックは React + Tailwind。
エッジケース: 商品が100件のとき、クーポンが無効のとき、決済APIが遅いとき"
```

### CLAUDE.md でのトークン規約設定例

```markdown
## デザイントークン
- 色・余白・文字は tailwind.config.ts の theme に定義した名前で書く
- 仕様書では値を直接書かず、トークン名で参照する
- 新しいトークンが必要な場合は末尾に「追加提案」として分ける
```

---

## 6. 仕様書の活用方法

- **保存**: 依頼文に「`docs/specs/checkout.md` に保存して」と書くと、ファイルとして残せる。
- **実装確認**: 状態表と実装コードを突き合わせ、欠けた状態を機械的に検出する。
- **往復検証**: 仕様と実装が食い違ったら、実装だけでなく仕様書側の曖昧さも検討する。

---

## 7. 隣のスキルとの使い分け

| 場面 | 推奨スキル |
|---|---|
| 画面案の改善点が欲しい | `design-critique` |
| トークン・命名の揺れを洗い出す | `design-system` |
| アクセシビリティを確認したい | `accessibility-review` |
| エラー文言・空状態文言を作りたい | `ux-copy` |
| 開発者向け仕様書を作りたい | `design-handoff` |

---

## まとめ

design-handoff の価値は、単なる雛形出力ではなく、**全状態・全ブレークポイント・判断理由まで記述させる設計原則**にあります。Figma 接続とエッジケースの明示によって、出力される仕様書の品質が大きく向上する点が実用的です。
