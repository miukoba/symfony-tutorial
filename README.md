# symfony-tutorial

Let's study Symfony!

http://symfony.com/doc/current/book/index.html の劣化版

## ちょっとまって

### PHP The Right Way

PHPの最近のベストプラクティスだから読んでおいてね

http://ja.phptherightway.com/

※ できたばかりの頃は量も少なくて超重要なことがまとまっていたけれど、充実しすぎて量もかなり多くなってしまいました。いまから説明することと重複している内容もありますが、あとで読んでおいてください。

### Symfony Best Practices

- http://symfony.com/doc/current/best_practices/index.html
- 日本語がいいなら http://docs.symfony.gr.jp/symfony2/best_practices/index.html
- チュートリアルではない、はじめに読むものではない
  - 慣れてきたら復習や勉強を兼ねて読んでみて

## Composer によるパッケージ管理

PHPの外部ライブラリの管理ツール。rubyでいうBundler, nodeでいうnpm, .NETでいうNuGet のようなもの。

- composer.json
  -  使用するライブラリを自分で記述する、バージョンの範囲を指定
  - ファイルを直接編集しなくてもcomposerのコマンドで追加することもできる
- composer.lock
  - 自動生成される
  -  実際に使用するバージョンやファイルのダウンロードURLが記述されている


### コマンド

- coposer selfupdate
  - composer自身の更新（適当にたまに実施してください）

- composer install
  - 外部ライブラリを実際に取得する
  - ファイルは vendors ディレクトリに配置され vendors/autoload.php ファイルで自動ロードの設定がされる
  - lockファイルが存在する場合はlockファイルのバージョンがダウンロードされる
  - lockファイルがない場合は、jsonファイルで指定された範囲のなかで最新のファイルがダウンロードされる
- composer update
  - lockファイルを無視してjsonファイルの内容でライブラリを更新する


### 参考リンク

- Composer公式 https://getcomposer.org/
- パッケージリポジトリ Packagist https://packagist.org/


## PSR PHPのコーディング

1. PHPはフレームワークごとにコーディング規約が乱立していた
2. 有名なPHPプロジェクトの人たちが集まり -> PHP-FIG
3. 共通点をまとめて新しいコーディング規約を作成した
4. それがPSR!

PSR-0, 1, 2, 3, 4, 7 とありますが、 普段の開発ではとりあえず 0, 1, 2 が重要。守ろう。

日本語がよければ　https://github.com/maosanhioro/fig-standards/tree/master/translation あたりを参照

## Symfony とは

### Symfonyのバージョン

- Symfony1.x系とSymfony2.x系は完全に別物、検索するときは特に注意
- Symfony2と3は同系の予定
- Symfonyはリリース・メンテナンススケジュールがしっかりしていて、LTS（Long Term Support）もある
  - http://symfony.com/doc/current/contributing/community/releases.html#schedule

### Doctrineのバージョン

- DoctrineはSymfony標準のORM(Object Relational Mapper)、詳細は後述。
- Doctrineも1.xと2.xがあるので、検索するときは注意
- Symfony 1.x はDoctrine 1.x を、 Symfony 2.x は Doctrine 2.x
- Doctrine 1.x は Active Record パターン、 Doctrine 2.x は Data Mapper パターン。
  - 参考 http://otndnld.oracle.co.jp/columns/arai-semi/data_access/2/



## Symfony のインストール

- Symfony本体も外部ライブラリなのでComposerでインストールする
- 既存プロジェクトに参加するときは不要
  - プロジェクトを git clone して、外部ライブラリのインストールを行えば、Symfony自体も入る
- 今回は詳細は割愛
  - http://symfony.com/doc/current/book/installation.html


## parameters.yml, config.yml

設定ファイル

- parameters.yml
  - 環境によって変わるパラメータを記載
  - DB接続情報とか
  - ファイルを保存するPATHとか
  - parameters.yml.dist というファイルをgitにコミットしておく
  - composer install 時に parameters.yml.dist から parameters.yml へ値をコピーして作成
