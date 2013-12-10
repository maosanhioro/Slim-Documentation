---
title: アプリケーション名とスコープ
status: live
---

Slimアプリケーションを構築すると、例えばグローバルスコープや関数スコープといった、様々なスコープが含まれます。
それぞれの場所でSlimアプリケーションを参照することになりますが、それにはいくつかの方法があります:

* Slimアプリケーションの静的メソッド`getInstance()`によるアプリケーション名を使う方法
* カリー化することで、`use`キーワードで関数スコープ内にアプリケーションを渡す方法

### アプリケーション名

それぞれのSlimアプリケーションに名前を与えることができます。**省略可能**。
名前は、各スコープからのSlimアプリケーションのインスタンス参照を助けます。


    <?php
    $app = new \Slim\Slim();
    $app->setName('foo');
    $name = $app->getName(); // "foo"

### スコープの解決

では実際どのようにSlimアプリケーションへ参照するのでしょう。以下の例は、ルートのコールバック関数内でSlimアプリケーションへの参照を取得しようとしています。
`$app`変数はGETルートを定義するためにグローバルスコープで使用されていますが、テンプレートのレンダリングのためにコールバックのスコープ内でも必要とされています。


    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () {
        $app->render('foo.php'); // <-- ERROR
    });

`$app`変数は、コールバック関数内で使用できないため、この例の実行結果は失敗となります。

#### カリー化

`use`キーワードを使いコールバック関数内に`$app`変数を注入することができます:

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () use ($app) {
        $app->render('foo.php'); // <-- SUCCESS
    });

#### 名前による取得

Slimアプリケーションの静的メソッド`getInstance()`を使うこともできます:

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', 'foo');
    function foo() {
        $app = Slim::getInstance();
        $app->render('foo.php');
    }
