---
marp: true
theme: gaia
paginate: true
---

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
strong,b {
  color: red;
}
</style>

<!-- _class : lead invert-->

# Dockerを使った開発のはじめ

イノベーション＆インキュベーション室
森光一

---

# 自己紹介

* 名前：森光一
* I＆I室での役割：開発に関わるもの全て
* 趣味：
  * ライブ、ギター
  * 酒、日本酒、ビール

---

# 今回の目的

* モダンな技術に触れてもらう
* FastAPiとReactについて何となく理解できるようになる
* 自分たちの作りたいものがサーバレスで提供できるようになる

---

# 今回やらないこと

* Dockerのインストール方法
* コンテナ技術、FastAPI、Reactの詳しい説明
* コードの解説

---

# コンテナ技術とは

アプリケーションの実行に必要な環境を**コンテナ**という1つの塊にして、アプリケーションを実行すること。
導入している企業：
LINEヤフー、メルカリ、楽天モバイル、サイバーエージェント...etc

### なぜ学ぶのか

* 流行りの技術に触れてほしい
* 色んな企業で採用されているから

---

### メリット

* 可搬性
  * OSに依存しないので、どんな環境でも同じように実行ができる
    ※アーキテクチャには依存する
* CI/CDとの相性が良い
  * 実行環境がコンテナ化されるので、ブルーグリーンデプロイをしやすい

### デメリット

* 教育コスト高め

---

# システム構成

ゴールはこういう構成になります。

![center](images/infrastructure.svg)

---

<!-- _class : lead invert-->
# 実習

---

# Todoアプリを立ち上げよう(1)

* 以下のURLからソースをクローンしてくる
`https://github.com/m8i-51/growing`

* プロジェクトのディレクトリに移動する
`cd growing`

* 以下のファイルに実行権限を与える
`chmod +x project/backend/entrypoint.sh`

* コンテナ達をビルド
`docker-compose up -d`

---

# Todoアプリを立ち上げよう(2)

* コンテナが正常に起動しているか確認する
`docker-compose logs web`

実行結果↓

```log
web-1  | waiting for postgres server
web-1  | Connection Successfully
web-1  | INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
web-1  | INFO:     Started reloader process [1] using statreload
web-1  | INFO:     Started server process [13]
web-1  | INFO:     Waiting for application startup.
web-1  | INFO:     Starting up...
web-1  | INFO:     Application startup complete.
web-1  | INFO:uvicorn.error:Application startup complete.
```

---

# Todoアプリを立ち上げよう(3)

* 正常に起動されていたらテーブルを作成する
`docker-compose exec web python app/db.py`

※正常に動作していれば何も返って来ないはず

---

# Todoアプリを立ち上げよう(4)

* テーブルが作成されたか確認する

```text
docker-compose exec web-db psql -U postgres

postgres-# postgres=\c test_db

test_db-# test_db=\dt

           List of relations
Schema |    Name     | Type  |  Owner
--------+-------------+-------+----------
public | textsummary | table | postgres
(1 row)
```

---
# Todoアプリを立ち上げよう()

これで準備が整いました。

* 以下のURLにアクセスするとTodoアプリが表示されるはず
`http://localhost:3007/`

![height:300 center](images/image1.png)

---

<!-- _class : lead invert-->
# 課題

---

# 課題

これであなたはReact + FastAPI + PostgreSQLを用いたアプリ開発のスタートラインを切ることができました。

現状、Todoアプリにはタスクの編集と削除しか実装されていません。
そこで、みなさんには今から課題を出します。

---

# 課題

* タスクの複製機能を実装
（画像が入る）

提出先：
**クローンしてきたリポジトリに新規でブランチを作成し提出**
###### コメント

---

# 質疑・応答

何かありますか？

---

# 次回予告

### TodoアプリをAWSの各サービスを活用して公開

長くなるのでオンデマンド形式にします。(**鋭意製作中**)

---

<!-- _class : lead-->
# おつかれさまでした。
![h:450px](images/ochakumi_man.png)