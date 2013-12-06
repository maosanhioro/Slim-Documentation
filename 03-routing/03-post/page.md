---
title: POSTルート
status: live
---

POSTメソッドでリクエストするリソースURIにコールバック関数をマッピングするためには、Slimアプリケーションの`post()`メソッドを使用します。

    <?php
    $app = new \Slim\Slim();
    $app->post('/books', function () {
        //bookを作成する
    });

この例では、"/books"というPOSTリクエストが、該当するコールバック関数を呼び出すことを示しています。

Slimアプリケーションにおける`post()`メソッドの最初の引数は、リソースURIとなります。第二引数は`is_callable()`からの`true`を返します。
一般的に、第二引数は[anonymous function][anon-func]を指定します。

[anon-func]: http://php.net/manual/en/functions.anonymous.php
