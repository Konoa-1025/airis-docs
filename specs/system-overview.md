# System Overview (airis) JP

## 目的
- すべてのショート動画をユーザーがAIで生成し、ユーザーが**視聴**と**投稿**の両方を楽しめる。

## コンポーネント（概略：UGC前提）
- **Web/App フロント**：視聴/投稿UI、アカウント、通知
- **Upload/Ingestion Service**：動画アップロード、メタ生成、転送/検証
- **Content Service**：作品メタ、タグ、検索
- **Moderation Service**：自動判定＋人手レビュー（詳細→ content-policy.md）
- **Watermark/Attribution Validator**：Sora2透かし等の検証、出典の整合性チェック
- **Storage/CDN**：動画/サムネ配信（転送・トランスコード含む）
- **Analytics/Events**：行動ログ、KPI

## 非機能要件（初期）
- 利用者体験：体感1〜2秒で主要UIが可視、生成は非同期表示
- 可用性：SLO 99.9%
- セキュリティ：公開鍵/署名、RBAC、PII保護、監査ログ
- コンプライアンス：著作権・利用規約準拠（詳細は別紙）

# System Overview (airis) EN

## Purpose
- Enable users to generate all short videos using AI, allowing them to enjoy both **viewing** and **posting**.

## Components (Overview: UGC-centric)
- **Web/App Frontend**: Viewing/Posting UI, Accounts, Notifications
- **Upload/Ingestion Service**: Video Upload, Meta Generation, Transfer/Verification
- **Content Service**: Work Metadata, Tags, Search
- **Moderation Service**: Automated Detection + Manual Review (Details → content-policy.md)
- **Watermark/Attribution Validator**: Verifies Sora2 watermarks, checks source integrity
- **Storage/CDN**: Video/thumbnail delivery (includes transfer and transcoding)
- **Analytics/Events**: User behavior logs, KPIs

## Non-Functional Requirements (Initial)
- User Experience: Primary UI visible within 1-2 seconds, asynchronous generation display
- Availability: SLO 99.9%
- Security: Public keys/signatures, RBAC, PII protection, audit logs
- Compliance: Copyright and Terms of Service adherence (details in separate document)

Translated with DeepL.com
