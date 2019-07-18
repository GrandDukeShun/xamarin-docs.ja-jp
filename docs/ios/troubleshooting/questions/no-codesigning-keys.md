---
title: iOS のビルドが失敗して "no valid iPhone code signing keys found in keychain" (キーチェーンに有効な iPhone コード署名キーがありません) と表示されるのはなぜですか。
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 9DF24C46-D521-4112-9B21-52EA4E8D90D0
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 04/03/2018
ms.openlocfilehash: fe267db1f83695b3d0e8f3d828f91e01b56ba8ee
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61419666"
---
# <a name="why-does-my-ios-build-fail-with-no-valid-iphone-code-signing-keys-found-in-keychain"></a>iOS のビルドが失敗して "no valid iPhone code signing keys found in keychain" (キーチェーンに有効な iPhone コード署名キーがありません) と表示されるのはなぜですか。

## <a name="cause-of-the-error"></a>エラーの原因
このエラー メッセージは、対象のプロジェクトが有効なコード署名の資格情報を検索するときに発生しますが、それらを検索することができません。 コード署名は、テストと物理 iOS デバイスに展開するために必要です。だけでなく、アドホックとアプリのビルドを格納します。 


### <a name="provisioning-devices"></a>デバイスのプロビジョニング
前に、iOS デバイスをプロビジョニングしていない場合、次のガイドを実行、完全なステップ バイ ステップのプロセス。[デバイス プロビジョニング ガイド](~/ios/get-started/installation/device-provisioning/index.md)


## <a name="bug-when-using-ios-simulator"></a>IOS シミュレーターを使用しているときのバグ

> [!NOTE]
> Visual Studio の Xamarin の最近のバージョンでこの問題を解決されています。 ただし、ソフトウェアの最新バージョンで問題が発生した場合を提出してください、[新しいバグ](~/cross-platform/troubleshooting/questions/howto-file-bug.md)完全なバージョン管理情報と完全のビルド ログ出力します。


Codesign シミュレーターに Entitlements.plist ビルド; を追加する Xamarin.Forms テンプレートで iOS プロジェクトの原因となった Xamarin.Visual Studio 3.11 にバグが発生しましたシミュレーターを使用したテストが効果的にブロックします。

### <a name="how-to-fix"></a>修正する方法
削除することで問題を回避することができます、`<CodesignEntitlements>`の .csproj ファイルにデバッグからフラグを作成します。 このことは次のように実行できます。

*警告: これを試みる前に、ファイルをバックアップすることをお勧め、.csproj ファイル内のエラーは、プロジェクトを分割できます。*

1. ソリューション ウィンドウで、iOS プロジェクトを右クリックし、選択**プロジェクトのアンロード**
2. プロジェクトを再び右クリックし、選択 **[ProjectName] .csproj の編集**
3. デバッグ Propertygroup を見つけ、次のようにするフラグで開始する必要があります。
   - デバッグ: `<PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|iPhoneSimulator' ">`
   - リリース: `<PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|iPhoneSimulator' ">`
4. 各シミュレーターを使用するビルドを削除またはコメント アウト、次のプロパティ。 `<CodesignEntitlements>Entitlements.plist</CodesignEntitlements>`
5. プロジェクトを再読み込みされ、シミュレーターに配置できる必要があります。

### <a name="next-steps"></a>次の手順
問い合わせ、または上記の情報を使用した後でもこの問題が残っている場合を参照してください、詳細については[Xamarin のどのようなサポート オプションを使用しますか?](~/cross-platform/troubleshooting/support-options.md)連絡先オプション、推奨事項は、についてする方法についても必要な場合は、新しいバグをファイルします。 
