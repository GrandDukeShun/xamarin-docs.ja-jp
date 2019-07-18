---
title: iOS クラッシュ ログにシンボル名を付加するための .dSYM ファイルはどこで入手できますか。
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: CB8607B9-FFDA-4617-8210-8E43EC512588
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 05/09/2018
ms.openlocfilehash: 0b8f3aa736cba6e70fbf346766499c23a9bbe270
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61418218"
---
# <a name="where-can-i-find-the-dsym-file-to-symbolicate-ios-crash-logs"></a>iOS クラッシュ ログにシンボル名を付加するための .dSYM ファイルはどこで入手できますか。

Mac または Visual Studio 2017 の Visual Studio での iOS アプリを構築する際にクラッシュ レポートのシンボル名を付加するために必要な .dSYM ファイルは、アプリのプロジェクト ファイル (.csproj) と同じディレクトリ階層に配置されます。 正確な場所は、プロジェクトのビルド設定によって異なります。

- デバイス固有のビルドを有効にした場合、次のディレクトリに、.dSYM を検出できます。

    **&lt;プロジェクト ディレクトリ&gt;/bin/&lt;プラットフォーム&gt;/&lt;構成&gt;/device-builds/&lt;デバイス&gt;- &lt;os バージョン&gt;/**

    例:
  
    **TestApp/bin/iPhone/Release/device-builds/iphone8.4-11.3.1/**

- デバイス固有のビルドを有効にしなかった、.dSYM 部分は次のディレクトリにあります。

    **&lt;プロジェクト ディレクトリ&gt;/bin/&lt;プラットフォーム&gt;/&lt;構成&gt;/**

    例:

    **TestApp/bin/iPhone/Release/**

> [!NOTE]
> ビルド プロセスの一環として、Visual Studio 2017 は、Windows、Mac ビルド ホストから .dSYM ファイルをコピーします。 Windows 上の .dSYM ファイルが表示されない場合は、アプリのビルド設定を構成したことを確認する[.ipa ファイルを作成する](~/ios/deploy-test/app-distribution/ipa-support.md)します。

## <a name="see-also"></a>関連項目

- [IOS クラッシュ ファイル (Xamarin.iOS) symbolicating](http://jmillerdev.net/symbolicating-ios-crash-files-xamarin-ios/)
- [IOS アプリケーションのクラッシュ ログの分かりやすい解説](https://www.raywenderlich.com/23704/demystifying-ios-application-crash-logs)

