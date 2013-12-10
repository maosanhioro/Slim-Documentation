---
title: カスタムHTTPメソッド
status: live
---

### 1ルートで複数のHTTPメソッドに対応

時には複数のHTTPメソッドに対応するルートが必要だったり、カスタムHTTPメソッドに対応するルートが必要なことがあります。
これはルートオブジェクトの`via()`を使うことで両方解決することができます。
例では複数のHTTPメソッドに応答するコールバックにリソースURIをマッピングしています。

    <?php
    $app = new \Slim\Slim();
    $app->map('/foo/bar', function() {
        echo "I respond to multiple HTTP methods!";
    })->via('GET', 'POST');
    $app->run();

この例で定義されたルートはGET/POST両方のリクエストを受付け、"/foo/bar"で識別されるリソースに応答します。
ルートオブジェクトの`via()`に個別の文字列引数として適切なHTTPメソッドを指定します。
その他のルートメソッド（例：`name()`、`conditions()`）も含めてチェーンメソッドとなります:

    <?php
    $app = new \Slim\Slim();
    $app->map('/foo/bar', function() {
        echo "Fancy, huh?";
    })->via('GET', 'POST')->name('foo');
    $app->run();

### 1ルートでカスタムHTTPメソッドに対応

ルートオブジェクトの`via()`は、GET, POST, PUT, DELETE, OPTIONSに限定されません。例えばWebDAVのHTTPリクエストに対応するといったカスタムHTTPメソッドを指定することも可能です。
下記のように"FOO"といったようにカスタムHTTPメソッドに対応するルートを定義することができます。

    <?php
    $app = new \Slim\Slim();
    $app->map('/hello', function() {
        echo "Hello";
    })->via('FOO');
    $app->run();
