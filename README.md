# PithWire Cron Trigger

1日4回（:07 UTC/JST）に https://pithwire.com/run-news を5言語分叩くための GitHub Actions cron。

## なぜ

Cloudflare Workers の scheduled() から Claude API を叩くと CF-CF ループ判定で 403 Error 1000 が返る問題があり、CF外部からcronで叩く必要がある。Claude Code Routines も試したが外部host allowlist制限で不可。最終的に GitHub Actions に落ち着いた。

## 仕様

- cron: `7 */6 * * *`（1日4回）
- 処理: ja/en/ko/hi/id を順次 curl、各 --max-time 300秒
- 実行時間: 1 run あたり約10-15分
- 料金: Public repo で Actions 無制限無料

## Secret

- `RUN_KEY`: PithWire Worker の MANUAL_RUN_KEY

## 関連

同じ CF-CF ループ問題で構築した姉妹プロジェクト: [2033-journey-cron-trigger](https://github.com/Toshi6969/2033-journey-cron-trigger)