- config.yml
  - プロジェクト全体の設定を記載する
  - Environmentごとに設定を変更できる
    - prodの場合は config_prod.yml、dev の場合は config_dev.yml を読み込む
    - config.yml + config_[env].yml ファイルが読み込まれる
    - 正確には config_prod.yml や config_dev.yml が読み込まれ、その中で config.yml をインポートしている

## Bundleとは

> A bundle is similar to a plugin in other software, but even better. The key difference is that everything is a bundle in Symfony, including both the core framework functionality and the code written for your application.

- プラグインのような、パッケージのような、なにか
- 実際に自分たちが書くコードもBundleを作成してその中に書きます
- SYmfony Best Practice には 「アプリケーションのBundleは AppBundle 1つにしましょう」 と書いてある
  - 使いまわせそうなライブラリにできるのであれば別でBundleを作ってもいい
  - Bundleは再利用できる単位であるべき


## Create your First Page

- app/console generate:controller
  - ControllerとViewが作られる
- コマンドについては後述

```
$ app/console generate:controller

  Welcome to the Symfony2 controller generator

Every page, and even sections of a page, are rendered by a controller.
This command helps you generate them easily.

First, you need to give the controller name you want to generate.
You must use the shortcut notation like AcmeBlogBundle:Post

Controller name: AppBundle:Post

Determine the format to use for the routing.

Routing format (php, xml, yml, annotation) [annotation]:

Determine the format to use for templating.

Template format (twig, php) [twig]:

Instead of starting with a blank controller, you can add some actions now. An action
is a PHP function or method that executes, for example, when a given route is matched.
Actions should be suffixed by Action.


New action name (press <return> to stop adding actions): index
 Name "index" is not suffixed by Action
New action name (press <return> to stop adding actions): indexAction
Action route [/index]: /
Templatename (optional) [AppBundle:Post:index.html.twig]:

New action name (press <return> to stop adding actions):

  Summary before generation


You are going to generate a "AppBundle:Post" controller
using the "annotation" format for the routing and the "twig" format
for templating
Do you confirm generation [yes]?


  Controller generation


Generating the bundle code: OK


  You can now start using the generated code!
```

- Controller
  - PostController.php
- view
  - index.html.twig


## Controller と Action



## Routing

- routing.yml
- @Route アノテーション

## Twig テンプレートエンジン

- http://twig.sensiolabs.org/

{# でコメントアウト

```
{# ここがコメントです #}
```

{{ で変数の内容を出力

```
{{ var }}
```

{% が制御文

```
{% for user in users %}
    {{ user.name }}
{% else %}
    空だよ
{% endfor %}
```


継承とブロック

extendsはphpのextendsのイメージ、blockがメソッドのオーバーライドのイメージ

```
{% extends "layout.html" %}
```

```
<title>{% block title %}{% endblock %}</title>

{% block body %}{% endblock %}
```

```
{% include 'header.html' %}
```

## データベースとDoctrine、Entity、Repository

誤解を承知でざっくり言うと

- Entity
  - リレーショナル・データベースの1テーブルと対になるPHPのクラス、POPO（Plain Old PHP Object）
- Repository
  - DBに対する基本的な操作のインターフェイス
  - 簡単な検索は予め用意されている find findBy findOneBy findAll が使える

## app/consle コマンド

app/console で実行すれば、利用可能なコマンドが列挙される

使いそうなところ

    app/console router:debug

    app/console cache:clear
    app/console cache:clear --env=dev
    app/console cache:clear --env=prod
    app/console cache:clear --env=dev --no-warmup

    app/console assets:install

    app/console generate:doctrine:entity
    app/console generate:controller
    app/console generate:doctrine:crud

## FormType と handleRequest

## Validation

## Security

## Translations

## Service Container

