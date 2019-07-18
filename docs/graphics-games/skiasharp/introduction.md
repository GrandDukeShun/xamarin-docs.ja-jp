---
title: SkiaSharp のプラットフォームに依存しない例
description: このドキュメントでは、中核となる SkiaSharp の概念の概要を示します。 具体的には、取得して、SKCanvas 上に描画について説明します。
ms.prod: xamarin
ms.techonology: xamarin-skiasharp
ms.assetid: 19506F08-2603-465E-A806-6BD01638DE90
author: davidbritch
ms.author: dabritch
ms.date: 10/03/2018
ms.openlocfilehash: 4d0e57b98a479112b9fdf4f9c503418f3966cc73
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61158890"
---
# <a name="skiasharp-platform-independent-examples"></a>SkiaSharp のプラットフォームに依存しない例

_これにより、プラットフォームに依存しない SkiaSharp の概念の概要_

SkiaSharp、豊富で強力な 2D グラフィックスを 2D のバッファーに表示するために使用できる API を提供します。  カスタム ユーザー インターフェイス要素や、アプリケーションに組み込むことが 2D グラフィックスを実装するために、これらを使用することができます。 SkiaSharp は .NET へのバインドを[Skia](https://skia.org)ライブラリ機能とこのライブラリの電源を継承します。

ライブラリは現在、クロス プラットフォームとして提供[NuGet パッケージ](https://www.nuget.org/packages/SkiaSharp)、NuGet 参照を追加することで、プロジェクトに追加できます。

を描画するために、コードは、作成、 `SkCanvas` 、画面の描画操作を行う場所について説明します。

## <a name="obtaining-an-skcanvas"></a>SKCanvas を取得します。

```csharp
using (var surface = SKSurface.Create (width: 640, height: 480, SKImageInfo.PlatformColorType, SKAlphaType.Premul)) {
    SKCanvas myCanvas = surface.Canvas;

    // Your drawing code goes here.
}
```

## <a name="drawing-on-skcanvas"></a>SKCanvas の描画

`SKCanvas`は描画のモデルを他の描画に似たモデルで使い慣れていたかもしれないこと、透明度の省略可能なチャネルを持つ色を使用し、線、円弧、テキストおよびイメージを描画できます。

SkiaSharp で実行できる多くのさまざまなことのほんの一部を次に示します。  変数の下の例で`canvas`SKCanvas 型です。

### <a name="drawing-xamagon"></a>描画 Xamagon

この例では、Xamarin のロゴ、Xamagon 描画します。

```csharp
// clear the canvas / fill with white
canvas.Clear (SKColors.White);

// set up drawing tools
using (var paint = new SKPaint ()) {
  paint.IsAntialias = true;
  paint.Color = new SKColor (0x2c, 0x3e, 0x50);
  paint.StrokeCap = SKStrokeCap.Round;

  // create the Xamagon path
  using (var path = new SKPath ()) {
    path.MoveTo (71.4311121f, 56f);
    path.CubicTo (68.6763107f, 56.0058575f, 65.9796704f, 57.5737917f, 64.5928855f, 59.965729f);
    path.LineTo (43.0238921f, 97.5342563f);
    path.CubicTo (41.6587026f, 99.9325978f, 41.6587026f, 103.067402f, 43.0238921f, 105.465744f);
    path.LineTo (64.5928855f, 143.034271f);
    path.CubicTo (65.9798162f, 145.426228f, 68.6763107f, 146.994582f, 71.4311121f, 147f);
    path.LineTo (114.568946f, 147f);
    path.CubicTo (117.323748f, 146.994143f, 120.020241f, 145.426228f, 121.407172f, 143.034271f);
    path.LineTo (142.976161f, 105.465744f);
    path.CubicTo (144.34135f, 103.067402f, 144.341209f, 99.9325978f, 142.976161f, 97.5342563f);
    path.LineTo (121.407172f, 59.965729f);
    path.CubicTo (120.020241f, 57.5737917f, 117.323748f, 56.0054182f, 114.568946f, 56f);
    path.LineTo (71.4311121f, 56f);
    path.Close ();

    // draw the Xamagon path
    canvas.DrawPath (path, paint);
  }
}
```

### <a name="drawing-text"></a>テキストの描画

```csharp
// clear the canvas / fill with white
canvas.DrawColor (SKColors.White);

// set up drawing tools
using (var paint = new SKPaint ()) {
  paint.TextSize = 64.0f;
  paint.IsAntialias = true;
  paint.Color = new SKColor (0x42, 0x81, 0xA4);
  paint.IsStroke = false;

  // draw the text
  canvas.DrawText ("Skia", 0.0f, 64.0f, paint);
}
```

### <a name="drawing-bitmaps"></a>ビットマップを描画

```csharp
Stream fileStream = File.OpenRead ("MyImage.png");

// clear the canvas / fill with white
canvas.DrawColor (SKColors.White);

// decode the bitmap from the stream
using (var stream = new SKManagedStream(fileStream))
using (var bitmap = SKBitmap.Decode(stream))
using (var paint = new SKPaint()) {
  canvas.DrawBitmap(bitmap, SKRect.Create(Width, Height), paint);
}
```

### <a name="drawing-with-image-filters"></a>イメージ フィルターによる描画

```csharp
Stream fileStream = File.OpenRead ("MyImage.png"); // open a stream to an image file

// clear the canvas / fill with white
canvas.DrawColor (SKColors.White);

// decode the bitmap from the stream
using (var stream = new SKManagedStream(fileStream))
using (var bitmap = SKBitmap.Decode(stream))
using (var paint = new SKPaint()) {
  // create the image filter
  using (var filter = SKImageFilter.CreateBlur(5, 5)) {
    paint.ImageFilter = filter;

    // draw the bitmap through the filter
    canvas.DrawBitmap(bitmap, SKRect.Create(width, height), paint);
  }
}
```

## <a name="more-information"></a>詳細情報

SkiaSharp の使用に関する詳細についてで見つかんだことができます、 [API ドキュメント](https://docs.microsoft.com/dotnet/api/skiasharp)
