<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="25171-101">このセクションでは、ユーザーの予定表にイベントを作成する機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="25171-101">In this section you will add the ability to create events on the user's calendar.</span></span>

1. <span data-ttu-id="25171-102">新しいイベント ビューの新しいページを追加します。</span><span class="sxs-lookup"><span data-stu-id="25171-102">Add a new page for the new event view.</span></span> <span data-ttu-id="25171-103">ソリューション エクスプローラーで **GraphTu solutionl** プロジェクトを右クリックし、[新しいアイテムの> **を選択します**。Choose **Blank Page,** enter `NewEventPage.xaml` in the **Name** field, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="25171-103">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `NewEventPage.xaml` in the **Name** field, and select **Add**.</span></span>

1. <span data-ttu-id="25171-104">**NewEventPage.xaml を開き**、その内容を次の内容に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="25171-104">Open **NewEventPage.xaml** and replace its contents with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/NewEventPage.xaml" id="NewEventPageXamlSnippet":::

1. <span data-ttu-id="25171-105">ファイル **NewEventPage.xaml.cs** を開き、ファイルの一番上に次 `using` のステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="25171-105">Open **NewEventPage.xaml.cs** and add the following `using` statements to the top of the file.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="UsingStatementsSnippet":::

1. <span data-ttu-id="25171-106">**INotifyPropertyChange** インターフェイスを **NewEventPage クラスに追加** します。</span><span class="sxs-lookup"><span data-stu-id="25171-106">Add the **INotifyPropertyChange** interface to the **NewEventPage** class.</span></span> <span data-ttu-id="25171-107">既存のクラス宣言を次に置き換える。</span><span class="sxs-lookup"><span data-stu-id="25171-107">Replace the existing class declaration with the following.</span></span>

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

1. <span data-ttu-id="25171-108">NewEventPage クラスに次 **のプロパティを追加** します。</span><span class="sxs-lookup"><span data-stu-id="25171-108">Add the following properties to the **NewEventPage** class.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="PropertiesSnippet":::

1. <span data-ttu-id="25171-109">次のコードを追加して、ページが読み込まれるときに Microsoft Graph からユーザーのタイム ゾーンを取得します。</span><span class="sxs-lookup"><span data-stu-id="25171-109">Add the following code to get the user's time zone from Microsoft Graph when the page loads.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="LoadTimeZoneSnippet":::

1. <span data-ttu-id="25171-110">イベントを作成するには、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="25171-110">Add the following code to create the event.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="CreateEventSnippet":::

1. <span data-ttu-id="25171-111">既存の `NavView_ItemInvoked` ステートメントを次 **MainPage.xaml.cs** 置き換える場合は、ファイル内のメソッド `switch` を変更します。</span><span class="sxs-lookup"><span data-stu-id="25171-111">Modify the `NavView_ItemInvoked` method in the **MainPage.xaml.cs** file to replace the existing `switch` statement with the following.</span></span>

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

1. <span data-ttu-id="25171-112">変更内容を保存し、アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="25171-112">Save your changes and run the app.</span></span> <span data-ttu-id="25171-113">サインインし、[新しい **イベント]** メニュー項目を選択してフォームに入力し、[作成] を選択してユーザーの予定表にイベントを追加します。</span><span class="sxs-lookup"><span data-stu-id="25171-113">Sign in, select the **New event** menu item, fill in the form, and select **Create** to add an event to the user's calendar.</span></span>

    ![新しいイベント ページのスクリーンショット](images/create-event-01.png)
