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

Data Type
: string

Default Value
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

Data Type
: boolean

Default Value
: true

### log.writer

適切な出力先にログメッセージを記録するにはカスタムログライターを使用してください。
標準でSlimロガーは`STDERR`に書き込みます。
カスタムログライターを使用する場合は、インターフェイスについては実装する必要があります。

    public write(mixed $message, int $level);

`write()`メソッドは、適切な出力先（例：テキストファイル、データベースもしくはWebサービス）に対してログ（必ずしも文字列だけではない）を送信します。

カスタムログライターを指定するには、インスタンス生成後であれば、Slimロガーに直接アクセスし、`setWriter()`を使用しなければなりません。

    <?php
    // インスタンス生成時の場合
    $app = new \Slim\Slim(array(
        'log.writer' => new \My\LogWriter()
    ));

    // インスタンス生成後の場合
    $log = $app->getLog();
    $log->setWriter(new \My\LogWriter());

Data Type
: mixed

Default Value
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

The `log.level` application setting determines which logged messages will be honored and which will be ignored.
For example, if the `log.level` setting is `\Slim\Log::INFO`, debug messages will be ignored while info, warn,
error, and fatal messages will be logged.

インスタンス生成後にこの設定を変更するには、Slimロガーに直接アクセスして`setLevel()`を使用しなければなりません。

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'log.level' => \Slim\Log::DEBUG
    ));

    // After instantiation
    $log = $app->getLog();
    $log->setLevel(\Slim\Log::WARN);

Data Type
: integer

Default Value
: \Slim\Log::DEBUG

### log.enabled

This enables or disables Slim's logger. To change this setting after instantiation you need to access Slim's logger
directly and use its `setEnabled()` method.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'log.enabled' => true
    ));

    // After instantiation
    $log = $app->getLog();
    $log->setEnabled(true);

Data Type
: boolean

Default Value
: true

### templates.path

The relative or absolute path to the filesystem directory that contains your Slim application's template files.
This path is referenced by the Slim application's View to fetch and render templates.

To change this setting after instantiation you need to access Slim's view directly and use its `setTemplatesDirectory()`
method.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'templates.path' => './templates'
    ));

    // After instantiation
    $view = $app->view();
    $view->setTemplatesDirectory('./templates');

Data Type
: string

Default Value
: "./templates"

### view

The View class or instance used by the Slim application. To change this setting after instantiation you need to
use the Slim application's `view()` method.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'view' => new \My\View()
    ));

    // After instantiation
    $app->view(new \My\View());

Data Type
: string|\Slim\View

Default Value
: \Slim\View

### cookies.encrypt

Determines if the Slim app should encrypt its HTTP cookies.

    <?php
    $app = new \Slim\Slim(array(
        'cookies.encrypt' => true
    ));

Data Type
: boolean

Default Value
: false

### cookies.lifetime

Determines the lifetime of HTTP cookies created by the Slim application. If this is an integer, it must be a valid
UNIX timestamp at which the cookie expires. If this is a string, it is parsed by the `strtotime()` function to extrapolate
a valid UNIX timestamp at which the cookie expires.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.lifetime' => '20 minutes'
    ));

    // After instantiation
    $app->config('cookies.lifetime', '20 minutes');

Data Type
: integer|string

Default Value
: "20 minutes"

### cookies.path

Determines the default HTTP cookie path if none is specified when invoking the Slim application's `setCookie()` or
`setEncryptedCookie()` methods.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.path' => '/'
    ));

    // After instantiation
    $app->config('cookies.path', '/');

Data Type
: string

Default Value
: "/"

### cookies.domain

Determines the default HTTP cookie domain if none specified when invoking the Slim application's `setCookie()` or
`setEncryptedCookie()` methods.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.domain' => 'domain.com'
    ));

    // After instantiation
    $app->config('cookies.domain', 'domain.com');

Data Type
: string

Default Value
: null

### cookies.secure

Determines whether or not cookies are delivered only via HTTPS. You may override this setting when invoking
the Slim application's `setCookie()` or `setEncryptedCookie()` methods.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.secure' => false
    ));

    // After instantiation
    $app->config('cookies.secure', false);

Data Type
: boolean

Default Value
: false

### cookies.httponly

Determines whether or not cookies are delivered only via the HTTP protocol. You may override this setting when invoking
the Slim application's `setCookie()` or `setEncryptedCookie()` methods.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.httponly' => false
    ));

    // After instantiation
    $app->config('cookies.httponly', false);

Data Type
: boolean

Default Value
: false

### cookies.secret_key

The secret key used for cookie encryption. You should change this setting if you use encrypted HTTP cookies
in your Slim application.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.secret_key' => 'secret'
    ));

    // After instantiation
    $app->config('cookies.secret_key', 'secret');

Data Type
: string

Default Value
: "CHANGE_ME"

### cookies.cipher

The mcrypt cipher used for HTTP cookie encryption. See [available ciphers](http://php.net/manual/en/mcrypt.ciphers.php).

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.cipher' => MCRYPT_RIJNDAEL_256
    ));

    // After instantiation
    $app->config('cookies.cipher', MCRYPT_RIJNDAEL_256);

Data Type
: integer

Default Value
: MCRYPT_RIJNDAEL_256

### cookies.cipher_mode

The mcrypt cipher mode used for HTTP cookie encryption. See [available cipher modes](http://php.net/manual/en/mcrypt.ciphers.php).

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.cipher_mode' => MCRYPT_MODE_CBC
    ));

    // After instantiation
    $app->config('cookies.cipher_mode', MCRYPT_MODE_CBC);

Data Type
: integer

Default Value
: MCRYPT_MODE_CBC

### http.version

By default, Slim returns an HTTP/1.1 response to the client. Use this setting if you need to return an HTTP/1.0
response. This is useful if you use PHPFog or an nginx server configuration where you communicate with backend
proxies rather than directly with the HTTP client.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'http.version' => '1.1'
    ));

    // After instantiation
    $app->config('http.version', '1.1');

Data Type
: string

Default Value
: "1.1"
