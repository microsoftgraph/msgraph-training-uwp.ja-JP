<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="4e4e8-101">この演習では、Microsoft Graph をアプリケーションに組み込みます。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="4e4e8-102">このアプリケーションでは、microsoft [Graph クライアントライブラリ](https://github.com/microsoftgraph/msgraph-sdk-dotnet)を使用して microsoft graph を呼び出すことにします。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-102">For this application, you will use the [Microsoft Graph Client Library for .NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="4e4e8-103">Outlook からカレンダー イベントを取得する</span><span class="sxs-lookup"><span data-stu-id="4e4e8-103">Get calendar events from Outlook</span></span>

1. <span data-ttu-id="4e4e8-104">予定表ビューの新しいページを追加します。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-104">Add a new page for the calendar view.</span></span> <span data-ttu-id="4e4e8-105">ソリューションエクスプローラーで**Graphtutorial**プロジェクトを右クリックし、[ **Add > New Item...**.] を選択します。[**空白のページ**] `CalendarPage.xaml`を選択し、[**名前**] フィールドに「」と入力して、[**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-105">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `CalendarPage.xaml` in the **Name** field, and select **Add**.</span></span>

1. <span data-ttu-id="4e4e8-106">を`CalendarPage.xaml`開き、次の行を既存`<Grid>`の要素の内側に追加します。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-106">Open `CalendarPage.xaml` and add the following line inside the existing `<Grid>` element.</span></span>

    ```xaml
    <TextBlock x:Name="Events" TextWrapping="Wrap"/>
    ```

1. <span data-ttu-id="4e4e8-107">を`CalendarPage.xaml.cs`開き、次`using`のステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-107">Open `CalendarPage.xaml.cs` and add the following `using` statements at the top of the file.</span></span>

    ```csharp
    using Microsoft.Toolkit.Graph.Providers;
    using Microsoft.Toolkit.Uwp.UI.Controls;
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="4e4e8-108">次の関数を`CalendarPage`クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-108">Add the following functions to the `CalendarPage` class.</span></span>

    ```csharp
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
        // Get the Graph client from the provider
        var graphClient = ProviderManager.Instance.GlobalProvider.Graph;

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

    <span data-ttu-id="4e4e8-109">の`OnNavigatedTo`コードについて考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-109">Consider with the code in `OnNavigatedTo` is doing.</span></span>

    - <span data-ttu-id="4e4e8-110">呼び出される URL は `/v1.0/me/events` です。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-110">The URL that will be called is `/v1.0/me/events`.</span></span>
    - <span data-ttu-id="4e4e8-111">`Select` 関数は、各イベントに返されるフィールドを、ビューで実際に使用されるフィールドだけに制限します。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-111">The `Select` function limits the fields returned for each events to just those the view will actually use.</span></span>
    - <span data-ttu-id="4e4e8-112">`OrderBy` 関数は、作成された日時で結果を並べ替えます。最新のアイテムが最初に表示されます。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-112">The `OrderBy` function sorts the results by the date and time they were created, with the most recent item being first.</span></span>

1. <span data-ttu-id="4e4e8-113">ファイル内`NavView_ItemInvoked`のメソッドを変更して、既存`switch`のステートメントを次のように置き換えます。 `MainPage.xaml.cs`</span><span class="sxs-lookup"><span data-stu-id="4e4e8-113">Modify the `NavView_ItemInvoked` method in the `MainPage.xaml.cs` file to replace the existing `switch` statement with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="SwitchStatementSnippet" highlight="4":::

<span data-ttu-id="4e4e8-114">これで、アプリを実行し、サインインして、左側のメニューの [**予定表**] ナビゲーション項目をクリックできるようになります。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-114">You can now run the app, sign in, and click the **Calendar** navigation item in the left-hand menu.</span></span> <span data-ttu-id="4e4e8-115">ユーザーの予定表にあるイベントの JSON ダンプが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-115">You should see a JSON dump of the events on the user's calendar.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="4e4e8-116">結果の表示</span><span class="sxs-lookup"><span data-stu-id="4e4e8-116">Display the results</span></span>

1. <span data-ttu-id="4e4e8-117">の`CalendarPage.xaml`内容全体を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-117">Replace the entire contents of `CalendarPage.xaml` with the following.</span></span>

    ```xaml
    <Page
        x:Class="GraphTutorial.CalendarPage"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:GraphTutorial"
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

1. <span data-ttu-id="4e4e8-118">を`CalendarPage.xaml.cs`開いて、 `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);`次の行に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-118">Open `CalendarPage.xaml.cs` and replace the `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` line with the following.</span></span>

    ```csharp
    EventList.ItemsSource = events.CurrentPage.ToList();
    ```

    <span data-ttu-id="4e4e8-119">今すぐアプリを実行して予定表を選択すると、イベントの一覧がデータグリッドに表示されます。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-119">If you run the app now and select the calendar, you should get a list of events in a data grid.</span></span> <span data-ttu-id="4e4e8-120">ただし、**開始**値と**終了**値は、非ユーザーフレンドリな方法で表示されます。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-120">However, the **Start** and **End** values are displayed in a non-user-friendly manner.</span></span> <span data-ttu-id="4e4e8-121">[値コンバーター](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter)を使用して、これらの値の表示方法を制御できます。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-121">You can control how those values are displayed by using a [value converter](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).</span></span>

1. <span data-ttu-id="4e4e8-122">ソリューションエクスプローラーで**Graphtutorial**プロジェクトを右クリックし、[ **> クラスの追加**] を選択します。クラス`GraphDateTimeTimeZoneConverter.cs`の名前を指定して、[**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-122">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > Class...**. Name the class `GraphDateTimeTimeZoneConverter.cs` and select **Add**.</span></span> <span data-ttu-id="4e4e8-123">ファイルの内容全体を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-123">Replace the entire contents of the file with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/GraphDateTimeTimeZoneConverter.cs" id="ConverterSnippet":::

    <span data-ttu-id="4e4e8-124">このコードでは、Microsoft Graph によって返された[dateTimeTimeZone](/graph/api/resources/datetimetimezone?view=graph-rest-1.0)構造`DateTimeOffset`体を取得し、それをオブジェクトに解析します。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-124">This code takes the [dateTimeTimeZone](/graph/api/resources/datetimetimezone?view=graph-rest-1.0) structure returned by Microsoft Graph and parses it into a `DateTimeOffset` object.</span></span> <span data-ttu-id="4e4e8-125">その後、値をユーザーのタイムゾーンに変換し、書式設定された値を返します。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-125">It then converts the value into the user's time zone and returns the formatted value.</span></span>

1. <span data-ttu-id="4e4e8-126">を`CalendarPage.xaml`開き、要素の`<Grid>` **前に**以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-126">Open `CalendarPage.xaml` and add the following **before** the `<Grid>` element.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="ResourcesSnippet":::

1. <span data-ttu-id="4e4e8-127">最後の2つ`DataGridTextColumn`の要素を次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-127">Replace the last two `DataGridTextColumn` elements with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="BindingSnippet" highlight="4,9":::

1. <span data-ttu-id="4e4e8-128">アプリを実行し、サインインして、**予定表**のナビゲーションアイテムをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-128">Run the app, sign in, and click the **Calendar** navigation item.</span></span> <span data-ttu-id="4e4e8-129">**開始**および**終了**の値が書式設定されたイベントの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="4e4e8-129">You should see the list of events with the **Start** and **End** values formatted.</span></span>

    ![イベント表のスクリーンショット](./images/add-msgraph-01.png)
