---
title: PUTルート
status: live
---

PUTメソッドでリクエストするリソースURIにコールバック関数をマッピングするためには、Slimアプリケーションの`put()`メソッドを使用します。

    <?php
    $app = new \Slim\Slim();
    $app->put('/books/:id', function ($id) {
        //$idで指定されたbookを更新する
    });

この例では、"/books/1"というPUTリクエストが、引数"1"をコールバックの引数として渡し、該当するコールバック関数を呼び出すことを示しています。

Slimアプリケーションにおける`put()`メソッドの最初の引数は、リソースURIとなります。第二引数は`is_callable()`からの`true`を返します。
一般的に、第二引数は[anonymous function][anon-func]を指定します。

### メソッドの上書き

残念ながら、モダンなブラウザはPUTリクエストをネイティブでサポートしていません。この制限を回避するには、HTMLフォームのメソッドを"post"で指定し、このようにHTMLフォームのメソッドを上書きすることで実現できます:

    <form action="/books/1" method="post">
        ... その他のフォームフィールド...
        <input type="hidden" name="_METHOD" value="PUT"/>
        <input type="submit" value="Update Book"/>
    </form>

もし[Backbone.js][backbone]、またはコマンドラインのHTTPクライアントを使用しているなら、**X-HTTP-Method-Override**ヘッダーを通してHTTPメソッドを上書きすることもできます。

[anon-func]: http://php.net/manual/en/functions.anonymous.php
[backbone]: http://documentcloud.github.com/backbone/
