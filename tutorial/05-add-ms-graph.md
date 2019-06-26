<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="8fd76-101">この演習では、Microsoft Graph をアプリケーションに組み込みます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="8fd76-102">このアプリケーションでは、microsoft [Graph クライアントライブラリ](https://github.com/microsoftgraph/msgraph-sdk-dotnet)を使用して microsoft graph を呼び出すことにします。</span><span class="sxs-lookup"><span data-stu-id="8fd76-102">For this application, you will use the [Microsoft Graph Client Library for .NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="8fd76-103">Outlook から予定表のイベントを取得する</span><span class="sxs-lookup"><span data-stu-id="8fd76-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="8fd76-104">最初に、予定表ビュー用の新しいページを追加します。</span><span class="sxs-lookup"><span data-stu-id="8fd76-104">Start by adding a new page for the calendar view.</span></span> <span data-ttu-id="8fd76-105">ソリューションエクスプローラーで**グラフ-チュートリアル**プロジェクトを右クリックし、[**新しいアイテムの追加 >**] を選択します。[**空白のページ**] `CalendarPage.xaml`を選択し、[**名前**] フィールドに「」と入力して、[**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8fd76-105">Right-click the **graph-tutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `CalendarPage.xaml` in the **Name** field, and select **Add**.</span></span>

<span data-ttu-id="8fd76-106">を`CalendarPage.xaml`開き、次の行を既存`<Grid>`の要素の内側に追加します。</span><span class="sxs-lookup"><span data-stu-id="8fd76-106">Open `CalendarPage.xaml` and add the following line inside the existing `<Grid>` element.</span></span>

```xml
<TextBlock x:Name="Events" TextWrapping="Wrap"/>
```

<span data-ttu-id="8fd76-107">を`CalendarPage.xaml.cs`開き、次`using`のステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="8fd76-107">Open `CalendarPage.xaml.cs` and add the following `using` statements at the top of the file.</span></span>

```cs
using Microsoft.Toolkit.Services.MicrosoftGraph;
using Microsoft.Toolkit.Uwp.UI.Controls;
using Newtonsoft.Json;
```

<span data-ttu-id="8fd76-108">その後、次の関数を`CalendarPage`クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="8fd76-108">Then add the following functions to the `CalendarPage` class.</span></span>

```cs
private void ShowNotification(string message)
{
    // Get the main page that contains the InAppNotification
    var mainPage = (Window.Current.Content as Frame).Content as MainPage;

    // Get the notification control
    var notification = mainPage.FindName("Notification") as InAppNotification;

    notification.Show(message);
}

protected override async void OnNavigatedTo(NavigationEventArgs e)
{
    // Get the Graph client from the service
    var graphClient = MicrosoftGraphService.Instance.GraphProvider;

    try
    {
        // Get the events
        var events = await graphClient.Me.Events.Request()
            .Select("subject,organizer,start,end")
            .OrderBy("createdDateTime DESC")
            .GetAsync();

        // TEMPORARY: Show the results as JSON
        Events.Text = JsonConvert.SerializeObject(events.CurrentPage);
    }
    catch(Microsoft.Graph.ServiceException ex)
    {
        ShowNotification($"Exception getting events: {ex.Message}");
    }

    base.OnNavigatedTo(e);
}
```

<span data-ttu-id="8fd76-109">の`OnNavigatedTo`コードについて考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="8fd76-109">Consider with the code in `OnNavigatedTo` is doing.</span></span>

- <span data-ttu-id="8fd76-110">呼び出し先の URL は`/v1.0/me/events`になります。</span><span class="sxs-lookup"><span data-stu-id="8fd76-110">The URL that will be called is `/v1.0/me/events`.</span></span>
- <span data-ttu-id="8fd76-111">関数`Select`は、各イベントに対して返されるフィールドを、ビューが実際に使用するものだけに制限します。</span><span class="sxs-lookup"><span data-stu-id="8fd76-111">The `Select` function limits the fields returned for each events to just those the view will actually use.</span></span>
- <span data-ttu-id="8fd76-112">関数`OrderBy`は、生成された日付と時刻で結果を並べ替えます。最新のアイテムが最初に表示されます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-112">The `OrderBy` function sorts the results by the date and time they were created, with the most recent item being first.</span></span>

<span data-ttu-id="8fd76-113">この予定表ページに移動できるようにするために、アプリを実行する直前に、 `NavView_ItemInvoked` `MainPage.xaml.cs`ファイルのメソッドを次のよう`throw new NotImplementedException();`に変更して行を置換します。</span><span class="sxs-lookup"><span data-stu-id="8fd76-113">Just before running the app, in order to be able to navigate to this calendar page, modify the `NavView_ItemInvoked` method in the `MainPage.xaml.cs` file to replace the `throw new NotImplementedException();` line with as follows.</span></span>

```cs
case "calendar":
    RootFrame.Navigate(typeof(CalendarPage));
    break;
```

<span data-ttu-id="8fd76-114">これで、アプリを実行し、サインインして、左側のメニューの [**予定表**] ナビゲーション項目をクリックできるようになります。</span><span class="sxs-lookup"><span data-stu-id="8fd76-114">You can now run the app, sign in, and click the **Calendar** navigation item in the left-hand menu.</span></span> <span data-ttu-id="8fd76-115">ユーザーの予定表にあるイベントの JSON ダンプが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-115">You should see a JSON dump of the events on the user's calendar.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="8fd76-116">結果を表示する</span><span class="sxs-lookup"><span data-stu-id="8fd76-116">Display the results</span></span>

<span data-ttu-id="8fd76-117">これで、JSON ダンプを、ユーザーにわかりやすい方法で結果を表示するためのものに置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-117">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="8fd76-118">の`CalendarPage.xaml`内容全体を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-118">Replace the entire contents of `CalendarPage.xaml` with the following.</span></span>

```xml
<Page
    x:Class="graph_tutorial.CalendarPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:graph_tutorial"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <Grid>
        <controls:DataGrid x:Name="EventList" Grid.Row="1"
                AutoGenerateColumns="False">
            <controls:DataGrid.Columns>
                <controls:DataGridTextColumn
                        Header="Organizer"
                        Width="SizeToCells"
                        Binding="{Binding Organizer.EmailAddress.Name}"
                        FontSize="20" />
                <controls:DataGridTextColumn
                        Header="Subject"
                        Width="SizeToCells"
                        Binding="{Binding Subject}"
                        FontSize="20" />
                <controls:DataGridTextColumn
                        Header="Start"
                        Width="SizeToCells"
                        Binding="{Binding Start.DateTime}"
                        FontSize="20" />
                <controls:DataGridTextColumn
                        Header="End"
                        Width="SizeToCells"
                        Binding="{Binding End.DateTime}"
                        FontSize="20" />
            </controls:DataGrid.Columns>
        </controls:DataGrid>
    </Grid>
</Page>
```

<span data-ttu-id="8fd76-119">これは、 `TextBlock`をに`DataGrid`置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-119">This replaces the `TextBlock` with a `DataGrid`.</span></span> <span data-ttu-id="8fd76-120">を開き`CalendarPage.xaml.cs` 、行を`Events.Text = JsonConvert.SerializeObject(events.CurrentPage);`次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-120">Now open `CalendarPage.xaml.cs` and replace the `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` line with the following.</span></span>

```cs
EventList.ItemsSource = events.CurrentPage.ToList();
```

<span data-ttu-id="8fd76-121">今すぐアプリを実行して予定表を選択すると、イベントの一覧がデータグリッドに表示されます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-121">If you run the app now and select the calendar, you should get a list of events in a data grid.</span></span> <span data-ttu-id="8fd76-122">ただし、**開始**値と**終了**値は、非ユーザーフレンドリな方法で表示されます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-122">However, the **Start** and **End** values are displayed in a non-user-friendly manner.</span></span> <span data-ttu-id="8fd76-123">[値コンバーター](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter)を使用して、これらの値の表示方法を制御できます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-123">You can control how those values are displayed by using a [value converter](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).</span></span>

<span data-ttu-id="8fd76-124">ソリューションエクスプローラーで**グラフのチュートリアル**プロジェクトを右クリックし、[ **> クラスの追加**] を選択します。クラス`GraphDateTimeTimeZoneConverter.cs`の名前を指定して、[**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8fd76-124">Right-click the **graph-tutorial** project in Solution Explorer and select **Add > Class...**. Name the class `GraphDateTimeTimeZoneConverter.cs` and select **Add**.</span></span> <span data-ttu-id="8fd76-125">ファイルの内容全体を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-125">Replace the entire contents of the file with the following.</span></span>

```cs
using Microsoft.Graph;
using System;

namespace graph_tutorial
{
    class GraphDateTimeTimeZoneConverter : Windows.UI.Xaml.Data.IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, string language)
        {
            DateTimeTimeZone date = value as DateTimeTimeZone;

            if (date != null)
            {
                // Resolve the time zone
                var timezone = TimeZoneInfo.FindSystemTimeZoneById(date.TimeZone);
                // Parse method assumes local time, which may not be the case
                var parsedDateAsLocal = DateTimeOffset.Parse(date.DateTime);
                // Determine the offset from UTC time for the specific date
                // Making this call adjusts for DST as appropriate
                var tzOffset = timezone.GetUtcOffset(parsedDateAsLocal.DateTime);
                // Create a new DateTimeOffset with the specific offset from UTC
                var correctedDate = new DateTimeOffset(parsedDateAsLocal.DateTime, tzOffset);
                // Return the local date time string
                return correctedDate.LocalDateTime.ToString();
            }

            return string.Empty;
        }

        public object ConvertBack(object value, Type targetType, object parameter, string language)
        {
            throw new NotImplementedException();
        }
    }
}
```

<span data-ttu-id="8fd76-126">このコードでは、Microsoft Graph によって返された[dateTimeTimeZone](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/datetimetimezone)構造`DateTimeOffset`体を取得し、それをオブジェクトに解析します。</span><span class="sxs-lookup"><span data-stu-id="8fd76-126">This code takes the [dateTimeTimeZone](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/datetimetimezone) structure returned by Microsoft Graph and parses it into a `DateTimeOffset` object.</span></span> <span data-ttu-id="8fd76-127">その後、値をユーザーのタイムゾーンに変換し、書式設定された値を返します。</span><span class="sxs-lookup"><span data-stu-id="8fd76-127">It then converts the value into the user's time zone and returns the formatted value.</span></span>

<span data-ttu-id="8fd76-128">を`CalendarPage.xaml`開き、要素の`<Grid>` **前に**以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="8fd76-128">Open `CalendarPage.xaml` and add the following **before** the `<Grid>` element.</span></span>

```xml
<Page.Resources>
    <local:GraphDateTimeTimeZoneConverter x:Key="DateTimeTimeZoneValueConverter" />
</Page.Resources>
```

<span data-ttu-id="8fd76-129">次に、その`Binding="{Binding Start.DateTime}"`行を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-129">Then, replace the `Binding="{Binding Start.DateTime}"` line with the following.</span></span>

```xml
Binding="{Binding Start, Converter={StaticResource DateTimeTimeZoneValueConverter}}"
```

<span data-ttu-id="8fd76-130">行を`Binding="{Binding End.DateTime}"`次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-130">Replace the `Binding="{Binding End.DateTime}"` line with the following.</span></span>

```xml
Binding="{Binding End, Converter={StaticResource DateTimeTimeZoneValueConverter}}"
```

<span data-ttu-id="8fd76-131">アプリを実行し、サインインして、**予定表**のナビゲーションアイテムをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8fd76-131">Run the app, sign in, and click the **Calendar** navigation item.</span></span> <span data-ttu-id="8fd76-132">**開始**および**終了**の値が書式設定されたイベントの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8fd76-132">You should see the list of events with the **Start** and **End** values formatted.</span></span>

![イベントの表のスクリーンショット](./images/add-msgraph-01.png)
