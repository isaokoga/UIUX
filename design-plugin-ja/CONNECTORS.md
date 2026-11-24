# コネクタ

## ツール参照の仕組み

プラグインのファイルでは、`~~category`（カテゴリ）を、ユーザーがそのカテゴリで連携したツールを指すプレースホルダとして使用します。たとえば `~~design tool` は、Figma、Sketch、あるいは MCP サーバーを持つ任意のデザインツールを指します。

プラグインは**ツール非依存（tool-agnostic）**です。特定の製品名ではなく、カテゴリ（デザインツール、プロジェクトトラッカー、ユーザーフィードバックなど）の観点でワークフローを記述します。`.mcp.json` は特定の MCP サーバーを事前設定していますが、そのカテゴリに属する任意の MCP サーバーが利用できます。

## このプラグインのコネクタ

| カテゴリ | プレースホルダ | 同梱サーバー | その他の選択肢 |
|----------|-------------|-----------------|---------------|
| チャット | `~~chat` | Slack | Microsoft Teams |
| デザインツール | `~~design tool` | Figma | Sketch、Adobe XD、Framer |
| ナレッジベース | `~~knowledge base` | Notion | Confluence、Guru、Coda |
| プロジェクトトラッカー | `~~project tracker` | Linear、Asana、Atlassian（Jira/Confluence） | Shortcut、ClickUp |
| ユーザーフィードバック | `~~user feedback` | Intercom | Productboard、Canny、UserVoice、Dovetail |
| プロダクトアナリティクス | `~~product analytics` | — | Amplitude、Mixpanel、Heap、FullStory |
