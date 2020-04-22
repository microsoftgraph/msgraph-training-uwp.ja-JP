<!-- markdownlint-disable MD002 MD041 -->

この演習では、Microsoft Graph をアプリケーションに組み込みます。 このアプリケーションでは、microsoft [Graph クライアントライブラリ](https://github.com/microsoftgraph/msgraph-sdk-dotnet)を使用して microsoft graph を呼び出すことにします。

## <a name="get-calendar-events-from-outlook"></a>Outlook からカレンダー イベントを取得する

1. 予定表ビューの新しいページを追加します。 ソリューションエクスプローラーで**Graphtutorial**プロジェクトを右クリックし、[ **Add > New Item...**.] を選択します。[**空白のページ**] `CalendarPage.xaml`を選択し、[**名前**] フィールドに「」と入力して、[**追加**] を選択します。

1. を`CalendarPage.xaml`開き、次の行を既存`<Grid>`の要素の内側に追加します。

    ```xaml
    <TextBlock x:Name="Events" TextWrapping="Wrap"/>
    ```

1. を`CalendarPage.xaml.cs`開き、次`using`のステートメントをファイルの先頭に追加します。

    ```csharp
    using Microsoft.Toolkit.Graph.Providers;
    using Microsoft.Toolkit.Uwp.UI.Controls;
    using Newtonsoft.Json;
    ```

1. 次の関数を`CalendarPage`クラスに追加します。

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

    の`OnNavigatedTo`コードについて考えてみましょう。

    - 呼び出される URL は `/v1.0/me/events` です。
    - `Select` 関数は、各イベントに返されるフィールドを、ビューで実際に使用されるフィールドだけに制限します。
    - `OrderBy` 関数は、作成された日時で結果を並べ替えます。最新のアイテムが最初に表示されます。

1. ファイル内`NavView_ItemInvoked`のメソッドを変更して、既存`switch`のステートメントを次のように置き換えます。 `MainPage.xaml.cs`

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="SwitchStatementSnippet" highlight="4":::

これで、アプリを実行し、サインインして、左側のメニューの [**予定表**] ナビゲーション項目をクリックできるようになります。 ユーザーの予定表にあるイベントの JSON ダンプが表示されます。

## <a name="display-the-results"></a>結果の表示

1. の`CalendarPage.xaml`内容全体を次のように置き換えます。

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

1. を`CalendarPage.xaml.cs`開いて、 `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);`次の行に置き換えます。

    ```csharp
    EventList.ItemsSource = events.CurrentPage.ToList();
    ```

    今すぐアプリを実行して予定表を選択すると、イベントの一覧がデータグリッドに表示されます。 ただし、**開始**値と**終了**値は、非ユーザーフレンドリな方法で表示されます。 [値コンバーター](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter)を使用して、これらの値の表示方法を制御できます。

1. ソリューションエクスプローラーで**Graphtutorial**プロジェクトを右クリックし、[ **> クラスの追加**] を選択します。クラス`GraphDateTimeTimeZoneConverter.cs`の名前を指定して、[**追加**] を選択します。 ファイルの内容全体を次のように置き換えます。

    :::code language="csharp" source="../demo/GraphTutorial/GraphDateTimeTimeZoneConverter.cs" id="ConverterSnippet":::

    このコードでは、Microsoft Graph によって返された[dateTimeTimeZone](/graph/api/resources/datetimetimezone?view=graph-rest-1.0)構造`DateTimeOffset`体を取得し、それをオブジェクトに解析します。 その後、値をユーザーのタイムゾーンに変換し、書式設定された値を返します。

1. を`CalendarPage.xaml`開き、要素の`<Grid>` **前に**以下を追加します。

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="ResourcesSnippet":::

1. 最後の2つ`DataGridTextColumn`の要素を次のように置き換えます。

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="BindingSnippet" highlight="4,9":::

1. アプリを実行し、サインインして、**予定表**のナビゲーションアイテムをクリックします。 **開始**および**終了**の値が書式設定されたイベントの一覧が表示されます。

    ![イベント表のスクリーンショット](./images/add-msgraph-01.png)
