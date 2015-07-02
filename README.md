# symfony-tutorial

Let's study Symfony!

http://symfony.com/doc/current/book/index.html の劣化版


## 目次

- Composer によるパッケージ管理
- PSR PHPのコーディング
- Symfony のインストール
- parameters.yml, config.yml
- Create your First Page
- Controller と Action
- Routing
- Twig テンプレートエンジン
- Configureing Symfony and Environments
- The Bundle System
- データベースとDoctrine、Entity、Repository
- app/consle コマンド系 cache:clear, assets:install
- FormType と handleRequest
- Validation
- Security
- Translations
- Service Container


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

日本語がよければ　https://github.com/maosanhioro/fig-standards/tree/master/translation あたり参照


## Symfony のインストール




## parameters.yml, config.yml

## Create your First Page

## Controller と Action

## Routing

## Twig テンプレートエンジン

## Configureing Symfony and Environments

## The Bundle System

## データベースとDoctrine、Entity、Repository

## app/consle コマンド系 cache:clear, assets:install

## FormType と handleRequest

## Validation

## Security

## Translations

## Service Container

