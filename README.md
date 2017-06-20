# 【Monaca】アプリにプッシュ通知を組み込もう！

![画像1](/readme-img/001.png)

## 概要
* [ニフティクラウドmobile backend](http://mb.cloud.nifty.com/)の『プッシュ通知』機能を実装したサンプルプロジェクトです
* 簡単な操作ですぐに [ニフティクラウドmobile backend](http://mb.cloud.nifty.com/)の機能を体験いただけます★☆

## ニフティクラウドmobile backendって何？？
スマートフォンアプリのバックエンド機能（プッシュ通知・データストア・会員管理・ファイルストア・SNS連携・位置情報検索・スクリプト）が**開発不要**、しかも基本**無料**(注1)で使えるクラウドサービス！

注1：詳しくは[こちら](http://mb.cloud.nifty.com/price.htm)をご覧ください

![画像2](/readme-img/002.png)

## 動作環境
※下記内容で動作確認をしています

iOS
* Mac OS X 10.11.6(El Capitan)
* iPhone5 iOS 9.3.5
* iPhone6s iOS 10.0.1

Android
* Nexus 5X Androidバージョン 7.0

※上記内容で動作確認をしています

## 動作環境の準備
### 共通
* Monaca会員登録
 * 右記リンクより登録（無料）をお願いします　https://ja.monaca.io/
* ブラウザ環境：ChromeまたはMozilla Firefox

### Android端末で動作確認をする場合
* PC
* Googleアカウント
* Android端末

### iOS端末で動作確認をする場合
* Mac
 * キーチェーンアクセスを利用します
* Apple Developer Program(有償)アカウント
 * 別のMacで使用しているアカウントの場合、発行する証明書に秘密鍵を紐付けることができません。ただし、アカウントを使用しているMacから秘密鍵を書き出して、今回使用するMacに送ることで作業は可能です
* iOS端末
 * Lightningケーブル（端末のUDIDを調べるために必要です）

※このサンプルアプリは、実機ビルドが必要です

## プッシュ通知の仕組み
* ニフティクラウドmobile backendのプッシュ通知は、各プラットフォームが提供している通知サービスを利用しています
 * Androidの通知サービス __FCM（Firebase Cloud Messaging）__

 ![画像a1](/readme-img/a001.png)
 ※ FCMはGCM(Google Cloud Messaging)の新バージョンです。既にGCMにてプロジェクトの作成・GCMの有効化設定を終えている場合は、継続してご利用いただくことが可能です。新規でGCMをご利用いただくことはできませんので、あらかじめご了承ください。

 * iOSの通知サービス　__APNs（Apple Push Notification Service）__

 ![画像i1](/readme-img/i001.png)

* 上図のように、アプリ（Monaca）・サーバー（ニフティクラウドmobile backend）・通知サービス（FCMあるいはAPNs）の間で認証が必要になります
 * 認証に必要な鍵や証明書の作成は作業手順の「0.プッシュ通知機能を使うための準備」で行います

## 作業の手順
### 0.プッシュ通知機能を使うための準備
* 動作確認を行う端末に応じて該当する内容を準備してください

#### Android端末で動作確認をする場合
* ニフティクラウド mobile backendと連携させるためのAPIキー(サーバーキー)と端末情報の登録処理時に必要なSender ID(送信者ID)を取得する必要があります
* 下記リンク先のドキュメントを参考に、FCMプロジェクトの作成とAPIキー・Sender IDの取得を行ってください

 __[mobile backendとFCMの連携に必要な設定](http://mb.cloud.nifty.com/doc/current/tutorial/push_setup_android.html)__

#### iOS端末で動作確認をする場合
__[【iOS】プッシュ通知の受信に必要な証明書の作り方(開発用)](https://github.com/NIFTYCloud-mbaas/iOS_Certificate)__
* 上記のドキュメントをご覧の上、必要な証明書類の作成をお願いします
* 証明書の作成には[Apple Developer Program](https://developer.apple.com/account/)の登録（有料）が必要です

![画像i002](/readme-img/i002.png)

### 1. [ニフティクラウドmobile backend](http://mb.cloud.nifty.com/)の会員登録とログイン→アプリ作成と設定
* 上記リンクから会員登録（無料）をします。登録ができたらログインをすると下図のように「アプリの新規作成」画面が出るのでアプリを作成します

![画像3](/readme-img/003.png)

* アプリ作成されると下図のような画面になります
* この２種類のAPIキー（アプリケーションキーとクライアントキー）はMonacaで作成するiOSアプリに[ニフティクラウドmobile backend](http://mb.cloud.nifty.com/)を紐付けるために使用します

![画像4](/readme-img/004.png)

* 続けてプッシュ通知の設定を行います

![画像5](/readme-img/005.png)

### 2. [Monaca](https://ja.monaca.io/)の会員登録とログイン→プロジェクトの作成
* 上記リンクから会員登録（無料）をします。登録ができたらログインします

![画像8](/readme-img/008.png)

* プロジェクト名を入力します
* 説明は空欄でOKです
* インポート方法は「URLを指定してインポート」を選択し、下記リンクを 右クリック してURLをコピーしたものを貼り付けてください
  * https://github.com/NIFTYCloud-mbaas/MonacaPushApp/archive/master.zip

![画像9](/readme-img/i038.png)

* 作成されたプロジェクトを「開く」をクリックして開きます

![画像6](/readme-img/006.png)

### 3. APIキーの設定

* `index.html`を編集します
* `YOUR_NCMB_APPLICATION_KEY`と`YOUR_NCMB_CLIENT_KEY`の部分を、先程[ニフティクラウドmobile backend](http://mb.cloud.nifty.com/)のダッシュボード上で確認したAPIキーに書き換えます
* また、Android端末で動作確認をする場合は、`YOUR_FCM_SENDER_ID`をFCMでプロジェクト作成時に発行されたSender ID(送信者ID)に書き換えます

![画像07](/readme-img/i034.png)

* このとき、ダブルクォーテーション（`"`）を消さないように注意してください！
* 書き換え終わったら「保存」をクリックして保存をします

![画像11](/readme-img/011.png)

### 4. 実機ビルド
* 動作確認を行う端末に応じて該当する作業を行ってください

#### Android端末で動作確認をする場合
* 「ビルド」＞「Androidアプリのビルド」をクリックして、Androidアプリケーションのビルドを開きます
* ｢デバッグビルド｣を選択して｢ビルドを開始する｣をクリックします
* 少し待つとビルドが完了します
* 任意の方法で端末にインストールをしてください

#### iOS端末で動作確認をする場合
* 「設定」＞「iOSビルド設定...」をクリックして、iOSビルド設定を開きます
* ⑦開発用証明書(秘密鍵.p12)を設定します

![画像i30](/readme-img/i032.png)

* ⑤で作成したプロビジョニングプロファイルを設定します

![画像i31](/readme-img/i033.png)

* 「ビルド」＞「iOSアプリのビルド」をクリックして、iOSアプリケーションのビルドを開きます
* ｢デバッグビルド｣を選択して｢ビルドを開始する｣をクリックします
* 少し待つとビルドが完了します
* 任意の方法で端末にインストールをしてください
 * インストール方法は、下記の参考欄に「iOSアプリのインストール方法」として記載していますのでご参照ください

### 5.動作確認
* インストールしたアプリを起動します
 * プッシュ通知の許可を求めるアラートが出たら、必ず許可してください！
* 起動されたらこの時点でAndroid端末はレジスタレーションID、iOS端末はデバイストークンが取得されます
* [ニフティクラウドmobile backend](http://mb.cloud.nifty.com/)のダッシュボードで「データストア」＞「installation」クラスを確認してみましょう！

![画像12](/readme-img/012.png)

* 端末側で起動したアプリは一度閉じておきます

### 6.__プッシュ通知を送りましょう！__
* いよいよです！実際にプッシュ通知を送ってみましょう！
* [ニフティクラウドmobile backend](http://mb.cloud.nifty.com/)のダッシュボードで「プッシュ通知」＞「＋新しいプッシュ通知」をクリックします
* プッシュ通知のフォームが開かれます
* 必要な項目を入力してプッシュ通知を作成します

![画像13](/readme-img/013.png)

* 端末を確認しましょう！
* 少し待つとプッシュ通知が届きます！！！

![画像17](/readme-img/017.png)

## 解説
サンプルプロジェクトに実装済みの内容のご紹介

#### SDKのインポートとCordvaプラグインの設定
* SDK・プラグインの更新も同様の作業で行えます

##### SDKのインポート
* Monacaで「設定」＞「JS/CSSコンポーネントの追加と削除...」を開きます
* 下図のようにSDKをインポートできます

![画像14](/readme-img/014.png)

##### Cordvaプラグインの設定
* Monacaで「設定」＞「Cordvaプラグインの管理...」を開きます
* プッシュ通知をアプリに実装する場合は以下のプラグインを有効にします

![画像15](/readme-img/i037.png)

#### ロジック
 * `index.html`の`<script></script>`タグ内にデバイストークンを取得し、[ニフティクラウドmobile backend](http://mb.cloud.nifty.com/)に保存するロジックを書いています

```js
document.addEventListener("deviceready", function(){
            // デバイストークンを取得してinstallationに登録する
            window.NCMB.monaca.setDeviceToken(
                "YOUR_NCMB_APPLICATIONKEY",
                "YOUR_NCMB_CLIENTKEY",
                "YOUR_FCM_SENDER_ID"
            );
        },false);
```

* 「`YOUR_NCMB_APPLICATIONKEY`」、「`YOUR_NCMB_CLIENTKEY`」はmobile backendのダッシュボードのアプリケーションキー、クライアントキーにそれぞれ書き換えてください
* Android端末で動作確認を行う場合は、「`YOUR_FCM_SENDER_ID`」をFCMでプロジェクト作成時に発行されたSenderID(送信者ID)に書き換えてください


## 参考
* ニフティクラウドmobile backend のドキュメントもご活用ください
 * [クイックスタート](http://mb.cloud.nifty.com/doc/current/introduction/quickstart_monaca.html)
 * [プッシュ通知](http://mb.cloud.nifty.com/doc/current/push/basic_usage_ios.html)

### iOSアプリのインストール方法
1. iTunesを使う方法
ダウンロードしたプロジェクト.ipaをドラッグ＆ドロップ

1. Xcodeを使う方法
http://docs.monaca.mobi/cur/ja/manual/deploy/non_market_deploy/

1. DeployGateを使う方法
アカウント（無料）を取得し、ダウンロードしたプロジェクト.ipaをドラッグ＆ドロップ
https://deploygate.com/
