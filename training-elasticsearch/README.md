## ElasticSearch

- 動作確認

```shell
$ curl -XGET 'localhost:9200/'
```

- インデックス作成

```shell
$ curl -XPUT 'localhost:9200/test'
```

- インデックス確認

    - RDSのデータベースに相当する.

```shell
$ curl -XGET 'localhost:9200/_aliases?pretty'

$ curl -XGET 'localhost:9200/test/_settings?pretty'
```

- データ登録

```shell
$ curl -H "Content-Type: application/json" -XPOST 'http://127.0.0.1:9200/test/_doc/1?pretty' -d '{"name" : "test"}'
```

- 登録データ確認

```shell
$ curl -XGET 'localhost:9200/test/_mapping/?pretty'

$ curl -XGET 'localhost:9200/test/_doc/1'
```

- 登録データの削除

```shell
$ curl -H "Content-Type: application/json" -XDELETE  localhost:9200/test/_doc/1
```

- インデックスの削除

```shell
$ curl -H "Content-Type: application/json" -XDELETE  localhost:9200/test/_doc/1
```

## 環境構築

```shell
$ docker compose up -d

$ docker compose exec centos bash

$ docker compose down --rmi all --volumes --remove-orphans
```

## 参考資料

- [Qiita | 【Elasticsearch】よく使うコマンド一覧](https://qiita.com/mug-cup/items/ba5dd0a14838e83e69ac)

- [Elasticsearchエラー「curl:(52)Empty reply from server」が発生した場合の対処法](https://mebee.info/2022/10/27/post-83923/)
    - Elasticsearch8からパスワードが必要

- [公式ドキュメント](https://www.elastic.co/guide/en/elasticsearch/reference/7.17/docker.html)

- [Elasticsearchの個人的によく使うコマンド集](https://zatoima.github.io/aws-elasticsearch-commands-lists.html)

- [Elastic Stack7: Elasticsearchインストール](https://www.server-world.info/query?os=CentOS_Stream_8&p=elasticstack7&f=1)
