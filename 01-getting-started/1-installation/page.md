---
title: インストール
status: live
---

### Composerによるインストール

Composerをインストールします:

    curl -s https://getcomposer.org/installer | php

プロジェクトルートに`composer.json`を作成します。

    {
        "require": {
            "slim/slim": "2.*"
        }
    }

Composer経由でSlim Frameworkをインストールします:

    php composer.phar install

Add this line to your application's `index.php` file:

    <?php
    require 'vendor/autoload.php';

### 手動インストール

プロジェクトディレクトリにSlim Frameworkをダウンロード・展開し、アプリケーションファイルである`index.php`で`require`します。オートローダー登録もします。

    <?php
    require 'Slim/Slim.php';
    \Slim\Slim::registerAutoloader();
