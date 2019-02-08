---
title: Xamarin.Forms のラベル
description: この記事では、Xamarin.Forms ラベル クラスを使用して、アプリケーションで単一と複数行のテキストを表示する方法について説明します。
ms.prod: xamarin
ms.assetid: 02E6C553-5670-49A0-8EE9-5153ED21EA91
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 12/13/2018
ms.openlocfilehash: ce1ba235a309e2388bd5eea7d70a1d72852fc615
ms.sourcegitcommit: 93c9fe61eb2cdfa530960b4253eb85161894c882
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2019
ms.locfileid: "55831860"
---
# <a name="xamarinforms-label"></a>Xamarin.Forms のラベル

[![サンプルのダウンロード](~/media/shared/download.png)サンプルをダウンロードします。](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Text)

_Xamarin.Forms にテキストを表示_

[ `Label` ](xref:Xamarin.Forms.Label)単一および複数行のテキストを表示するビューを使用します。 ラベルは、装飾、色付きのテキストがあるし、カスタム フォント (ファミリ、サイズ、およびオプション) を使用することができます。

## <a name="text-decorations"></a>文字装飾

下線、取り消し線テキスト装飾に適用できる[ `Label` ](xref:Xamarin.Forms.Label)インスタンスを設定して、`Label.TextDecorations`プロパティを 1 つまたは複数`TextDecorations`列挙型メンバー。

- `None`
- `Underline`
- `Strikethrough`

次の XAML の例は、設定を示して、`Label.TextDecorations`プロパティ。

```xaml
<Label Text="This is underlined text." TextDecorations="Underline"  />
<Label Text="This is text with strikethrough." TextDecorations="Strikethrough" />
<Label Text="This is underlined text with strikethrough." TextDecorations="Underline, Strikethrough" />
```

同等の c# コードに示します。

```csharp
var underlineLabel = new Label { Text = "This is underlined text.", TextDecorations = TextDecorations.Underline };
var strikethroughLabel = new Label { Text = "This is text with strikethrough.", TextDecorations = TextDecorations.Strikethrough };
var bothLabel = new Label { Text = "This is underlined text with strikethrough.", TextDecorations = TextDecorations.Underline | TextDecorations.Strikethrough };
```

次のスクリーン ショットに示す、`TextDecorations`列挙型のメンバーに適用される[ `Label` ](xref:Xamarin.Forms.Label)インスタンス。

![](label-images/label-textdecorations.png "文字装飾を使用してラベル")

