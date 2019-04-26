---
title: GridViewPager
ms.prod: xamarin
ms.assetid: A1CDD5F0-049B-4DFA-A268-8A875D26A675
ms.technology: xamarin-android
author: conceptdev
ms.author: crdun
ms.date: 02/02/2018
ms.openlocfilehash: 81bb4e302f81b58eec91ea2a2aef985adbf72e2c
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61285288"
---
# <a name="gridviewpager"></a>GridViewPager

[GridViewPager](https://developer.xamarin.com/samples/GridViewPager/) Android Wear の 2D ピッカーのナビゲーション パターンを実装する方法を示します。

![正方形の表示で GridViewPager の例のスクリーン ショット](gridviewpager-images/gridviewpager.png)

最初に追加、 [Xamarin Android Wear サポート](https://www.nuget.org/packages/Xamarin.Android.Wear/)をプロジェクトに NuGet パッケージ。

レイアウト XML は、ようになります。

```xml
<android.support.wearable.view.GridViewPager xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/pager"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:keepScreenOn="true" />
```

作成します。 [`GridPagerAdapter`](https://developer.android.com/reference/android/support/wearable/view/GridPagerAdapter.html)
(またはサブクラスなど [`FragmentGridPagerAdapter`](https://developer.android.com/reference/android/support/wearable/view/FragmentGridPagerAdapter.html)
ユーザーとして表示するビューを提供する次のように移動します。

[サンプル アダプター](https://github.com/xamarin/monodroid-samples/blob/master/wear/GridViewPager/GridViewPager/SimpleGridPagerAdapter.cs)の上書きを含めて、必要なメソッドを実装する方法を示します`RowCount`、 `GetColumnCount`、`GetBackground`と `GetFragment`

示すように、アダプターを接続します。

```csharp
pager.Adapter = new SimpleGridPagerAdapter (this, FragmentManager);
```



## <a name="related-links"></a>関連リンク

- [Google の 2D ピッカー ドキュメント](https://developer.android.com/training/wearables/ui/2d-picker.html)
- [android.support.wearable docs](https://developer.android.com/reference/android/support/wearable/view/package-summary.html)
- [GridViewPager (sample)](https://developer.xamarin.com/samples/GridViewPager/)
