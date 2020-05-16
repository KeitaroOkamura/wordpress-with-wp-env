# wordpress-with-wp-env

wp-env使ってWordPress環境構築するやつ（npm 経由）

# 前提条件

- docker/docker-compose が使える状態にある
- Node（v12以上）がインストールしてある

## 参考 URL

### Docker for Mac
https://docs.docker.com/docker-for-mac/install/

### Docker for Windows
https://docs.docker.com/docker-for-windows/install/


## セットアップ

### 初回起動
```bash
$ npm run wp-env start
```

### 起動確認

現在実行中の Docker コンテナ一覧にいたらOK

```bash
$ docker ps
```

### Web ブラウザでアクセス

[http://localhost:3000/](http://localhost:3000/)


### ログイン

デフォルトのログインアカウントは `admin`/`password` です

[http://localhost:3000/wp-login.php](http://localhost:3000/wp-login.php)


### 停止
```bash
$ npm run wp-env stop
```

### データベースのリセット

```bash
$ wp-env clean all
```

#### 上手くいかない場合

```
// コンテナID指定してコンテナ削除
$ docker rm -f $(docker ps -aq)
// ボリューム名を指定してボリューム削除
$ docker volume rm -f $(docker volume ls -q)
// ローカル WordPress 環境内の投稿、ページ、メディア等を削除
$ rm -rf "../$(basename $(pwd))-wordpress"
```

## .wp-env.json

| フィールド | デフォルト | 説明 |
| --- | --- | --- |
| `core` | `null` | 使用する WordPress のバージョンまたはビルド。null の場合、最新リリース版 |
| `plugins` | `[]` | 環境にインストール、有効化するプラグインのリスト |
| `themes` | `[]` | 環境にインストールするテーマのリスト。最初のテーマが有効化される |
| `port` | `8888` | インストールに使用するポート番号。インスタンスには [http://localhost:8888](http://localhost:8888) でアクセスできる |
| `testsPort` | `8889` | テストインスタンスに使用するポート番号 |
| `config` | `"{ WP_DEBUG: true, SCRIPT_DEBUG: true }"` | wp-config.php の定数とその値 |
| `mappings` | `{}` | WordPress インスタンス内にマウントされるローカルディレクトリと WordPress ディレクトリのマッピング |

## 参照

[https://ja.wordpress.org/team/handbook/block-editor/packages/packages-env/](https://ja.wordpress.org/team/handbook/block-editor/packages/packages-env/)
