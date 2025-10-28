# アップロード取込パイプライン（UGC Ingestion）

## 目的
ユーザーが Sora2 等で作成した動画を安全・確実に受け取り、検証・変換・配信可能にする。

## 受付〜公開の流れ
1. **クライアント検証**：拡張子/概算サイズ/長さの事前チェック
2. **一時保存**：オリジナルを一時バケットに格納（ウイルス/マルウェアスキャン）
3. **メタ抽出**：解像度/フレームレート/長さ/コーデック/ハッシュ
4. **透かし・出典検証**（Watermark/Attribution Validator）
5. **コンプライアンス検査**（自動モデレーション：NSFW/暴力/著作権リスクヒント）
6. **トランスコード**：配信用（HLS/DASH）、サムネ/プレビュー生成
7. **審査待ち/公開**：ポリシー閾値によって自動公開 or 人手レビュー待ち
8. **CDN配置**：公開後にCDNへ伝播
9. **監査ログ**：全ステップで request_id を伝搬、不可変ログへ書き込み

## 非同期設計
- 受付APIは**ジョブID**を返し、進捗はポーリング/プッシュ通知
- 失敗時は再試行（exponential backoff）、致命的失敗はデッドレターキュー

## Mermaid（簡易）
```mermaid
flowchart TD
  U[User Upload] --> V{Client pre-check}
  V --> I[(Temp Storage)]
  I --> S[Security Scan]
  S --> M[Metadata Extractor]
  M --> W[Watermark/Attribution]
  W --> R{Policy/Moderation}
  R -- OK --> T[Transcode]
  R -- Review --> H[Human Review]
  T --> P[Publish to CDN]
  H --> P
  P --> Done[Public]
