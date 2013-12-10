---
title: アプリケーション設定
status: live
---

### mode

これはアプリケーションの現在の操作モード識別子です。モードはSlimアプリケーションの内部機能には影響しません。
むしろ`configMode()`で与えられたモードに応じたそれぞれのコードを呼び出すためだけにあります。

アプリケーションモードは、環境変数、またはSlimアプリケーションのコンストラクタの引数としてインスタンス生成時に宣言されます。これはその後変更はできません。
モード名は自由です。 "development"、"test"、"production"などはよくありますが、"foo"といったように好きなモード名を指定することもできます。

    <?php
    $app = new \Slim\Slim(array(
        'mode' => 'development'
    ));

データの型
: string

デフォルト値
: "development"

### debug

<div class="alert alert-info">
    <strong>注意！</strong> Slimはエラーを`ErrorException`インスタンスに変換しています。
</div>

デバッグが有効の場合、Slimはキャッチできない例外について診断表示するために組み込みのエラーハンドラを使用します。
逆にデバッグが無効の場合は、唯一の引数としてキャッチされなかった例外を渡し、カスタムエラーハンドラを呼び出します。

    <?php
    $app = new \Slim\Slim(array(
        'debug' => true
    ));

データの型
: boolean

デフォルト値
: true

### log.writer

適切な出力先にログメッセージを記録するにはカスタムログライターを使用してください。
標準でSlimロガーは`STDERR`に書き込みます。
カスタムログライターを使用する場合は、インターフェイスについては実装する必要があります。

    public write(mixed $message, int $level);

`write()`メソッドは、適切な出力先（例：テキストファイル、データベースもしくはWebサービス）に対してログ（必ずしも文字列だけではない）を送信します。

カスタムログライターを指定するには、インスタンス生成後であれば、Slimロガーに直接アクセスし、`setWriter()`を使用する必要があります。

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'log.writer' => new \My\LogWriter()
    ));

    // インスタンス生成後の場合
    $log = $app->getLog();
    $log->setWriter(new \My\LogWriter());

データの型
: mixed

デフォルト値
: \Slim\LogWriter

### log.level

<div class="alert alert-info">
    <strong>注意！</strong> 整数の代わりに`\Slim\Log`の定数を使用してください。
</div>

Slimのログレベル:

* \Slim\Log::EMERGENCY
* \Slim\Log::ALERT
* \Slim\Log::CRITICAL
* \Slim\Log::ERROR
* \Slim\Log::WARN
* \Slim\Log::NOTICE
* \Slim\Log::INFO
* \Slim\Log::DEBUG

`log.level`設定は、ログを記録するしないを決定します。
例えば`log.level`を`\Slim\Log::INFO`とすると、debugメッセージは出力されず、その他のinfo, warn, error, fatalはログに出力されます。

インスタンス生成後にこの設定を変更するには、Slimロガーに直接アクセスして`setLevel()`を使用する必要があります。

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'log.level' => \Slim\Log::DEBUG
    ));

    // インスタンス生成後の場合
    $log = $app->getLog();
    $log->setLevel(\Slim\Log::WARN);

データの型
: integer

デフォルト値
: \Slim\Log::DEBUG

### log.enabled

Slimロガーを有効または無効にします。
インスタンス生成後にこの設定を変更するには、Slimロガーに直接アクセスして`setEnabled()`を使用する必要があります。

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'log.enabled' => true
    ));

    // インスタンス生成後の場合
    $log = $app->getLog();
    $log->setEnabled(true);

データの型
: boolean

デフォルト値
: true

### templates.path

Slimアプリケーションのテンプレートファイルが含まれているディレクトリは、相対パスまたは絶対パスで指定します。
このパスはテンプレートを取得・レンダリングするためにViewで参照されます。

インスタンス生成後にこの設定を変更するには、Slim Viewに直接アクセスして`setTemplatesDirectory()`を使用する必要があります。

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'templates.path' => './templates'
    ));

    // インスタンス生成後の場合
    $view = $app->view();
    $view->setTemplatesDirectory('./templates');

データの型
: string

デフォルト値
: "./templates"

### view

