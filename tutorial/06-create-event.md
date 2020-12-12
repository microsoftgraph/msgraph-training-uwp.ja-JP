<!-- markdownlint-disable MD002 MD041 -->

このセクションでは、ユーザーの予定表にイベントを作成する機能を追加します。

1. 新しいイベント ビューの新しいページを追加します。 ソリューション エクスプローラーで **GraphTu solutionl** プロジェクトを右クリックし、[新しいアイテムの> **を選択します**。Choose **Blank Page,** enter `NewEventPage.xaml` in the **Name** field, and select **Add**.

1. **NewEventPage.xaml を開き**、その内容を次の内容に置き換えます。

    :::code language="xaml" source="../demo/GraphTutorial/NewEventPage.xaml" id="NewEventPageXamlSnippet":::

1. ファイル **NewEventPage.xaml.cs** を開き、ファイルの一番上に次 `using` のステートメントを追加します。

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="UsingStatementsSnippet":::

1. **INotifyPropertyChange** インターフェイスを **NewEventPage クラスに追加** します。 既存のクラス宣言を次に置き換える。

    ```csharp
    public sealed partial class NewEventPage : Page, INotifyPropertyChanged
    {
        public NewEventPage()
        {
            this.InitializeComponent();
            DataContext = this;
        }
    }
    ```

1. NewEventPage クラスに次 **のプロパティを追加** します。

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="PropertiesSnippet":::

1. 次のコードを追加して、ページが読み込まれるときに Microsoft Graph からユーザーのタイム ゾーンを取得します。

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="LoadTimeZoneSnippet":::

1. イベントを作成するには、次のコードを追加します。

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="CreateEventSnippet":::

1. 既存の `NavView_ItemInvoked` ステートメントを次 **MainPage.xaml.cs** 置き換える場合は、ファイル内のメソッド `switch` を変更します。

    ```csharp
    switch (invokedItem.ToLower())
    {
        case "new event":
            RootFrame.Navigate(typeof(NewEventPage));
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

1. 変更内容を保存し、アプリケーションを実行します。 サインインし、[新しい **イベント]** メニュー項目を選択してフォームに入力し、[作成] を選択してユーザーの予定表にイベントを追加します。

    ![新しいイベント ページのスクリーンショット](images/create-event-01.png)
