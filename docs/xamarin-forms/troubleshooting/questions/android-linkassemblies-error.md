---
title: Android のビルド エラー – The LinkAssemblies タスクが予期せず失敗しました
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: EB3BE685-CB72-48E3-89D7-C845E76B9FA2
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/25/2017
ms.openlocfilehash: b027dd23b9144a865bc16b55ebac71855bae0725
ms.sourcegitcommit: 817d26585093cd180a36b28179eb354b0eb900b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2019
ms.locfileid: "55292039"
---
# <a name="android-build-error--the-linkassemblies-task-failed-unexpectedly"></a>Android のビルド エラー – The LinkAssemblies タスクが予期せず失敗しました

エラー メッセージが表示することがあります`The "LinkAssemblies" task failed unexpectedly`Xamarin.Android プロジェクトのビルドがフォームを使用している場合。 リンカーは、アクティブな場合 (通常で、*リリース*アプリ パッケージのサイズを小さくビルド); Android ターゲットが最新のフレームワークに更新されないために発生するとします。 (詳細については。[Android の要件の Xamarin.Forms](~/get-started/installation.md#android))

この問題を解決最新サポート対象の Android SDK バージョンがあり、設定するかどうかを確認するには、**ターゲット フレームワーク**に**使用がインストールされている最新のプラットフォーム**します。 またに設定することをお勧め、**ターゲット Android バージョン**に**ターゲット フレームワーク バージョンを使用して**と**最小 Android バージョン**API 15 以降。 これは、サポートされる構成と見なされます。

## <a name="setting-in-visual-studio-for-mac"></a>Visual Studio for Mac 設定

1.  Android プロジェクトを右クリックします。
2.  移動して**ビルド > [全般] > フレームワークをターゲットに**します。
3.  設定、**フレームワークをターゲットにします。使用してインストールされている最新のプラットフォーム**します。
4.  プロジェクトのオプションの中に移動します。**ビルド > Android アプリケーション**します。
5.  設定、 **Minimum Android version** API レベル 15 以上に (&)、 **Target Android version**に**自動 - ターゲット フレームワーク バージョンを使用して**します。

## <a name="setting-in-visual-studio"></a>Visual Studio での設定

1.  Android プロジェクトを右クリックします。
2.  移動して**アプリケーション**プロジェクト オプション。
3.  設定、 **Android バージョンを使用してコンパイル** & **Target Android version**設定**最新のプラットフォームを使用** / **使用SDK のバージョンを使用してコンパイル**します。
4.  設定、**最小 Android ターゲット**API 19 以上を設定します。

これらの設定を更新した後は、クリーンアップ、変更内容が取り出されることを確認するようにプロジェクトを再構築してください。