> [!NOTE]
> 文字装飾にも適用[ `Span` ](xref:Xamarin.Forms.Span)インスタンス。 詳細については、`Span`クラスを参照してください[書式設定されたテキスト](#Formatted_Text)します。

## <a name="colors"></a>色

使用して、バインド可能なカスタムのテキストの色を使用するラベルを設定できます[ `TextColor` ](xref:Xamarin.Forms.Label.TextColor)プロパティ。

特別な注意は、色は各プラットフォームで使用できることを確認する必要があります。 各プラットフォームには、テキストと背景の色の既定値があるためには、それぞれで動作する、既定値を選択するように注意する必要があります。

次の XAML の例のテキストの色の設定、 `Label`:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="TextSample.LabelPage"
             Title="Label Demo">
    <StackLayout Padding="5,10">
      <Label TextColor="#77d065" FontSize = "20" Text="This is a green label." />
    </StackLayout>
</ContentPage>
```

同等の c# コードに示します。

```csharp
public partial class LabelPage : ContentPage
{
    public LabelPage ()
    {
        InitializeComponent ();

        var layout = new StackLayout { Padding = new Thickness(5,10) };
        var label = new Label { Text="This is a green label.", TextColor = Color.FromHex("#77d065"), FontSize = 20 };
        layout.Children.Add(label);
        this.Content = layout;
    }
}
```

次のスクリーン ショットの設定の結果を表示する、`TextColor`プロパティ。

![](label-images/textcolor.png "ラベル TextColor 例")

色の詳細については、次を参照してください。[色](~/xamarin-forms/user-interface/colors.md)します。

## <a name="fonts"></a>フォント

フォントを指定することの詳細については、`Label`を参照してください[フォント](~/xamarin-forms/user-interface/text/fonts.md)します。

<a name="Truncation_and_Wrapping" />

## <a name="truncation-and-wrapping"></a>切り捨てと折り返し

によって公開されているいくつかの方法のいずれかで 1 つの行に収まらないテキストを処理するためにラベルを設定することができます、`LineBreakMode`プロパティ。 [`LineBreakMode`](xref:Xamarin.Forms.LineBreakMode) 次の値を持つ列挙型を示します。

- **HeadTruncation** &ndash;末尾を示す、テキストの先頭を切り捨てます。
- **CharacterWrap** &ndash;文字境界でテキストを新しい行をラップします。
- **MiddleTruncation** &ndash;先頭と末尾の省略記号によって中間置換後の文字列で、テキストが表示されます。
- **NoWrap** &ndash;のみを表示するテキストを折り返しませんしたりできるだけ多くのテキストに合わせて 1 つの行にします。
- **TailTruncation** &ndash;末尾を切り捨てる、テキストの先頭を示します。
- **WordWrap** &ndash;ワード境界でテキストをラップします。

## <a name="displaying-a-specific-number-of-lines"></a>特定の行数を表示します。

によって表示される行の数、 [ `Label` ](xref:Xamarin.Forms.Label)を設定して指定することができます、`Label.MaxLines`プロパティを`int`値。

- ときに`MaxLines`0 の場合は、`Label`の値を尊重、 [ `LineBreakMode` ](xref:Xamarin.Forms.Label.LineBreakMode)プロパティを切り捨てられる可能性がある場合、1 つの行を表示するか、またはすべてのテキストを含むすべての行。
- ときに`MaxLines`1 に設定されて、結果の設定と同じですが、 [ `LineBreakMode` ](xref:Xamarin.Forms.Label.LineBreakMode)プロパティを[ `NoWrap` ](xref:Xamarin.Forms.LineBreakMode)、 [ `HeadTruncation` ](xref:Xamarin.Forms.LineBreakMode)、 [`MiddleTruncation` ](xref:Xamarin.Forms.LineBreakMode)、または[ `TailTruncation`](xref:Xamarin.Forms.LineBreakMode)します。 ただし、`Label`の値を尊重、 [ `LineBreakMode` ](xref:Xamarin.Forms.Label.LineBreakMode)に関して該当する場合、省略記号の配置プロパティです。
- ときに`MaxLines`が 1 より大きい、`Label`の値を考慮しながら、行の指定した数が表示されます、 [ `LineBreakMode` ](xref:Xamarin.Forms.Label.LineBreakMode)に関して該当する場合、省略記号の配置プロパティです。 ただし、設定、`MaxLines`プロパティを 1 には効果があるない場合よりも大きい値に、 [ `LineBreakMode` ](xref:Xamarin.Forms.Label.LineBreakMode)プロパティに設定されて[ `NoWrap`](xref:Xamarin.Forms.LineBreakMode)します。

次の XAML の例は、設定を示して、`MaxLines`プロパティを[ `Label` ](xref:Xamarin.Forms.Label):

```xaml
<Label Text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. In facilisis nulla eu felis fringilla vulputate. Nullam porta eleifend lacinia. Donec at iaculis tellus."
       LineBreakMode="WordWrap"
       MaxLines="2" />
```

同等の c# コードに示します。

```csharp
var label =
{
  Text = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. In facilisis nulla eu felis fringilla vulputate. Nullam porta eleifend lacinia. Donec at iaculis tellus.", LineBreakMode = LineBreakMode.WordWrap,
  MaxLines = 2
};
```

次のスクリーン ショットの設定の結果を表示する、`MaxLines`プロパティをテキストは、2 つ以上の行を占有するのに十分なときに、2。

![](label-images/label-maxlines.png "ラベル MaxLines 例")

<a name="Formatted_Text" />

## <a name="formatted-text"></a>書式付きテキスト

ラベルの公開、 [ `FormattedText` ](xref:Xamarin.Forms.Label.FormattedText)プロパティを複数のフォントとテキストの表示を許可し、同じビューでの色します。

`FormattedText`プロパティの型は[ `FormattedString` ](xref:Xamarin.Forms.FormattedString)、1 つまたは複数で構成される[ `Span` ](xref:Xamarin.Forms.Span)設定を使用して、インスタンス、 [ `Spans` ](xref:Xamarin.Forms.FormattedString.Spans)プロパティ. 次`Span`を視覚的な外観を設定するプロパティを使用できます。

- [`BackgroundColor`](xref:Xamarin.Forms.Span.BackgroundColor) – span の背景の色。
- [`Font`](xref:Xamarin.Forms.Span.Font) -範囲内のテキストのフォント。
- [`FontAttributes`](xref:Xamarin.Forms.Span.FontAttributes) -範囲内のテキストのフォント属性。
- [`FontFamily`](xref:Xamarin.Forms.Span.FontFamily) -範囲内のテキストのフォントが所属するフォント ファミリ。
- [`FontSize`](xref:Xamarin.Forms.Span.FontSize) -範囲内のテキストのフォントのサイズ。
- [`ForegroundColor`](xref:Xamarin.Forms.Span.ForegroundColor) -範囲内のテキストの色。 このプロパティは廃止され、置き換えられましたが、`TextColor`プロパティ。
- [`LineHeight`](xref:Xamarin.Forms.Span.LineHeight) -範囲の既定の行の高さに適用する乗数。 詳細については、次を参照してください。[行の高さ](#line-height)します。
- [`Style`](xref:Xamarin.Forms.Span.Style) – スパンに適用するスタイル。
- [`Text`](xref:Xamarin.Forms.Span.Text) – スパンのテキスト。
- [`TextColor`](xref:Xamarin.Forms.Span.TextColor) -範囲内のテキストの色。
- `TextDecorations` -範囲内のテキストに適用する装飾。 詳細については、次を参照してください。[装飾](#text-decorations)します。

さらに、 [ `GestureRecognizers` ](xref:Xamarin.Forms.GestureElement.GestureRecognizers)のジェスチャに応答するジェスチャ レコグナイザーのコレクションを定義するプロパティを使用できます、 [ `Span`](xref:Xamarin.Forms.Span)します。

XAML の例を次に示します、`FormattedText`プロパティの 3 つで構成される[ `Span` ](xref:Xamarin.Forms.Span)インスタンス。

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="TextSample.LabelPage"
             Title="Label Demo - XAML">
    <StackLayout Padding="5,10">
        ...
        <Label LineBreakMode="WordWrap">
            <Label.FormattedText>
                <FormattedString>
                    <Span Text="Red Bold, " TextColor="Red" FontAttributes="Bold" />
                    <Span Text="default, " Style="{DynamicResource BodyStyle}">
                        <Span.GestureRecognizers>
                            <TapGestureRecognizer Command="{Binding TapCommand}" />
                        </Span.GestureRecognizers>
                    </Span>
                    <Span Text="italic small." FontAttributes="Italic" FontSize="Small" />
                </FormattedString>
            </Label.FormattedText>
        </Label>
    </StackLayout>
</ContentPage>
```

同等の c# コードに示します。

```csharp
public class LabelPageCode : ContentPage
{
    public LabelPageCode ()
    {
        var layout = new StackLayout{ Padding = new Thickness (5, 10) };
        ...
        var formattedString = new FormattedString ();
        formattedString.Spans.Add (new Span{ Text = "Red bold, ", ForegroundColor = Color.Red, FontAttributes = FontAttributes.Bold });

        var span = new Span { Text = "default, " };
        span.GestureRecognizers.Add(new TapGestureRecognizer { Command = new Command(async () => await DisplayAlert("Tapped", "This is a tapped Span.", "OK")) });
        formattedString.Spans.Add(span);
        formattedString.Spans.Add (new Span { Text = "italic small.", FontAttributes = FontAttributes.Italic, FontSize =  Device.GetNamedSize(NamedSize.Small, typeof(Label)) });

        layout.Children.Add (new Label { FormattedText = formattedString });
        this.Content = layout;
    }
}
```

> [!IMPORTANT]
> [ `Text` ](xref:Xamarin.Forms.Span.Text)のプロパティを`Span`データ バインドを通じて設定できます。 詳細については、次を参照してください。[データ バインディングの](~/xamarin-forms/app-fundamentals/data-binding/index.md)します。

なお、 [ `Span` ](xref:Xamarin.Forms.Span) 、span に追加されるすべてのジェスチャに応答できますも[ `GestureRecognizers` ](xref:Xamarin.Forms.GestureElement.GestureRecognizers)コレクション。 たとえば、 [ `TapGestureRecognizer` ](xref:Xamarin.Forms.TapGestureRecognizer)が 2 番目に追加された`Span`上記のコード例でします。 そのため、この`Span`がタップされた、`TapGestureRecognizer`が実行することによって応答、`ICommand`によって定義された、 [ `Command` ](xref:Xamarin.Forms.TapGestureRecognizer.Command)プロパティ。 ジェスチャ レコグナイザーの詳細については、次を参照してください。 [Xamarin.Forms ジェスチャ](~/xamarin-forms/app-fundamentals/gestures/index.md)します。

次のスクリーン ショットの設定の結果を表示する、`FormattedString`プロパティを 3 つ`Span`インスタンス。

![](label-images/formattedtext.png "ラベルの FormattedText の例")

## <a name="line-height"></a>[行間]

縦の高さを[ `Label` ](xref:Xamarin.Forms.Label)と[ `Span` ](xref:Xamarin.Forms.Span)を設定してカスタマイズできる、 [ `Label.LineHeight` ](xref:Xamarin.Forms.Label.LineHeight)プロパティまたは[ `Span.LineHeight`](xref:Xamarin.Forms.Span.LineHeight)を`double`値。 IOS と Android でこれらの値には、元の行の高さとユニバーサル Windows プラットフォーム (UWP) の乗数、`Label.LineHeight`プロパティの値がラベルのフォント サイズの乗数。

> [!NOTE]
> - Ios では、 [ `Label.LineHeight` ](xref:Xamarin.Forms.Label.LineHeight)と[ `Span.LineHeight` ](xref:Xamarin.Forms.Span.LineHeight)プロパティが 1 つの行に一致するテキストと複数の行に折り返されるテキストの行の高さを変更します。
> - Android の場合、 [ `Label.LineHeight` ](xref:Xamarin.Forms.Label.LineHeight)と[ `Span.LineHeight` ](xref:Xamarin.Forms.Span.LineHeight)プロパティのみ複数の行に折り返されるテキストの行の高さを変更します。
> - UWP での[ `Label.LineHeight` ](xref:Xamarin.Forms.Label.LineHeight)プロパティが複数の行に折り返されるテキストの行の高さを変更し、 [ `Span.LineHeight` ](xref:Xamarin.Forms.Span.LineHeight)プロパティは影響を与えません。

次の XAML の例は、設定を示して、 [ `LineHeight` ](xref:Xamarin.Forms.Label.LineHeight)プロパティを[ `Label` ](xref:Xamarin.Forms.Label):

```xaml
<Label Text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. In facilisis nulla eu felis fringilla vulputate. Nullam porta eleifend lacinia. Donec at iaculis tellus."
       LineBreakMode="WordWrap"
       LineHeight="1.8" />
```

同等の c# コードに示します。

```csharp
var label =
{
  Text = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. In facilisis nulla eu felis fringilla vulputate. Nullam porta eleifend lacinia. Donec at iaculis tellus.", LineBreakMode = LineBreakMode.WordWrap,
  LineHeight = 1.8
};
```

次のスクリーン ショットの設定の結果を表示する、 [ `Label.LineHeight` ](xref:Xamarin.Forms.Label.LineHeight) 1.8 へのプロパティ。

![](label-images/label-lineheight.png "ラベル LineHeight の例")

次の XAML の例は、設定を示して、 [ `LineHeight` ](xref:Xamarin.Forms.Span.LineHeight)プロパティを[ `Span` ](xref:Xamarin.Forms.Span):

```xaml
<Label LineBreakMode="WordWrap">
    <Label.FormattedText>
        <FormattedString>
            <Span Text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. In a tincidunt sem. Phasellus mollis sit amet turpis in rutrum. Sed aliquam ac urna id scelerisque. "
                  LineHeight="1.8"/>
            <Span Text="Nullam feugiat sodales elit, et maximus nibh vulputate id."
                  LineHeight="1.8" />
        </FormattedString>
    </Label.FormattedText>
</Label>
```

同等の c# コードに示します。

```csharp
var formattedString = new FormattedString();
formattedString.Spans.Add(new Span
{
  Text = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. In a tincidunt sem. Phasellus mollis sit amet turpis in rutrum. Sed aliquam ac urna id scelerisque. ",
  LineHeight = 1.8
});
formattedString.Spans.Add(new Span
{
  Text = "Nullam feugiat sodales elit, et maximus nibh vulputate id.",
  LineHeight = 1.8
});
var label = new Label
{
  FormattedText = formattedString,
  LineBreakMode = LineBreakMode.WordWrap
};
```

次のスクリーン ショットの設定の結果を表示する、 [ `Span.LineHeight` ](xref:Xamarin.Forms.Span.LineHeight) 1.8 へのプロパティ。

![](label-images/span-lineheight.png "LineHeight の span の例")

## <a name="hyperlinks"></a>ハイパーリンク

によって表示されるテキスト[ `Label` ](xref:Xamarin.Forms.Label)と[ `Span` ](xref:Xamarin.Forms.Span)インスタンスは、次の方法でハイパーリンクに変換できます。

1. 設定、`TextColor`と`TextDecoration`のプロパティ、 [ `Label` ](xref:Xamarin.Forms.Label)または[ `Span`](xref:Xamarin.Forms.Span)します。
1. 追加、 [ `TapGestureRecognizer` ](xref:Xamarin.Forms.TapGestureRecognizer)を[ `GestureRecognizers` ](xref:Xamarin.Forms.GestureElement.GestureRecognizers)のコレクション、 [ `Label` ](xref:Xamarin.Forms.Label)または[ `Span`](xref:Xamarin.Forms.Span)が[ `Command` ](xref:Xamarin.Forms.TapGestureRecognizer.Command)プロパティにバインドされて、 `ICommand`、およびその[ `CommandParameter` ](xref:Xamarin.Forms.TapGestureRecognizer.CommandParameter)プロパティには、開くための URL が含まれています。
1. 定義、`ICommand`によって実行される、 [ `TapGestureRecognizer`](xref:Xamarin.Forms.TapGestureRecognizer)します。
1. によって実行されるコードを記述、`ICommand`します。

取得した次のコード例、[ハイパーリンク デモ](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/HyperlinkDemos)サンプルを示しています、 [ `Label` ](xref:Xamarin.Forms.Label)コンテンツが複数設定[ `Span` ](xref:Xamarin.Forms.Span)インスタンス。

```xaml
<Label>
    <Label.FormattedText>
        <FormattedString>
            <Span Text="Alternatively, click " />
            <Span Text="here"
                  TextColor="Blue"
                  TextDecorations="Underline">
                <Span.GestureRecognizers>
                    <TapGestureRecognizer Command="{Binding TapCommand}"
                                          CommandParameter="https://docs.microsoft.com/xamarin/" />
                </Span.GestureRecognizers>
            </Span>
            <Span Text=" to view Xamarin documentation." />
        </FormattedString>
    </Label.FormattedText>
</Label>
```

この例では、最初と 3 番目の[ `Span` ](xref:Xamarin.Forms.Span) 、2 番目のテキストを構成するインスタンス`Span`tappable ハイパーリンクを表します。 これがそのテキストの色を青に設定し、下線文字の装飾が。 次のスクリーン ショットに示すように、ハイパーリンクの外観が作成されます。

[![ハイパーリンク](label-images/hyperlinks-small.png "ハイパーリンク")](label-images/hyperlinks-large.png#lightbox)

ハイパーリンクをタップすると、ときに、 [ `TapGestureRecognizer` ](xref:Xamarin.Forms.TapGestureRecognizer)が応答を実行して、`ICommand`によって定義されたその[ `Command` ](xref:Xamarin.Forms.TapGestureRecognizer.Command)プロパティ。 URL がさらに、指定された、 [ `CommandParameter` ](xref:Xamarin.Forms.TapGestureRecognizer.CommandParameter)プロパティに渡される、`ICommand`をパラメーターとして。

XAML ページの分離コードが含まれています、`TapCommand`実装。

```csharp
public partial class MainPage : ContentPage
{
    public ICommand TapCommand => new Command<string>(OpenBrowser);

    public MainPage()
    {
        InitializeComponent();
        BindingContext = this;
    }

    void OpenBrowser(string url)
    {
        Device.OpenUri(new Uri(url));
    }
}
```

`TapCommand`実行、`OpenBrowser`渡して、メソッド、 [ `TapGestureRecognizer.CommandParameter` ](xref:Xamarin.Forms.TapGestureRecognizer.CommandParameter)プロパティの値をパラメーターとして。 さらに、このメソッドを呼び出す、 [ `Device.OpenUri` ](xref:Xamarin.Forms.Device.OpenUri*)メソッドを web ブラウザーで URL を開きます。 そのため、全体的な影響されるときに、ページのハイパーリンクがタップされた、web ブラウザーが表示され、ハイパーリンクに関連付けられている URL にナビゲートするとします。

### <a name="creating-a-reusable-hyperlink-class"></a>ハイパーリンクの再利用可能なクラスを作成します。

ハイパーリンクを作成するのには、前のアプローチでは、アプリケーションのハイパーリンクを必要とするたびに繰り返し発生するコードの記述が必要です。 ただし、両方、 [ `Label` ](xref:Xamarin.Forms.Label)と[ `Span` ](xref:Xamarin.Forms.Span)クラスをサブクラスを作成することができる`HyperlinkLabel`と`HyperlinkSpan`クラス、ジェスチャ レコグナイザーとテキストの書式設定コードが追加されました。

取得した次のコード例、[ハイパーリンク デモ](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/HyperlinkDemos)サンプルを示しています、`HyperlinkSpan`クラス。

```csharp
public class HyperlinkSpan : Span
{
    public static readonly BindableProperty UrlProperty =
        BindableProperty.Create(nameof(Url), typeof(string), typeof(HyperlinkSpan), null);

    public string Url
    {
        get { return (string)GetValue(UrlProperty); }
        set { SetValue(UrlProperty, value); }
    }

    public HyperlinkSpan()
    {
        TextDecorations = TextDecorations.Underline;
        TextColor = Color.Blue;
        GestureRecognizers.Add(new TapGestureRecognizer
        {
            Command = new Command(() => Device.OpenUri(new Uri(Url)))
        });
    }
}
```

`HyperlinkSpan`クラスを定義、`Url`プロパティと関連付けられた[ `BindableProperty` ](xref:Xamarin.Forms.BindableProperty)、コンス トラクターは、ハイパーリンクの外観を設定して、 [ `TapGestureRecognizer` ](xref:Xamarin.Forms.TapGestureRecognizer)が応答します。ときにハイパーリンクをタップします。 ときに、`HyperlinkSpan`がタップされた、`TapGestureRecognizer`が応答を実行して、 [ `Device.OpenUri` ](xref:Xamarin.Forms.Device.OpenUri*)メソッドを呼び出して、によって指定された URL を開き、 `Url` web ブラウザーでのプロパティ。

`HyperlinkSpan`クラスのインスタンスを XAML に追加することでクラスを使用できます。

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:HyperlinkDemo"
             x:Class="HyperlinkDemo.MainPage">
    <StackLayout>
        ...
        <Label>
            <Label.FormattedText>
                <FormattedString>
                    <Span Text="Alternatively, click " />
                    <local:HyperlinkSpan Text="here"
                                         Url="https://docs.microsoft.com/appcenter/" />
                    <Span Text=" to view AppCenter documentation." />
                </FormattedString>
            </Label.FormattedText>
        </Label>
    </StackLayout>
</ContentPage>
```

## <a name="styling-labels"></a>スタイル ラベル

前のセクションでは、対象設定[ `Label` ](xref:Xamarin.Forms.Label)と[ `Span` ](xref:Xamarin.Forms.Span) -インスタンスごとのプロパティ。 ただし、プロパティのセットは、1 つまたは複数のビューに一貫して適用されるスタイルを 1 つにグループ化できます。 コードの読みやすさを向上でき設計の変更を簡単に実装できます。 詳細については、次を参照してください。[スタイル](~/xamarin-forms/user-interface/text/styles.md)します。

## <a name="related-links"></a>関連リンク

- [テキスト (サンプル)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Text)
- [ハイパーリンク (サンプル)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Hyperlinks)
- [第 3 章、Xamarin.Forms でモバイル アプリの作成](https://developer.xamarin.com/r/xamarin-forms/book/chapter03.pdf)
- [ラベルの API](xref:Xamarin.Forms.Label)
- [API のスパン](xref:Xamarin.Forms.Span)
