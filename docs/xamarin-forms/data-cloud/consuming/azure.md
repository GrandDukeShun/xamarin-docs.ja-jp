---
title: Azure Mobile Appsの使用
description: これは Node.js バックエンドを使用する Azure のモバイル アプリに適用できるのみ、この記事では、クエリ、挿入、更新、および Azure Mobile Apps インスタンス内のテーブルに格納されたデータを削除する方法について説明します。
ms.prod: xamarin
ms.assetid: 2B3EFD0A-2922-437D-B151-4B4DE46E2095
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 09/20/2016
ms.openlocfilehash: 8bd77ec4975fae3cc7245c5adc2b5ef18568b9e1
ms.sourcegitcommit: 57e8a0a10246ff9a4bd37f01d67ddc635f81e723
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2019
ms.locfileid: "57667583"
---
# <a name="consuming-an-azure-mobile-app"></a>Azure Mobile Appsの使用

[![サンプルのダウンロード](~/media/shared/download.png)サンプルをダウンロードします。](https://developer.xamarin.com/samples/xamarin-forms/WebServices/TodoAzure/)

_Azure Mobile Appsでは、モバイル認証、オフライン同期、およびプッシュ通知のサポートにより、Azure App Serviceでホストされているスケーラブルなバックエンドでアプリを開発できます。この記事は、Azure Mobile AppsでNode.jsバックエンドを使用する場合にのみ適用され、Azure Mobile Appsインスタンスのテーブルに格納されたデータのクエリ、挿入、更新、および削除方法について説明しています。_ 


> [!NOTE]
> 6 月 30 日以降は、すべての新しい Azure モバイル アプリが作成されます TLS 1.2 を既定では。 さらもをお勧めする既存の Azure Mobile Apps TLS 1.2 を使用するように再構成します。 Azure モバイル アプリで TLS 1.2 を適用する方法については、次を参照してください。[適用の TLS バージョン](/azure/app-service/app-service-web-tutorial-custom-ssl#enforce-tls-versions)します。 TLS 1.2 を使用する Xamarin プロジェクトを構成する方法については、次を参照してください。[トランスポート層セキュリティ (TLS) 1.2](~/cross-platform/app-fundamentals/transport-layer-security.md)します。

Xamarin.Forms で利用できる Azure Mobile Apps インスタンスを作成する方法については、 [Xamarin.Forms アプリを作成する](https://azure.microsoft.com/documentation/articles/app-service-mobile-xamarin-forms-get-started/) を参照してください。 これらの手順に従うと、後に設定して、Azure Mobile Apps インスタンスを使用するダウンロード可能なサンプル アプリケーションを構成できます。`Constants.ApplicationURL` Azure Mobile Apps インスタンスの URL にします。 次に、サンプル アプリケーションを実行すると、次のスクリーン ショットに示すように、Azure Mobile Apps インスタンスに接続します。

![](azure-images/portal.png "サンプル アプリケーション")

Azure Mobile Apps へのアクセスは、 [Azure Mobile Client SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/) を介して行われ、Xamarin.FormsサンプルアプリケーションからAzureへのすべての接続はHTTPS経由で行われます。

> [!NOTE]
> iOS 9 以降では、アプリのトランスポート セキュリティ (ATS) は、機密情報の誤った情報開示を回避をセキュリティで保護された接続 (アプリのバック エンド サーバーなど) のインターネット リソースと、アプリの間に強制します。   ATS が iOS 9 用にビルドされたアプリで既定で有効になるために、すべての接続は ATS セキュリティ要件に応じたされます。 接続はこれらの要件を満たしていない場合は、例外で失敗します。
> 使用することができない場合の ATS を選択することができます、`HTTPS`プロトコルし、インターネット リソースのための通信をセキュリティで保護します。 これは、アプリの更新することで実現できます**Info.plist**ファイル。 詳細については、次を参照してください。[アプリ トランスポート セキュリティ](~/ios/app-fundamentals/ats.md)します。

## <a name="consuming-an-azure-mobile-app-instance"></a>Azure Mobile App インスタンスの使用

[Azure Mobile Client SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)が提供する`MobileServiceClient`クラスは、次のコード例に示すように Azure Mobile Apps インスタンスへのアクセスするために Xamarin.Forms アプリケーションによって使用されます。

```csharp
IMobileServiceTable<TodoItem> todoTable;
MobileServiceClient client;

public TodoItemManager ()
{
  client = new MobileServiceClient (Constants.ApplicationURL);
  todoTable = client.GetTable<TodoItem> ();
}
```

ときに、`MobileServiceClient`インスタンスが作成されると、Azure Mobile Apps のインスタンスを識別するために、アプリケーションの URL を指定する必要があります。 モバイル アプリのダッシュ ボードからこの値を取得することができます、 [Microsoft Azure Portal](https://portal.azure.com/)します。

参照、`TodoItem`そのテーブルに対して操作を実行できるされる前に、Azure Mobile Apps インスタンスに格納されているテーブルを取得する必要があります。 これは、呼び出すことによって実現されます、`GetTable`メソッドを`MobileServiceClient`インスタンスを返す、`IMobileServiceTable<TodoItem>`参照。

### <a name="querying-data"></a>データのクエリ

テーブルの内容を呼び出すことによって取得できます、`IMobileServiceTable.ToEnumerableAsync`メソッドを非同期的にクエリを評価し、結果が返されます。 データを含めることによってサーバー側をフィルター処理、`Where`クエリ内の句。 `Where`次のコード例に示すように、句が、行のフィルタ リング、テーブルに対するクエリに述語を適用します。

```csharp
public async Task<ObservableCollection<TodoItem>> GetTodoItemsAsync (bool syncItems = false)
{
  ...
  IEnumerable<TodoItem> items = await todoTable
              .Where (todoItem => !todoItem.Done)
              .ToEnumerableAsync ();

  return new ObservableCollection<TodoItem> (items);
}
```

このクエリからすべての項目を返します、`TodoItem`テーブルです`Done`プロパティは等しく`false`します。 クエリの結果に配置し、`ObservableCollection`表示用です。

### <a name="inserting-data"></a>データの挿入

Azure Mobile Apps のインスタンスでデータを挿入するときに新しい列が自動的に生成する必要に応じて、テーブル内の提供、Azure Mobile Apps のインスタンスでその動的スキーマが有効にします。 `IMobileServiceTable.InsertAsync`の次のコード例に示すように、指定したテーブルに新しいデータの行を挿入するメソッドを使用します。

```csharp
public async Task SaveTaskAsync (TodoItem item)
{
  ...
  await todoTable.InsertAsync (item);
  ...
}
```

挿入リクエストを行うときに、ID を Azure Mobile Apps インスタンスに渡されるデータで指定されている必要があります。  挿入リクエストには、ID が含まれている場合、`MobileServiceInvalidOperationException`がスローされます。

後に、`InsertAsync`メソッドが完了するで Azure Mobile Apps のインスタンス内のデータの ID が設定されて、 `TodoItem` Xamarin.Forms アプリケーションのインスタンス。

### <a name="updating-data"></a>データの更新

Azure Mobile Apps のインスタンス内のデータを更新するときに新しい列が自動的に生成する必要に応じて、テーブル内の提供、Azure Mobile Apps のインスタンスでその動的スキーマが有効にします。 `IMobileServiceTable.UpdateAsync`の次のコード例に示すように、新しい情報で既存のデータを更新するメソッドを使用します。

```csharp
public async Task SaveTaskAsync (TodoItem item)
{
  ...
  await todoTable.UpdateAsync (item);
  ...
}
```

更新リクエストを行うときは、Azure Mobile Apps インスタンスは、更新するデータを識別できるように ID を指定してください。 この ID の値が格納されている、`TodoItem.ID`プロパティです。  更新のリクエストが含まれていない ID には更新するには、Azure Mobile Apps インスタンス データを決定する方法はありません、そのため、`MobileServiceInvalidOperationException`がスローされます。

### <a name="deleting-data"></a>データの削除

`IMobileServiceTable.DeleteAsync`の次のコード例に示すように、Azure Mobile Apps テーブルからデータを削除するメソッドを使用します。

```csharp
public async Task DeleteTaskAsync (TodoItem item)
{
  ...
  await todoTable.DeleteAsync(item);
  ...
}
```

削除リクエストを行うときは、Azure Mobile Apps インスタンス が削除されるデータを識別できるように、ID を指定してください。 この ID の値が格納されている、`TodoItem.ID`プロパティです。 削削除リクエストに ID が含まれていない場合は、Azure Mobile Apps インスタンスが削除するデータを決定する方法はありませんので、`MobileServiceInvalidOperationException`がスローされます。

## <a name="summary"></a>まとめ

この記事では、Azure Mobile Apps インスタンス内のテーブルに格納されたデータをクエリ、挿入、更新、および 削除する際の[Azure Mobile Client SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)の使用方法を説明しました。 このSDKはAzure Mobile Apps インスタンスにアクセスするためにXamarin.Forms アプリケーションによって使用される `MobileServiceClient` クラスを提供します。


## <a name="related-links"></a>関連リンク

- [TodoAzure (サンプル)](https://developer.xamarin.com/samples/xamarin-forms/WebServices/TodoAzure/)
- [Xamarin.Forms アプリを作成します。](https://azure.microsoft.com/documentation/articles/app-service-mobile-xamarin-forms-get-started/)
- [Azure Mobile Client SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
- [MobileServiceClient](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx)
