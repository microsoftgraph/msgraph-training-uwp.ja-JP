<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="797f4-101">この演習では、Microsoft Graph をアプリケーションに組み込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="797f4-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="797f4-102">このアプリケーションでは [、.NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) 用 Microsoft Graph クライアント ライブラリを使用して Microsoft Graph を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="797f4-102">For this application, you will use the [Microsoft Graph Client Library for .NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="797f4-103">Outlook からカレンダー イベントを取得する</span><span class="sxs-lookup"><span data-stu-id="797f4-103">Get calendar events from Outlook</span></span>

1. <span data-ttu-id="797f4-104">予定表ビューの新しいページを追加します。</span><span class="sxs-lookup"><span data-stu-id="797f4-104">Add a new page for the calendar view.</span></span> <span data-ttu-id="797f4-105">ソリューション エクスプローラーで **GraphTu solutionl** プロジェクトを右クリックし、[新しいアイテムの> **を選択します**。Choose **Blank Page,** enter `CalendarPage.xaml` in the **Name** field, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="797f4-105">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `CalendarPage.xaml` in the **Name** field, and select **Add**.</span></span>

1. <span data-ttu-id="797f4-106">既存 `CalendarPage.xaml` の要素内で次の行を開いて追加 `<Grid>` します。</span><span class="sxs-lookup"><span data-stu-id="797f4-106">Open `CalendarPage.xaml` and add the following line inside the existing `<Grid>` element.</span></span>

    ```xaml
    <TextBlock x:Name="Events" TextWrapping="Wrap"/>
    ```

1. <span data-ttu-id="797f4-107">ファイル `CalendarPage.xaml.cs` の上部に `using` 次のステートメントを開いて追加します。</span><span class="sxs-lookup"><span data-stu-id="797f4-107">Open `CalendarPage.xaml.cs` and add the following `using` statements at the top of the file.</span></span>

    ```csharp
    using Microsoft.Graph;
    using Microsoft.Toolkit.Graph.Providers;
    using Microsoft.Toolkit.Uwp.UI.Controls;
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="797f4-108">次の関数をクラスに追加 `CalendarPage` します。</span><span class="sxs-lookup"><span data-stu-id="797f4-108">Add the following functions to the `CalendarPage` class.</span></span>

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
            // Get the user's mailbox settings to determine
            // their time zone
            var user = await graphClient.Me.Request()
                .Select(u => new { u.MailboxSettings })
                .GetAsync();

            var startOfWeek = GetUtcStartOfWeekInTimeZone(DateTime.Today, user.MailboxSettings.TimeZone);
            var endOfWeek = startOfWeek.AddDays(7);

            var queryOptions = new List<QueryOption>
            {
                new QueryOption("startDateTime", startOfWeek.ToString("o")),
                new QueryOption("endDateTime", endOfWeek.ToString("o"))
            };

            // Get the events
            var events = await graphClient.Me.CalendarView.Request(queryOptions)
                .Header("Prefer", $"outlook.timezone=\"{user.MailboxSettings.TimeZone}\"")
                .Select(ev => new
                {
                    ev.Subject,
                    ev.Organizer,
                    ev.Start,
                    ev.End
                })
                .OrderBy("start/dateTime")
                .Top(50)
                .GetAsync();

            // TEMPORARY: Show the results as JSON
            Events.Text = JsonConvert.SerializeObject(events.CurrentPage);
        }
        catch (ServiceException ex)
        {
            ShowNotification($"Exception getting events: {ex.Message}");
        }

        base.OnNavigatedTo(e);
    }

    private static DateTime GetUtcStartOfWeekInTimeZone(DateTime today, string timeZoneId)
    {
        TimeZoneInfo userTimeZone = TimeZoneInfo.FindSystemTimeZoneById(timeZoneId);

        // Assumes Sunday as first day of week
        int diff = System.DayOfWeek.Sunday - today.DayOfWeek;

        // create date as unspecified kind
        var unspecifiedStart = DateTime.SpecifyKind(today.AddDays(diff), DateTimeKind.Unspecified);

        // convert to UTC
        return TimeZoneInfo.ConvertTimeToUtc(unspecifiedStart, userTimeZone);
    }
    ```

    <span data-ttu-id="797f4-109">コードの実行を `OnNavigatedTo` 検討してください。</span><span class="sxs-lookup"><span data-stu-id="797f4-109">Consider with the code in `OnNavigatedTo` is doing.</span></span>

    - <span data-ttu-id="797f4-110">呼び出される URL は `/me/calendarview` です。</span><span class="sxs-lookup"><span data-stu-id="797f4-110">The URL that will be called is `/me/calendarview`.</span></span>
        - <span data-ttu-id="797f4-111">パラメーター `startDateTime` は `endDateTime` 、カレンダー ビューの開始と終了を定義します。</span><span class="sxs-lookup"><span data-stu-id="797f4-111">The `startDateTime` and `endDateTime` parameters define the start and end of the calendar view.</span></span>
        - <span data-ttu-id="797f4-112">ヘッダーにより、ユーザーのタイム ゾーンでイベントと `Prefer: outlook.timezone` `start` `end` イベントが返されます。</span><span class="sxs-lookup"><span data-stu-id="797f4-112">The `Prefer: outlook.timezone` header causes the `start` and `end` of the events to be returned in the user's time zone.</span></span>
        - <span data-ttu-id="797f4-113">この `Select` 関数は、各イベントで返されるフィールドを、アプリが実際に使用するフィールドに制限します。</span><span class="sxs-lookup"><span data-stu-id="797f4-113">The `Select` function limits the fields returned for each event to just those the app will actually use.</span></span>
        - <span data-ttu-id="797f4-114">この `OrderBy` 関数は、結果を開始日時で並べ替える。</span><span class="sxs-lookup"><span data-stu-id="797f4-114">The `OrderBy` function sorts the results by the start date and time.</span></span>
        - <span data-ttu-id="797f4-115">この `Top` 関数は、最大で 50 のイベントを要求します。</span><span class="sxs-lookup"><span data-stu-id="797f4-115">The `Top` function requests at most 50 events.</span></span>

1. <span data-ttu-id="797f4-116">ファイル内 `NavView_ItemInvoked` のメソッドを `MainPage.xaml.cs` 変更して、既存のステートメントを次のステートメント `switch` に置き換える。</span><span class="sxs-lookup"><span data-stu-id="797f4-116">Modify the `NavView_ItemInvoked` method in the `MainPage.xaml.cs` file to replace the existing `switch` statement with the following.</span></span>

    ```csharp
    switch (invokedItem.ToLower())
    {
        case "new event":
            throw new NotImplementedException();
            break;
        case "calendar":
            RootFrame.Navigate(typeof(CalendarPage));
            break;
        case "home":
        default:
            RootFrame.Navigate(typeof(HomePage));
            break;
    }
    ```

<span data-ttu-id="797f4-117">これで、アプリを実行し、サインインして、左側のメニューの **予定表** ナビゲーション項目をクリックできます。</span><span class="sxs-lookup"><span data-stu-id="797f4-117">You can now run the app, sign in, and click the **Calendar** navigation item in the left-hand menu.</span></span> <span data-ttu-id="797f4-118">ユーザーの予定表にイベントの JSON ダンプが表示されます。</span><span class="sxs-lookup"><span data-stu-id="797f4-118">You should see a JSON dump of the events on the user's calendar.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="797f4-119">結果の表示</span><span class="sxs-lookup"><span data-stu-id="797f4-119">Display the results</span></span>

1. <span data-ttu-id="797f4-120">内容全体を次の `CalendarPage.xaml` 内容に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="797f4-120">Replace the entire contents of `CalendarPage.xaml` with the following.</span></span>

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

1. <span data-ttu-id="797f4-121">行 `CalendarPage.xaml.cs` を開き、 `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` 次の行に置き換える。</span><span class="sxs-lookup"><span data-stu-id="797f4-121">Open `CalendarPage.xaml.cs` and replace the `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` line with the following.</span></span>

    ```csharp
    EventList.ItemsSource = events.CurrentPage.ToList();
    ```

    <span data-ttu-id="797f4-122">アプリを今すぐ実行してカレンダーを選択すると、データ グリッド内のイベントの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="797f4-122">If you run the app now and select the calendar, you should get a list of events in a data grid.</span></span> <span data-ttu-id="797f4-123">ただし **、Start 値と** **End** 値は、ユーザーに対して分け方が悪い方法で表示されます。</span><span class="sxs-lookup"><span data-stu-id="797f4-123">However, the **Start** and **End** values are displayed in a non-user-friendly manner.</span></span> <span data-ttu-id="797f4-124">値コンバーターを使用して、これらの値の表示方法を [制御できます](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter)。</span><span class="sxs-lookup"><span data-stu-id="797f4-124">You can control how those values are displayed by using a [value converter](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).</span></span>

1. <span data-ttu-id="797f4-125">ソリューション エクスプローラーで **GraphTu solutionl** プロジェクトを右クリックし、[クラスの追加> **選択します**。クラスに名前を付 `GraphDateTimeTimeZoneConverter.cs` け、[追加] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="797f4-125">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > Class...**. Name the class `GraphDateTimeTimeZoneConverter.cs` and select **Add**.</span></span> <span data-ttu-id="797f4-126">ファイルの内容全体を次の内容に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="797f4-126">Replace the entire contents of the file with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/GraphDateTimeTimeZoneConverter.cs" id="ConverterSnippet":::

    <span data-ttu-id="797f4-127">このコードは、Microsoft Graph によって返される [dateTimeTimeZone](/graph/api/resources/datetimetimezone?view=graph-rest-1.0) 構造体を取得し、それをオブジェクトに解析 `DateTimeOffset` します。</span><span class="sxs-lookup"><span data-stu-id="797f4-127">This code takes the [dateTimeTimeZone](/graph/api/resources/datetimetimezone?view=graph-rest-1.0) structure returned by Microsoft Graph and parses it into a `DateTimeOffset` object.</span></span> <span data-ttu-id="797f4-128">次に、値をユーザーのタイム ゾーンに変換し、書式設定された値を返します。</span><span class="sxs-lookup"><span data-stu-id="797f4-128">It then converts the value into the user's time zone and returns the formatted value.</span></span>

1. <span data-ttu-id="797f4-129">要素 `CalendarPage.xaml` の前に次を開 **いて** 追加 `<Grid>` します。</span><span class="sxs-lookup"><span data-stu-id="797f4-129">Open `CalendarPage.xaml` and add the following **before** the `<Grid>` element.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="ResourcesSnippet":::

1. <span data-ttu-id="797f4-130">最後の 2 つの要素を `DataGridTextColumn` 次の要素に置き換える。</span><span class="sxs-lookup"><span data-stu-id="797f4-130">Replace the last two `DataGridTextColumn` elements with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="BindingSnippet" highlight="4,9":::

1. <span data-ttu-id="797f4-131">アプリを実行し、サインインして、[予定表] ナビゲーション **項目を** クリックします。</span><span class="sxs-lookup"><span data-stu-id="797f4-131">Run the app, sign in, and click the **Calendar** navigation item.</span></span> <span data-ttu-id="797f4-132">Start 値と End 値が書式設定 **されたイベントの** 一 **覧が** 表示されます。</span><span class="sxs-lookup"><span data-stu-id="797f4-132">You should see the list of events with the **Start** and **End** values formatted.</span></span>

    ![イベント表のスクリーンショット](./images/add-msgraph-01.png)
