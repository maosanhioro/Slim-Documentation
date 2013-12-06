---
title: PATCHルート
status: live
---

PATCHメソッドでリクエストするリソースURIにコールバック関数をマッピングするためには、Slimアプリケーションの`patch()`メソッドを使用します。

    <?php
    $app = new \Slim\Slim();
    $app->patch('/books/:id', function ($id) {
        // Patch book with given ID
        //$idで指定されたbookを差分更新する
    });

この例では、"/books/1"というPATCHリクエストが、引数"1"をコールバックの引数として渡し、該当するコールバック関数を呼び出すことを示しています。

Slimアプリケーションにおける`patch()`メソッドの最初の引数は、リソースURIとなります。第二引数は`is_callable()`からの`true`を返します。
一般的に、第二引数は[anonymous function][anon-func]を指定します。

