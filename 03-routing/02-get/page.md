---
title: GETルート
status: live
---

GETメソッドでリクエストするリソースURIにコールバック関数をマッピングするためには、Slimアプリケーションの`get()`メソッドを使用します。

    <?php
    $app = new \Slim\Slim();
    $app->get('/books/:id', function ($id) {
        //$idで指定されたbookを表示する
    });

この例では、"/books/1"というGETリクエストが、引数"1"をコールバックの引数として渡し、該当するコールバック関数を呼び出すことを示しています。

Slimアプリケーションにおける`get()`メソッドの最初の引数は、リソースURIとなります。第二引数は`is_callable()`からの`true`を返します。
一般的に、第二引数は[anonymous function][anon-func]を指定します。

[anon-func]: http://php.net/manual/en/functions.anonymous.php
