
##  本稼働・接続セットアップ手順（全4ステップ）

### Step 1: Supabase側の読み取り権限（RLS）の確認

Supabaseのデータベースで、対象テーブル（`daily_logs`、`voice_insights` 等）に対して `anon` ロールでの `SELECT`（読み取り）が許可されているか（Row Level Security の設定）を確認します。

### Step 2: 接続情報の設定（2通りの方法）

以下のいずれかの方法で Supabase プロジェクトに接続できます。

1. **画面上のモーダルから接続（推奨・コード変更不要）**
   * ブラウザで `index.html` を開きます（初期状態はサンプルデータモードで起動します）。
   * 画面右上の **「クエリ仕様・接続設定」** ボタンを開き、`Supabase Project URL`（`https://<YOUR_PROJECT_ID>.supabase.co`）と `Anon Key` を入力して **「Read-Only接続を試行 (GETのみ)」** をクリックします。
2. **`index.html` 内のプロパティ定数（`APP_CONFIG`）で設定（個人ローカル環境向け）**
   * `index.html` 内の `<script>` 先頭にある `APP_CONFIG` オブジェクトのプレースホルダーを書き換えます。
   ```javascript
   const APP_CONFIG = Object.freeze({
     SUPABASE_URL: "https://<YOUR_PROJECT_ID>.supabase.co",
     SUPABASE_ANON_KEY: "<YOUR_SUPABASE_ANON_KEY>"
   });
   ```
   > **注意**: 公開リポジトリ（GitHub等）へ Push する際は、必ずプレースホルダー（`YOUR_SUPABASE_PROJECT_URL` / `YOUR_SUPABASE_ANON_KEY`）の状態に戻してください。

### Step 3: 実データ表示の動作確認

ナレッジグラフ、統合タイムライン、クロス検索＆JSON/CSVエクスポート画面で実データが正しく表示されることを確認します。

### Step 4: 静的ホスティング（GitHub Pages 等）での公開

バックエンドサーバーを必要としない単一HTMLファイル（SPA）のため、GitHub Pages・Vercel・Cloudflare Pages 等の無料ホスティングサービスでそのまま配信できます。

#### GitHub Pages の設定手順例:
1. 変更をコミットし、`git push` で GitHub リポジトリ（`<YOUR_USERNAME>/lifelog-system`）へ反映します。
2. GitHub リポジトリ上部の **Settings ➔ Pages** を開きます。
3. **Source** を `Deploy from a branch`、**Branch** を `main`（フォルダは `/ (root)`）に設定して **Save** します。
4. 数分後、`https://<YOUR_USERNAME>.github.io/lifelog-system/Webapp/` のURLが発行され、PCやスマートフォンのブラウザからアクセス可能になります。
　※スマートフォン部分はまだ開発中です
