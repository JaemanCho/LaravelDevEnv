Laravel 開発環境
====

## 概要
Homesteadを使ってローカル開発環境を構築する
## 必須事項

Vagrant  
VirtualBox 6.x

## 構築手順
### 1. コマンド実行
```bash
mkdir project_folder
cd project_folder
composer require laravel/homestead --dev
vendor\\bin\\homestead make
cd ~/.ssh
ssh-keygen -t rsa
エンター
パスワード入力
```
### 2. Homestead.yml
```yaml
ip: 指定ip
memory: 2048
cpus: 2
provider: virtualbox
authorize: ~/.ssh/id_rsa.pub
keys:
    - ~/.ssh/id_rsa
folders:
    -
        map: 'ローカルプロジェクトディレクトリパス'
        to: /home/vagrant/code
sites:
    -
        map: ドメイン.local
        to: /home/vagrant/code/public
        type: "apache"
        php: "バージョン"
        options:
            owner: "root"
            group: "root"
            mount_options: ['dmode=777','fmode=777']
databases:
    - データベース名
features:
    -
        mariadb: false
    -
        ohmyzsh: false
    -
        webdriver: false
name: vm名
hostname: ホストネーム
```
### 3. hosts ファイル修正
```bash
指定ip  ドメイン.local
```
### 4. vagrant 実行
```bash
vagrant up
```
### 5. Laravel インストール
```bash
vagrant ssh
cd ~/code
composer create-project laravel/laravel --prefer-dist .
```
### 6. アクセス
http://ドメイン.local

### 7. アクセスできない場合
方法1
```bash
vagrant provision
```

方法2
```bash
vagrant ssh
sudo apachectl restart
#もしくは
sudo service apache2 start
```

### 8. Homestead.yml に修正をした場合
```bash
vagrant reload --provision
```
## DB 接続情報
### MySQL
127.0.0.1:33060  
指定ip:3306  
homestead / secret

### PostgreSQL
127.0.0.1:54320  
指定ip :5432  
homestead / secret

## Mailhog
127.0.0.1 or localhost:8025  
指定ip or ドメイン:8025

## 公式ドキュメント
### 英語
https://laravel.com/docs/7.x/homestead
### 日本語
https://readouble.com/laravel/7.x/ja/homestead.html