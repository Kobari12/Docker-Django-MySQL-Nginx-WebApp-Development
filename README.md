# Dockerを用いたDjango、MySQL、Nginxを使用したWebアプリケーションの開発環境構築

## 概要
このRead.meファイルは、Dockerを使用してDjango、MySQL、Nginxを使用したWebアプリケーションの開発環境を構築するためのガイドです。

## 準備
1. Dockerをインストールします。詳細は、[Docker公式サイト](https://www.docker.com/)を参照してください。

2. このリポジトリをクローンします。

    ```console
    $ git clone https://github.com/Kobari12/docker_django_mysql_nginx.git
    ```

3. クローンしたリポジトリ内に移動し、「.env」ファイル内の、データベースの接続に必要な情報などを、環境変数に設定します。

    ```console
    $ cd docker_django_mysql_nginx
    $ vi .env

    MYSQL_DATABASE=*****
    MYSQL_USER=*****
    MYSQL_PASSWORD=*****
    MYSQL_ROOT_PASSWORD=*****
    ```

## 起動

1. 次のコマンドを実行して、Dockerコンテナをビルドします。

    ```console
    $ docker-compose build
    ```

2. 次のコマンドを実行して、Dockerコンテナをバックグラウンドで起動します。

    ```console
    $ docker-compose up -d
    ```

    これにより、Djangoアプリケーションが「[http://localhost:8000](http://localhost:8000)」で公開されます。

3. Djangoプロジェクトを作成する。以下のコマンドを実行すると、「mysite」という名前のフォルダが作成され、その中にDjangoプロジェクトが作成されます。

    ```console
    $ docker-compose exec app django-admin startproject mysite .
    ```

    設定を適切に変更して下さい．


## 停止
Dockerコンテナを停止するには、次のコマンドを実行します。

```console
$ docker-compose stop
```

## データベースの管理
Docker上のMySQLコンテナに接続するには、「docker-compose exec」コマンドを使用します。次のように入力します。

```console
$ docker-compose exec db mysql -u root -p
```

「-u root -p」というオプションを指定することで、MySQLに「root」ユーザーとして接続できます。接続後、「mysql>」プロンプトが表示されるので、SQL文を入力することができます。

接続を終了するには、「exit」と入力します。

```console
mysql> exit
```

詳細は、[MySQL公式ドキュメント](https://dev.mysql.com/doc/refman/8.0/ja/)を参照してください。

## Djangoアプリケーションの管理

Djangoアプリケーションを管理するには、「docker-compose exec」コマンドを使用します。次のように入力します。

```console
$ docker-compose exec app python manage.py [コマンド]
```

「[コマンド]」の部分には、実行したいDjango管理コマンドを入力します。例えば、次のようにすることで、マイグレーションを実行することができます。

```console
$ docker-compose exec app python manage.py migrate
```

また、次のようにすることで、スーパーユーザーを作成することができます。

```console
$ docker-compose exec app python manage.py createsuperuser
```

詳細は、[Django公式ドキュメント](https://docs.djangoproject.com/ja/3.1/ref/django-admin/)を参照してください。

## アプリケーション構成

本アプリケーションは、以下のコンテナから構成されています。

- Django: Webアプリケーションフレームワーク
- MySQL: リレーショナルデータベース管理システム
- Nginx: Webサーバー

詳細は、Docker Composeファイルを参照してください。

## 注意点
このリポジトリは、開発環境構築のためのものです。本番環境での使用は推奨しません。また、このリポジトリを使用したことによる問題や損害については、作者は一切の責任を負いません。必ず、本番環境用の適切な構成を検討し、構築するようお願いします。

また、DjangoやNginxなどの設定は、このリポジトリでは最小限のものしか用意されていません。本番環境で使用する場合は、必ず各設定ファイルを確認し、適切な設定を行うようお願いします。


## 作者
このリポジトリは、@Kobari12が作成しました。

Dockerを用いたWebアプリケーションの開発環境構築については、まだまだ勉強中です。そのため、このリポジトリには不備や誤りが含まれる可能性があります。そのような場合は、お手数ですがIssueやPull Requestをいただけると幸いです。

また、このリポジトリを使用した際に、ご不明な点がありましたら、お気軽にお問い合わせください。

皆様のご支援をよろしくお願いします。
