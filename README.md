# 検品・たたみ 外注管理

## 公開方法

このフォルダをそのまま静的サイトとして公開できます。

- `index.html`: アプリ本体
- `supabase/schema.sql`: Supabase用DB・Storage・権限SQL
- `supabase/SETUP.md`: Supabase設定手順

## 注意

現時点の `index.html` はローカルデモ版です。
本番公開では、Supabaseの `Project URL` と `anon public key` を入れて、ログイン・データ保存・画像保存をSupabaseに接続してください。

## 推奨公開先

- Netlify
- Vercel
- GitHub Pages

