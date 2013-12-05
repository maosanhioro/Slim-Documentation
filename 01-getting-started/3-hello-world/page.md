---
title: Hello World
status: live
---

Slimアプリケーションをインスタンス化します:

    $app = new \Slim\Slim();

HTTP GETルートを定義します:

    $app->get('/hello/:name', function ($name) {
        echo "Hello, $name";
    });

Slimアプリケーションを実行します:

    $app->run();
