# 開発者向け


## 開発環境セットアップ

MoodleとJupyterhubを同じマシン上に起動します。

開発環境用のセットアップを行います。  

```
make devsetup
```

`.env`ファイルが作成されます。  
Moodleのログインパスワードなどを変更する場合は、手動で編集してください。  

コンテナを起動します。  

```
make devup
```

```
make devup
```

3分ほどで、JupyterhubとMoodleが起動します。  
Moodleが起動したらブラウザでアクセスし、ログインします。  

URL: https://localhost/moodle/  
ID: `admin` PW: `changethis`（`.env`に記載）

`サイト管理 > プラグイン > 活動モジュール > 外部ツール > ツールを管理する` と進み、ツールの手動設定画面を開きます。  

- `ツール名`: 任意のツール名
- `ツールURL`: `https://localhost`
- `LTIバージョン`: `LTI 1.3`
- `公開鍵タイプ`: `RSAキー`
- `公開鍵`: `mcj-data/secrets/lti_pubkey.pem` の内容
- `ログイン開始URL`: `https://localhost/hub/lti13/oauth_login`
- `リダイレクトURI`: `https://localhost/hub/lti13/oauth_callback`
- `ツール設定使用`: `活動チューザまたは事前設定ツールに表示する`
- `デフォルト起動コンテナ`: `新しいウィンドウ`

- `サービス`>`IMS LTI課題および評定サービス`: `このサービスを評定同期およびカラム管理に使用する`(AGS用)
- `サービス`>`IMS LTI氏名およびロールプロビジョニング`: `このサービスをプライバシー設定を基にメンバシップ情報を検索するため使用します`(NRPS用)
- `プライバシー`>`ランチャ名をツールと共有する`: `常に`
- `プライバシー`>`ツールからの評定を受け付ける`: `常に`

必要事項を入力後、ツールを作成すると、ツール一覧に追加されます。  
追加されたツールの虫眼鏡アイコンから、以下の項目を確認し、`.env`ファイルに記載します。  

|Moodle上の項目名|`.env`での項目名|
|-|-|
|プラットフォームID|LMS_PLATFORM_ID|
|クライアントID|LMS_CLIENT_ID|

`.env`ファイル編集後、jupyterhubで読み込むために、jupyterhubコンテナを再起動します。  

```
make devrestartjh
```

Moodleにてコース作成・設定を行うことで、Jupyterhubにログイン可能となります。  

- コース作成
- 作成したコースでの、外部ツール利用設定
- 設定した外部ツールからJupyterhubにログイン