Slimアプリケーションで使用されるviewクラスまたはそのインスタンスを指します。
インスタンス生成後にこの設定を変更するには、`view()`を使用する必要があります。

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'view' => new \My\View()
    ));

    // インスタンス生成後の場合
    $app->view(new \My\View());

データの型
: string|\Slim\View

デフォルト値
: \Slim\View

### cookies.encrypt

cookieを暗号化するかどうかを指定します。

    <?php
    $app = new \Slim\Slim(array(
        'cookies.encrypt' => true
    ));

データの型
: boolean

デフォルト値
: false

### cookies.lifetime

Slimアプリケーションにより生成されるcookieの有効期間を指定します。
整数であれば妥当なUNIXタイムスタンプでなければなりません。文字列の場合は、妥当なUNIXタイムスタンプとするために`strtotime()`でパースされます。

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'cookies.lifetime' => '20 minutes'
    ));

    // インスタンス生成後の場合
    $app->config('cookies.lifetime', '20 minutes');

データの型
: integer|string

デフォルト値
: "20 minutes"

### cookies.path

`setCookie()`や`setEncryptedCookie()`を呼び出す時に、指定がなかった場合のデフォルトのcookieパスを指定します。

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'cookies.path' => '/'
    ));

    // インスタンス生成後の場合
    $app->config('cookies.path', '/');

データの型
: string

デフォルト値
: "/"

### cookies.domain

`setCookie()`や`setEncryptedCookie()`を呼び出す時に、指定がなかった場合のデフォルトのcookieドメインを指定します。

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'cookies.domain' => 'domain.com'
    ));

    // インスタンス生成後の場合
    $app->config('cookies.domain', 'domain.com');

データの型
: string

デフォルト値
: null

### cookies.secure

cookieがHTTPS経由のみでの利用とするかを指定します。
`setCookie()`や`setEncryptedCookie()`を呼び出す時に、この設定を上書きすることもできます。

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'cookies.secure' => false
    ));

    // インスタンス生成後の場合
    $app->config('cookies.secure', false);

データの型
: boolean

デフォルト値
: false

### cookies.httponly

cookieがHTTP経由のみでの利用とするかを指定します。
`setCookie()`や`setEncryptedCookie()`を呼び出す時に、この設定を上書きすることもできます。

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'cookies.httponly' => false
    ));

    // インスタンス生成後の場合
    $app->config('cookies.httponly', false);

データの型
: boolean

デフォルト値
: false

### cookies.secret_key

cookie暗号化で使用する秘密鍵です。暗号化cookieを使用する場合にはここを変更すべきです。

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'cookies.secret_key' => 'secret'
    ));

    // インスタンス生成後の場合
    $app->config('cookies.secret_key', 'secret');

データの型
: string

デフォルト値
: "CHANGE_ME"

### cookies.cipher

cookie暗号化に使用されるmcrypt暗号文字列を指定します。
参照 [available ciphers](http://php.net/manual/en/mcrypt.ciphers.php).

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'cookies.cipher' => MCRYPT_RIJNDAEL_256
    ));

    // インスタンス生成後の場合
    $app->config('cookies.cipher', MCRYPT_RIJNDAEL_256);

データの型
: integer

デフォルト値
: MCRYPT_RIJNDAEL_256

### cookies.cipher_mode

cookie暗号化に使用されるmcrypt暗号モードを指定します。
参照 [available cipher modes](http://php.net/manual/en/mcrypt.ciphers.php).

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'cookies.cipher_mode' => MCRYPT_MODE_CBC
    ));

    // インスタンス生成後の場合
    $app->config('cookies.cipher_mode', MCRYPT_MODE_CBC);

データの型
: integer

デフォルト値
: MCRYPT_MODE_CBC

### http.version

デフォルトでは、SlimはクライアントにHTTP/1.1レスポンスを返します。必要があればHTTP/1.0へと設定を変更することができます。
これはHTTPクライアントと直接ではなく、バックエンドのプロキシとしてPHPFogやnginxサーバ構成を使用する際には便利です。

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'http.version' => '1.1'
    ));

    // インスタンス生成後の場合
    $app->config('http.version', '1.1');

データの型
: string

デフォルト値
: "1.1"
