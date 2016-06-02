# 【Monaca×mobile backend】プッシュ通知をカンタン実装！スピード感ある開発をしよう！

ハンズオンセミナー「【Monaca×mobile backend】プッシュ通知をカンタン実装！スピード感ある開発をしよう！」のコーディング時に使用するコピペ用ページです

* 別に配布の資料のページと一致する部分のコードのみ記載しています。
 * 事前準備資料（iOSのみ）：http://goo.gl/8wISOm
 * セミナー資料：http://goo.gl/NaI1rc
* 詳しい進め方等は資料をご覧ください。

## P52 index.html

```js
document.addEventListener("deviceready", function(){
            // デバイストークンを取得してinstallationに登録する
            window.NCMB.monaca.setDeviceToken(
                "YOUR_NCMB_APPLICATIONKEY",
                "YOUR_NCMB_CLIENTKEY",
                "PROJECT_NUMBER(Android_only)"
            );
        },false);
```

※「YOUR_NCMB_APPLICATIONKEY」、「YOUR_NCMB_CLIENTKEY」はmobile backendのダッシュボードのアプリケーションキー、クライアントキーにそれぞれ書き換えてください

※【Androidのみ】「PROJECT_NUMBER(Android_only)」はGCMのプロジェクト番号に書き換えてください


## 参考

### アプリのインストール方法

1. iTunesを使う方法
ダウンロードしたプロジェクト.ipaをドラッグ＆ドロップ

1. Xcodeを使う方法
詳しくはこちらhttp://docs.monaca.mobi/cur/ja/manual/deploy/non_market_deploy/

1. DeployGateを使う方法
アカウント（無料）を取得し、ダウンロードしたプロジェクト.ipaをドラッグ＆ドロップ
https://deploygate.com/
