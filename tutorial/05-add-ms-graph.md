<!-- markdownlint-disable MD002 MD041 -->

この演習では、Microsoft Graph をアプリケーションに組み込む必要があります。 このアプリケーションでは [、.NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) 用 Microsoft Graph クライアント ライブラリを使用して Microsoft Graph を呼び出します。

## <a name="get-calendar-events-from-outlook"></a>Outlook からカレンダー イベントを取得する

1. 予定表ビューの新しいページを追加します。 ソリューション エクスプローラーで **GraphTu solutionl** プロジェクトを右クリックし、[新しいアイテムの> **を選択します**。Choose **Blank Page,** enter `CalendarPage.xaml` in the **Name** field, and select **Add**.

1. 既存 `CalendarPage.xaml` の要素内で次の行を開いて追加 `<Grid>` します。

    ```xaml
    <TextBlock x:Name="Events" TextWrapping="Wrap"/>
    ```

1. ファイル `CalendarPage.xaml.cs` の上部に `using` 次のステートメントを開いて追加します。

    ```csharp
    using Microsoft.Graph;
    using Microsoft.Toolkit.Graph.Providers;
    using Microsoft.Toolkit.Uwp.UI.Controls;
    using Newtonsoft.Json;
    ```

1. 次の関数をクラスに追加 `CalendarPage` します。

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

    コードの実行を `OnNavigatedTo` 検討してください。

    - 呼び出される URL は `/me/calendarview` です。
        - パラメーター `startDateTime` は `endDateTime` 、カレンダー ビューの開始と終了を定義します。
        - ヘッダーにより、ユーザーのタイム ゾーンでイベントと `Prefer: outlook.timezone` `start` `end` イベントが返されます。
        - この `Select` 関数は、各イベントで返されるフィールドを、アプリが実際に使用するフィールドに制限します。
        - この `OrderBy` 関数は、結果を開始日時で並べ替える。
        - この `Top` 関数は、最大で 50 のイベントを要求します。

1. ファイル内 `NavView_ItemInvoked` のメソッドを `MainPage.xaml.cs` 変更して、既存のステートメントを次のステートメント `switch` に置き換える。

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

これで、アプリを実行し、サインインして、左側のメニューの **予定表** ナビゲーション項目をクリックできます。 ユーザーの予定表にイベントの JSON ダンプが表示されます。

## <a name="display-the-results"></a>結果の表示

1. 内容全体を次の `CalendarPage.xaml` 内容に置き換えてください。

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

1. 行 `CalendarPage.xaml.cs` を開き、 `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` 次の行に置き換える。

    ```csharp
    EventList.ItemsSource = events.CurrentPage.ToList();
    ```

    アプリを今すぐ実行してカレンダーを選択すると、データ グリッド内のイベントの一覧が表示されます。 ただし **、Start 値と** **End** 値は、ユーザーに対して分け方が悪い方法で表示されます。 値コンバーターを使用して、これらの値の表示方法を [制御できます](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter)。

1. ソリューション エクスプローラーで **GraphTu solutionl** プロジェクトを右クリックし、[クラスの追加> **選択します**。クラスに名前を付 `GraphDateTimeTimeZoneConverter.cs` け、[追加] を **選択します**。 ファイルの内容全体を次の内容に置き換えてください。

    :::code language="csharp" source="../demo/GraphTutorial/GraphDateTimeTimeZoneConverter.cs" id="ConverterSnippet":::

    このコードは、Microsoft Graph によって返される [dateTimeTimeZone](/graph/api/resources/datetimetimezone?view=graph-rest-1.0) 構造体を取得し、それをオブジェクトに解析 `DateTimeOffset` します。 次に、値をユーザーのタイム ゾーンに変換し、書式設定された値を返します。

1. 要素 `CalendarPage.xaml` の前に次を開 **いて** 追加 `<Grid>` します。

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="ResourcesSnippet":::

1. 最後の 2 つの要素を `DataGridTextColumn` 次の要素に置き換える。

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="BindingSnippet" highlight="4,9":::

1. アプリを実行し、サインインして、[予定表] ナビゲーション **項目を** クリックします。 Start 値と End 値が書式設定 **されたイベントの** 一 **覧が** 表示されます。

    ![イベント表のスクリーンショット](./images/add-msgraph-01.png)
