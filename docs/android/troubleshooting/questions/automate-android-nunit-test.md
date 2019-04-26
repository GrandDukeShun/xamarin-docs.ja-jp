---
title: Android NUnit テスト プロジェクトを自動化する方法を教えてください
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: EA3CFCC4-2D2E-49D6-A26C-8C0706ACA045
ms.technology: xamarin-android
author: conceptdev
ms.author: crdun
ms.date: 03/29/2018
ms.openlocfilehash: b785ef171d2cb00d4f8f5a17f37d49de17fd3da9
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61153296"
---
# <a name="how-do-i-automate-an-android-nunit-test-project"></a>Android NUnit テスト プロジェクトを自動化する方法を教えてください

> [!NOTE]
> このガイドでは、Android NUnit テスト プロジェクトの Xamarin.UITest プロジェクトではないを自動化する方法について説明します。 Xamarin.UITest ガイド[ここ](https://docs.microsoft.com/appcenter/test-cloud/preparing-for-upload/uitest)します。

作成するときに、**単体テスト アプリ (Android)** Visual Studio でプロジェクト (または**Android 単体テスト**Visual Studio for Mac でプロジェクト)、このプロジェクトは、自動的に既定では、テストを実行します。
作成することができます、ターゲット デバイスでの NUnit テストを実行する、 [Android.App.Instrumentation](https://developer.xamarin.com/api/type/Android.App.Instrumentation/)によって次のコマンドを使用して開始されたサブクラスです。 

```shell
adb shell am instrument 
```

次の手順では、このプロセスについて説明します。

1.  という新しいファイルを作成**TestInstrumentation.cs**: 

    ```cs 
    using System;
    using System.Reflection;
    using Android.App;
    using Android.Content;
    using Android.Runtime;
    using Xamarin.Android.NUnitLite;
     
    namespace App.Tests {
     
        [Instrumentation(Name="app.tests.TestInstrumentation")]
        public class TestInstrumentation : TestSuiteInstrumentation {
     
            public TestInstrumentation (IntPtr handle, JniHandleOwnership transfer) : base (handle, transfer)
            {
            }
     
            protected override void AddTests ()
            {
                AddTest (Assembly.GetExecutingAssembly ());
            }
        }
    }
    ```
    このファイルで[Xamarin.Android.NUnitLite.TestSuiteInstrumentation](https://developer.xamarin.com/api/type/Xamarin.Android.NUnitLite.TestSuiteInstrumentation/) (から**Xamarin.Android.NUnitLite.dll**) を作成するサブクラス化は`TestInstrumentation`します。

2.  実装、 [TestInstrumentation](https://developer.xamarin.com/api/constructor/Xamarin.Android.NUnitLite.TestSuiteInstrumentation.TestSuiteInstrumentation/p/System.IntPtr/Android.Runtime.JniHandleOwnership/)コンス トラクターと[AddTests](https://developer.xamarin.com/api/member/Xamarin.Android.NUnitLite.TestSuiteInstrumentation.AddTests%28%29)メソッド。 `AddTests`メソッドのコントロールが実際にテストを実行します。

3.  変更、`.csproj`ファイルを追加する**TestInstrumentation.cs**します。 例:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Project DefaultTargets="Build" ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
        ...
        <ItemGroup>
            <Compile Include="TestInstrumentation.cs" />
        </ItemGroup>
        <Target Name="RunTests" DependsOnTargets="_ValidateAndroidPackageProperties">
            <Exec Command="&quot;$(_AndroidPlatformToolsDirectory)adb&quot; $(AdbTarget) $(AdbOptions) shell am instrument -w $(_AndroidPackage)/app.tests.TestInstrumentation" />
        </Target>
        ...
    </Project>
    ```

3.  単体テストを実行するのにには、次のコマンドを使用します。 置換`PACKAGE_NAME`アプリのパッケージ名を持つ (アプリのパッケージ名が見つかりません`/manifest/@package`属性にある**AndroidManifest.xml**)。

    ```shell
    adb shell am instrument -w PACKAGE_NAME/app.tests.TestInstrumentation
    ```

4.  必要に応じて変更することができます、`.csproj`を追加するファイル、 `RunTests` MSBuild ターゲット。 これにより、次のようなコマンドを使用して単体テストを起動できるようにします。

    ```shell
    msbuild /t:RunTests Project.csproj
    ```
    (は、この新しいターゲットを使用している必要はありません以前、`adb`の代わりにコマンドを使用できる`msbuild`。)。

使用しての詳細については、`adb shell am instrument`単体テストを実行し、Android の開発者を参照してくださいコマンド[ADB によるテストの実行](https://developer.android.com/studio/test/command-line.html#RunTestsDevice)トピック。


> [!NOTE]
> [Xamarin.Android 5.0](https://developer.xamarin.com/releases/android/xamarin.android_5/xamarin.android_5.1/#Android_Callable_Wrapper_Naming)リリースの場合は、エクスポートされる型のアセンブリ修飾名の md5 チェックサムに基づいて Android 呼び出し可能ラッパーは、既定のパッケージ名。 これにより、2 つの異なるアセンブリから指定して、パッケージのエラーを取得できませんに同じ完全修飾名です。 これを使用することを確認、`Name`プロパティを`Instrumentation`属性が読み取り可能なについて/クラス名を生成します。

_についての名前を使用する必要があります、`adb`上記のコマンド_します。
名前変更リファクタリング、C#クラスは、変更する必要がありますので、`RunTests`コマンドについての正しい名前を使用します。

