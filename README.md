# Laravelローカル環境サンプル

## ローカル環境でのバージョン確認
<br>

PHPバージョン確認コマンド
- `php -version`

<br>

nginxバージョン確認コマンド
- `nginx -v`

（apacheバージョン確認コマンド）
- `httptd -v`  または  `apachectl -v`

<br>

# ローカル開発環境の構築手順

## 前提条件

- Dockerをインストールすること
  - https://www.docker.com/get-started
  - Windowsの場合、wsl2が無効である場合は、有効にするよう警告される。そのダイアログに書かれているリンクをクリックして WSLのmsiをダウンロード・インストール。
  - Macの場合は、ダウンロードするファイルが、Intelチップ版とM1チップ版があるので、画面の一番左上のリンゴマークから「このMacについて」を呼び出して確認すること。

<br>

## コマンドの表記

  - [Shell] : docker-compose.ymlが直下に存在するディレクトリにて実行
  - [app]   : Dockerの、Webサーバーのシェル（Apache Server）にて実行（Webサーバーのシェルに移動するには、コマンド`docker compose exec {コンテナ名} bash`を使う）

  - また、`docker compose` と `docker-compose` コマンドは全て、docker-compose.ymlファイルが存在するディレクトリに移動して実行すること。

<br>

## 環境構築の手順

1. 当リポジトリをクローンして、中身だけを、プロジェクトを作成したいフォルダにコピペする。

2. コピペ先のフォルダの、以下のファイルを削除する。
  - `./README.md`
  - `./backend/.gitignore`
  - `./backend/.gitkeep`

3. docker-compose.ymlが直下に存在するディレクトリに移動する。

4. ターミナルで以下のコマンドを実行(上から1つずつ順番に実行すればOK)
- - `docker compose up -d --build` [Shell]
  - `docker compose exec app bash` [Shell]
  - `composer self-update --2` [app]
  - `composer create-project laravel/laravel . "8.*" --prefer-dist` [app]
  - `chmod 707 -R storage` [app]

5. `documents/.env.example` と `backend/src/.env` を開いて、 `backend/src/.env` の項目のうち、 `documents/.env.example` にある項目を、`documents/.env.example`の内容に変更する。その後、documentsディレクトリを削除する。

6. 以上の手順を行うことでローカル開発環境で、以下の画面が閲覧できる。
- - Webアプリケーション
    - http://localhost
  - MailHog（Laravelアプリケーションが送信したメールを確認できるページ）
    - http://localhost:8025/#

<br>

## ローカル環境で作業中に使うコマンド一覧

1. ローカルサーバを起動するコマンド(初回以降)
- `docker compose up -d` [Shell]

2. ローカルサーバを終了するコマンド(作業終了後、PCをシャットダウンする前に必ず実行すること)
- `docker compose down` [Shell]

3. Webサーバ(Laravelが実行されているサーバ)のシェルへ移動するコマンド
- `docker compose exec app bash` [Shell]

4. 3 で移動したWebサーバのシェルを終了して、元のシェルに移動するコマンド
- `exit` [app]

5. Laravelのキャッシュクリアコマンド

- アプリキャッシュのクリア
  - `php artisan cache:clear` [app]

- viewキャッシュのクリア
  - `php artisan view:clear` [app]

- configキャッシュのクリア
  - `php artisan config:cache` [app]

- routeキャッシュのクリア
  - `php artisan route:cache` [app]

<br>

## ローカル環境でのメールの送信について

開発環境では mailhog を利用する。  
以下のURLにアクセスすれば mailhog用の受信トレイを表示する事ができる。  

- http://localhost:8025/#

<br>

## 開発用ツールについて

`./documents/`推奨ツール.md に記載。

# 以下、環境構築の手順の解説

## `composer self-update --2` [app]

<br>

composerのアップグレードコマンド。composerのバージョンを2.x系の最新版にする。
- `composer self-update --2` [app]

<br>

※以下のコマンドを実行すると最新バージョンを教えてくれる。
- `composer self-update` [app]

<br>

## `composer create-project laravel/laravel . "8.*" --prefer-dist` [app]

composerのコマンドで、Laravelをインストールする。以下が各オプションについての詳細。  
参考：https://readouble.com/laravel/8.x/ja/installation.html

- `create-project`
  - プロジェクトを作成するオプション。アプリケーションを指定する。今回の場合はLaravel(laravel/laravel)を指定する。

- `.`
  - プロジェクトを作成するディレクトリを指定する。文字列にすると、その名前のディレクトリが作成され、その中にLaravelアプリがダウンロードされる。今回は、存在するディレクトリに直接インストールしたいので、カレントディレクトリを表す "." のみを入力する。
  - 参考：https://www.engilaboo.com/laravel-install-current-directory/

- `"8.*"`
  - インストールするLaravelのバージョンを指定する。指定しない場合は最新のバージョンが指定される。今回は、Laravel8 の最新バージョンを指定したいので、"8.*"と入力する。\* には「すべて」のような意味合いがあり、これで最新のものを指定できる。

- `--prefer-dist`
  - ダウンロードをzip形式に指定する（それにより高速化できる）。
  - 参考：https://kin29.info/composer-の-prefer-distってよく使うけど何してる？/

<br>


## `chmod 707 -R storage` [app]

<br>

localhostにアクセスすると、以下のエラーページが表示されることがある。

```
UnexpectedValueException
The stream or file "/work/src/storage/logs/laravel.log" could not be opened in append mode: Failed to open stream: Permission denied
http://localhost/
```

このエラーは、phpを実行するアプリケーション(今回の場合はnginxサーバ)に、storage/内のファイルの書き込み権限がないことで、storage/内にlogを記録できないことで発生するもの。

<br>

これを解決するには、このコマンドを実行する。  
このコマンドで、nginxアプリケーションに対してstorage/以下のファイルの全権限を与えることができる。

<br>

## `php artisan key:generate` [app]

<br>

encryption key の生成。  
artisan コマンドで encryption key を設定する。  
(参考：https://qiita.com/ponsuke0531/items/197c76fcb9300d7c5f36)。

<br>
