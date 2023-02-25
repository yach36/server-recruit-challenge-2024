# サーバーエンジニア向け 2024新卒採用事前課題

あなたは歌手とアルバムを管理するAPIの機能開発にたずさわることになりました。

次の課題に順に取り組んでください。

できない課題があっても構いません。

面接中に課題に関して質問をしますので、分かる範囲で説明してください。

## 課題1
プログラムのコードを読み、中身を把握しましょう。

## 課題2
go をインストールし(各自で調べてください)、歌手を管理するAPIの動作を確認しましょう。

```
# (ターミナルを開いて)
# サーバーを起動する
go run main.go
```

```
# (別のターミナルを開いて)
# 歌手の一覧を取得する
curl http://localhost:8888/singers

# 指定したIDの歌手を取得する
curl http://localhost:8888/singers/1

# 歌手を追加する
curl -X POST -d '{"id":10,"name":"John"}' http://localhost:8888/singers

# 歌手を削除する
curl -X DELETE http://localhost:8888/singers/1
```

## 課題3
アルバムを管理するAPIを新規作成しましょう。

### 3-1
アルバムの一覧を取得するAPI
```
curl http://localhost:8888/albums

# このようなレスポンスを期待しています
[{"id":1,"title":"Alice's 1st Album","singer_id":1},{"id":2,"title":"Alice's 2nd Album","singer_id":1},{"id":3,"title":"Bella's 1st Album","singer_id":2}]
```

### 3-2
指定したIDのアルバムを取得するAPI
```
curl http://localhost:8888/albums/1

# このようなレスポンスを期待しています
{"id":1,"title":"Alice's 1st Album","singer_id":1}
```

### 3-3
アルバムを追加するAPI
```
curl -X POST -d '{"id":10,"title":"Chris 1st","singer_id":3}' http://localhost:8888/albums

# このようなレスポンスを期待しています
{"id":10,"title":"Chris 1st","singer_id":3}

# そして、アルバムを取得するAPIでは、追加したものが存在するように
curl http://localhost:8888/albums/10
```

### 3-4
アルバムを削除するAPI
```
curl -X DELETE http://localhost:8888/albums/1
```

## 課題4
アルバムを取得するAPIでは、歌手の情報も付加するように改修しましょう。

### 4-1
指定したIDのアルバムを取得するAPI
```
curl http://localhost:8888/albums/1

# このようなレスポンスを期待しています
{"id":1,"title":"Alice's 1st Album","singer":{"id":1,"name":"Alice"}}
```

### 4-2
アルバムの一覧を取得するAPI
```
curl http://localhost:8888/albums

# このようなレスポンスを期待しています
[{"id":1,"title":"Alice's 1st Album","singer":{"id":1,"name":"Alice"}},{"id":2,"title":"Alice's 2nd Album","singer":{"id":1,"name":"Alice"}},{"id":3,"title":"Bella's 1st Album","singer":{"id":2,"name":"Bella"}}]
```

## 課題5
歌手とそのアルバムを管理するという点で、現状のAPIの改善点を検討し思いつく限り書き出してください。

実装をする必要はありません。

```
【回答】
・歌手やアルバムに詳細な情報を与えるため、構造体に「生年月日」や「発売日」などのフィールドを追加すること
・アルバムに収録されている曲の一覧も表示するとわかりやすいので、「曲」の構造体を追加すること
・POSTされた歌手やアルバムのデータを永続化するためにDBを設けること
・歌手が歌手名を変えるなど、既存データに変更が生じたときのために更新処理(PATCH)を追加すること
・第三者によるデータの操作を防ぐために、POSTやDELETEのときは認証を行うこと
・curlコマンドで処理するよりも画面で操作する方がわかりやすいので、UIを作成すること
```
