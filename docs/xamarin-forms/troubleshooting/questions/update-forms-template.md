---
title: Xamarin.Forms の既定のテンプレートを新しい NuGet パッケージに更新することはできますか。
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 160FBE13-26EB-4B4F-9248-A5CBE58FDD7F
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/25/2017
ms.openlocfilehash: e439d39dd8591cad14485e64aabab2d6016a8e27
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61345912"
---
# <a name="can-i-update-the-xamarinforms-default-template-to-a-newer-nuget-package"></a>Xamarin.Forms の既定のテンプレートを新しい NuGet パッケージに更新することはできますか。

このガイドは、例として、Xamarin.Forms .NET Standard ライブラリ テンプレートを使用しますが、同じ一般的な方法は、Xamarin.Forms 共有プロジェクト テンプレートの動作も。 このガイドは、Xamarin.Forms 1.5.1.6471 に 2.1.0.6529 から更新の例で記述されたが、同じ手順は他のバージョンを代わりに、既定として設定すること。

1.  元のテンプレートをコピーして`.zip`から。

    > `C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Xamarin\Xamarin\[Xamarin Version]\T\PT\Cross-Platform\Xamarin.Forms.PCL.zip`

2.  解凍、`.zip`一時的な場所にします。

3.  使用するには新しいバージョンには、すべてのフォーム パッケージの古いバージョンの出現回数を変更します。
    *   `FormsTemplate\FormsTemplate.vstemplate`
    *   `FormsTemplate.Android\FormsTemplate.Android.vstemplate`
    *   `FormsTemplate.iOS\FormsTemplate.iOS.vstemplate`

    例: `<package id="Xamarin.Forms" version="1.5.1.6471" />` -> `<package id="Xamarin.Forms" version="2.1.0.6529" />`

4.  メインの"name"要素を変更する[複数プロジェクトのテンプレート ファイル](https://msdn.microsoft.com/library/ms185308.aspx)(`Xamarin.Forms.PCL.vstemplate`) 一意になるようにします。 例えば:
    > <Name>Blank App (Xamarin.Forms Portable) - 2.1.0.6529</Name>

5.  再全体のテンプレート フォルダーを zip 圧縮します。 元のファイル構造と一致することを確認、`.zip`ファイル。 `Xamarin.Forms.PCL.vstemplate`の上部にあるファイルがあります、`.zip`ファイル、フォルダー内にありません。

6.  ユーザーごとの Visual Studio のテンプレート フォルダーで「モバイル アプリ」サブディレクトリを作成します。
    > `%USERPROFILE%\Documents\Visual Studio 2013\Templates\ProjectTemplates\Visual C#\Mobile Apps`

7.  新しい「モバイル アプリ」ディレクトリに、新しい zip 形式のテンプレート フォルダーをコピーします。

8.  手順 3 からバージョンに対応する NuGet パッケージをダウンロードします。 たとえば、 [ http://nuget.org/api/v2/package/Xamarin.Forms/2.1.0.6529 ](http://nuget.org/api/v2/package/Xamarin.Forms/2.1.0.6529) (も参照してください[ https://stackoverflow.com/questions/8597375/how-to-get-the-url-of-a-nupkg-file ](https://stackoverflow.com/questions/8597375/how-to-get-the-url-of-a-nupkg-file))、Xamarin Visual Studio 拡張機能フォルダーの適切なサブフォルダーにコピーします。
    > `C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Xamarin\Xamarin\[Xamarin Version]\Packages`
