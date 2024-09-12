# gulp-dev_wp-env_flocss_SPtoPC

## 動作が確認できている環境
- Nodeバージョン v16.13.0
- Gulp 4系
- Dockerインストール済み

## 使い方（ゼロからローカル環境構築を始める場合）
1. クローンorダウンロードしたフォルダをvscode等で開く
2. .wp-env.jsonの16行目のthemeNameを任意のテーマ名に変更
3. style.cssの中身を任意の内容に変更する
4. ターミナルを開き、`npm i`とコマンドを入力
5. node_modulesとpackage-lock.jsonが生成されるのを確認する
6. 必要があれば.wp-env.jsonのWordPressのバージョン(2行目)とPHPのバージョン(3行目)を書き換える（本番環境と合わせておくと良い）
7. `npm run wp-env start`とコマンド入力し、wp-envを起動（WordPressの環境構築が行われる）
8. `npx gulp`とコマンドを入力するとgulpが動き出す（gulpはブラウザシンク、scssコンパイル、画像圧縮の役割を担っている）
9. WordPressの管理画面（/wp-admin）に入り、テーマをこれから開発するものに変更（初期ユーザー名`admin`、初期パス`password`）

## 使い方（既に開発が進んでいる状態からローカル環境構築を始める場合）
1. クローンorダウンロードしたフォルダをvscode等で開く
2. ターミナルを開き、`npm i`とコマンドを入力
3. node_modulesとpackage-lock.jsonが生成されるのを確認する
4. `npm run wp-env start`とコマンド入力し、wp-envを起動（WordPressの環境構築が行われる）
5. データベースをインポートする`npm run wp-env run cli wp db import sql/wpenv.sql`
6. `npx gulp`とコマンドを入力するとgulpが動き出す（gulpはブラウザシンク、scssコンパイル、画像圧縮の役割を担っている）
7. WordPressの管理画面（/wp-admin）に入り、テーマを開発中のものに変更（初期ユーザー名`admin`、初期パス`password`）

## データベース更新するときの手順
__1人での開発の場合は任意のタイミングで手順3と4を行えばOK__
1. チームメンバーがデータベースを触っていないことを確認
2. データベースを更新
3. データベースをエクスポート`npm run wp-env run cli wp db export sql/wpenv.sql`
4. Gitにあげる
5. チームメンバーに更新したことを伝える
6. チームメンバーはデータベースを更新されたデータベースをインポートする`npm run wp-env run cli wp db import sql/wpenv.sql`

## .wp-env.jsonを書き換えたときの手順
1. wp-envを停止 `npm run wp-env stop`
2. アプデした状態で再起動 `npm run wp-env start --update`
- ポート番号を変更した場合は、gulpfile.jsの22行目を書き換える必要あり

## 作業ディレクトリについて
- sassの記述はsrcフォルダの中で行う
- 画像はsrcフォルダのimagesの中に格納する
- phpとjsはdist直下のファイルに直接記述する
- プラグインは管理画面からインストールすると/pluginsに自動的に格納される
- メディアは管理画面からアップロードすると/uploadsフォルダに自動的に格納される（ただし容量が増えすぎる場合はGitHub等で管理すべきでない。管理から外すときは.wp-env.jsonの18行目を消去する。）

## よく使うコマンドまとめ
- wp-env起動 `npm run wp-env start`  
- wp-env停止 `npm run wp-env stop`  
- アプデした状態で再起動 `npm run wp-env start --update`  
- データベースをエクスポート `npm run wp-env run cli wp db export sql/wpenv.sql`  
- データベースをインポート `npm run wp-env run cli wp db import sql/wpenv.sql`
- パッケージインストール　`npm i`
- gulp起動　`npx gulp`

## 備考
- CSS設計はFLOCSS(https://github.com/hiloki/flocss )を採用
- スマホファースト
- rem記述を前提
