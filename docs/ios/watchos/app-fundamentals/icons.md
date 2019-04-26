---
title: WatchOS で Xamarin のアイコンの使用
description: このドキュメントでは、watchOS アプリケーションおよびこれらのアイコンを含むようにソリューションを設定する方法に必要なさまざまなアイコンについて説明します。
ms.prod: xamarin
ms.assetid: EE3D45BD-8091-4C04-BA83-371371D8BEB9
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 07/26/2018
ms.openlocfilehash: 435af10484827826d53b767c2738e3945e0bae42
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61345241"
---
# <a name="working-with-watchos-icons-in-xamarin"></a>WatchOS で Xamarin のアイコンの使用

Apple Watch のソリューションには、2 つのアイコンのセットが必要です。

* IPhone で表示される iOS アプリのアイコン。
* Apple Watch 通知画面と [ウォッチ] メニューの円で表示されるアイコン。 Watch アプリのアイコンにも表示されます、 [Apple Watch](~/ios/watchos/app-fundamentals/settings.md) iOS アプリ。

## <a name="apple-watch-icons"></a>Apple Watch のアイコン

| | | |
|-|-|-|
|iOS アプリのアイコン|IPhone で表示され、親アプリを起動|![iOS アプリのアイコン](icons-images/icon-ios.png)|
|アプリのアイコンをご覧ください。|Apple Watch ホーム画面に表示されます。|![watchOS アプリのアイコン](icons-images/icon-home.png)|
||ウォッチの通知が表示されます。|![watchOS の通知アイコン](icons-images/notification-icon.png)|
||表示されます、 [iOS Apple Watch アプリ](~/ios/watchos/app-fundamentals/settings.md)|![iOS Watch アプリ アイコン](icons-images/watch-app-sml.png)|

## <a name="configuring-your-solution"></a>ソリューションを構成します。

IOS アプリと watch アプリは、正しい名前とアイコンを表示するためには、各プロジェクトに次の手順に従います。

### <a name="ios-app"></a>iOS アプリ

参照してください、 [iOS アプリケーションのアイコンのガイド](~/ios/app-fundamentals/images-icons/app-icons.md)に iOS アプリのアイコンが正しく構成されていることを確認します。

#### <a name="infoplist"></a>Info.plist

Watch アプリで横に表示される文字列、 [Apple Watch の設定 アプリ](~/ios/watchos/app-fundamentals/settings.md)で構成されている場合は、 **iOS アプリの Info.plist**します。

いることを確認、 **Info.plist**が、`CFBundleName`キーと値 (注: これとは異なります、 `CFBundleDisplayName`、両方があることができます)。

```xml
<key>CFBundleName</key>
<string>Your App Name</string>
```

### <a name="apple-watch-app"></a>Apple Watch アプリ

1 回、[親アプリ](~/ios/watchos/app-fundamentals/parent-app.md)watch アプリにアプリケーション アイコンのアセット カタログを追加する必要がありますが、アイコンが構成されます。

1. Watch アプリのプロジェクトを右クリックし、選択**ファイル > 追加 > 新しいファイル... > iOS > 資産カタログ**アセット カタログをプロジェクトに追加します。

 ![](icons-images/newasset.png "アセット カタログをプロジェクトに追加します。")

2. ダブルクリックして、 **AppIcon.appiconset/Contents.json**ファイル

  ![](icons-images/xcassets-iconset-sml.png "AppIcon 内容")

3. このスクリーン ショットで示すように、すべての watchOS イメージを追加します。

  [![](icons-images/appicons-sml.png "このスクリーン ショットで示すように、すべての watchOS イメージを追加します。")](icons-images/appicons.png#lightbox)

  参照してください[Apple のアイコンのガイドライン](https://developer.apple.com/design/human-interface-guidelines/watchos/icons-and-images/menu-icons/)(寸法が画面の表示も)、必要なサイズにします。 円で表示するためにこれらのアイコンを自動的にクリップすることに注意してください。

  アイコンの一覧は、次のようになります。

  ![](icons-images/xcassets-complete-sml.png "ソリューション エクスプ ローラーでアイコンの一覧")

4. 資産カタログが、アプリに含まれることを確認するには、次のキーを追加し、値を**Watch アプリの Info.plist**:

```xml
<key>XSAppIconAssets</key>
<string>Images.xcassets/AppIcon.appiconset</string>
```

アイコンがチェックして適切な構成を確認することができます、 [Apple Watch の設定 アプリ](~/ios/watchos/app-fundamentals/settings.md)iPhone シミュレーターで生成するか、[通知](~/ios/watchos/platform/notifications.md)通知に表示されるアイコンを確認します。画面。

> [!NOTE]
> アイコンは、アルファ チャネル (アプリは拒否されますアプリ ストアの送信中に、アルファ チャネルが存在する場合) を含めることはできません。 アルファ チャネルが存在し、削除するかどうかにチェックすることができます[プレビュー アプリを使用して、Mac OS X で](~/ios/watchos/troubleshooting.md#noalpha)します。


## <a name="related-links"></a>関連リンク

- [Apple の watchOS のアイコンとイメージのガイド](https://developer.apple.com/design/human-interface-guidelines/watchos/icons-and-images/)
