---
title: Xamarin ファイアウォールの構成手順
description: このドキュメントでは、企業環境で Xamarin が機能するように、ファイアウォールでホワイトリストに登録する必要があるホストのリストを示します。
ms.prod: xamarin
ms.assetid: 658f699b-8cca-48f7-ae54-fa956384b6d6
author: asb3993
ms.author: amburns
ms.date: 10/05/2018
ms.openlocfilehash: 68689ce7d92a038d0724e1441f68fddcb1d0bba8
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61346862"
---
# <a name="xamarin-firewall-configuration-instructions"></a>Xamarin ファイアウォールの構成手順

_会社で Xamarin のプラットフォームが機能するように、ファイアウォールでホワイトリストに登録するのに必要なホストのリスト。_

Xamarin 製品をインストールし、製品が正常に動作するには、ソフトウェアに必要なツールと更新プログラムをダウンロードできるように、特定のエンドポイントをアクセス可能にする必要があります。 管理者または会社がファイアウォール設定を厳格にしている場合は、インストール、ライセンス、コンポーネントなどで問題が発生する可能性があります。 このドキュメントでは、Xamarin が動作するためにホワイトリストに登録する必要があるいくつかの既知のエンドポイントについて概要を説明します。 このホワイトリストには、ダウンロードに含まれるすべてのサードパーティ ツールに必要なエンドポイントを含めません。 このリストを使用しても問題が解決しない場合は、Apple または Android のインストールに関するトラブルシューティング ガイドを参照してください。

## <a name="endpoints-to-whitelist"></a>ホワイトリストに登録するエンドポイント

### <a name="xamarin-installer"></a>Xamarin インストーラー

最新リリースの Xamarin インストーラーを使用するときにソフトウェアを適切にインストールするには、次の既知のアドレスを追加する必要があります。

- xamarin.com (インストーラーのマニフェスト)
- dl.xamarin.com (パッケージのダウンロード場所)
- dl.google.com (Android SDK をダウンロードする場合)
- download.oracle.com (JDK)
- visualstudio.com (セットアップ パッケージのダウンロード場所)
- go.microsoft.com (セットアップ URL の解決)
- aka.ms (セットアップ URL の解決)

Mac を使用していて Xamarin.Android のインストールの問題が発生している場合は、macOS が Java をダウンロードできることを確認してください。

### <a name="nuget-including-xamarinforms"></a>NuGet (Xamarin.Forms を含む)

NuGet にアクセスするには、次のアドレスを追加する必要があります (Xamarin.Forms は NuGet としてパッケージ化されています)。

- www\.nuget.org (NuGet にアクセスする場合)
- az320820.vo.msecnd.net (NuGet のダウンロード)
- dl-ssl.google.com (Android および Xamarin.Forms 用 Google コンポーネント)

### <a name="software-updates"></a>ソフトウェア更新プログラム

ソフトウェア更新プログラムを適切にダウンロードするには、次のアドレスを追加する必要があります。

- software.xamarin.com (更新機能サービス)
- download.visualstudio.microsoft.com
- dl.xamarin.com

## <a name="xamarin-mac-agent"></a>Xamarin Mac エージェント

Xamarin Mac エージェントを使用して Visual Studio を Mac ビルド ホストに接続するには、SSH ポートを開く必要があります。 この既定値は**ポート 22** です。

## <a name="summary"></a>まとめ

このガイドでは、Xamarin 製品をコンピューターに適切にインストールし、更新するためにホワイトリストに登録する必要があるエンドポイントについて説明しました。
