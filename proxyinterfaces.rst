==========================
サービスインターフェース
==========================

http://code.google.com/intl/ja/apis/cloudprint/docs/proxyinterfaces.html

cloud print proxy(PCにインストールして使うソフト)のインターフェース紹介。
プリンタベンダ、製造業者向けに公開されている。
これをファームウェアに実装すればCloud Aware Printerになるはず。

Google Account Client Login API
=================================
プリンタの登録、ジョブの取得でGoogle Accountを使う必要がある。
別資料を参考のこと -> http://code.google.com/intl/ja/apis/accounts/docs/AuthForInstalledApps.html


Google Cloud Print Service Interface Reference
===============================================
以下のAPIがある
 * register : プリンタの登録
 * update : プリンタ情報の更新
 * list : 特定ユーザが利用可能なプリンタ一覧の取得
 * delete : プリンタの削除
 * control : プリントジョブの状態取得
 * fetch : 次のプリントジョブの取得


Common Output Control Parameters and Values
=============================================
全てのインターフェースで利用可能な共通パラメータについて

--------
output
--------
以下の3種をサポート
 * json
 * xml
 * text

--------
objects
--------
出力情報の粒度を制御
 * capabilities : 選択されたプリンタ/プリントジョブの情報を出力
 * all : 利用可能な全ての情報を出力


Error Handling
===============
処理結果はBooleanで返ってくる。(true/false)
falseの場合はエラーが発生したことを意味する。エラーの詳細はmessageを見ることで知ることが出来る。


Job Availability Notification
==============================
プリントジョブがあるかどうかはGoogle Talkを通して、永続化したXMPP接続(using a persistent XMPP connection)を通して通知する。
プロキシはGoogle Talk XMPPサーバに接続し印刷要求の通知を購読する。
接続方法の詳細はオープンソースのlibjingleを参照のこと。

これ以外に、頻繁に/fetchインターフェースを使ってジョブの確認をすることもできる。

