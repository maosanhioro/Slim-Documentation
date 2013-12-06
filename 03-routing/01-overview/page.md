---
title: ルーティングの要約
status: live
---

Slim Frameworkは特定のHTTPリクエスト（例：GET, POST, PUT, DELETE, OPTIONSもしくはHEAD）の関数にコールバックすることでリソースURIにマッピングすることができます。
Slimアプリケーションは、最初にHTTPリクエストURIとメソッドにマッチしたルートを呼び出します。

SlimアプリケーションがHTTPリクエストURIとメソッドにマッチしたルートを見つけられない場合は、自動的に**404 Not Found**を返します。
