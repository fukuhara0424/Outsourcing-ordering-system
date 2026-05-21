# Supabase 本番公開セットアップ

## 1. Supabaseプロジェクトを作成

1. Supabaseで新規プロジェクトを作成
2. Project Settings > API から以下を控える
   - Project URL
   - anon public key

## 2. DB・Storage・権限を作成

Supabaseの SQL Editor で `schema.sql` の中身をそのまま実行します。

作成されるもの:

- `partners`: 外注先
- `profiles`: ログインユーザーの権限
- `jobs`: 案件
- `job_reports`: 進捗・完了報告
- `b_reports`: B品疑い報告
- `faqs`: FAQ
- `inspection-images`: 画像保存用Storage bucket
- RLS: 外注先は自分の案件だけ見える権限

## 3. ログインユーザーを作成

Authentication > Users でユーザーを作成します。

例:

- 管理者: `admin@example.com`
- 外注先A: `aozora@example.com`
- 外注先B: `himawari@example.com`

Supabase Authは基本的にメールアドレス形式のログインIDを使います。

## 4. profilesに権限を登録

ユーザーを作成したら、Auth Usersの `User UID` を確認して、SQL Editorで以下のように登録します。

```sql
-- 先に外注先を作成
insert into public.partners (name, contact, color)
values
  ('あおぞら就労支援', '田中 裕子', '#1A9E72'),
  ('ひまわりワークス', '佐藤 健太', '#2F7ED8'),
  ('なごみ就労支援', '山田 花', '#D85A30');

-- 管理者
insert into public.profiles (id, role, display_name)
values ('AUTH_USER_UID_HERE', 'admin', '管理者');

-- 外注先ユーザー
insert into public.profiles (id, role, display_name, partner_id)
values ('AUTH_USER_UID_HERE', 'partner', 'あおぞら就労支援', 1);
```

## 5. 公開先

GitHubで管理し、公開は以下のどれかがおすすめです。

- Vercel
- Netlify
- GitHub Pages

本番は `inspection_system.html` にSupabaseの `Project URL` と `anon public key` を入れて公開します。

